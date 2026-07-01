# Streaming (SSE/WebSocket) Test Pattern

Standard route mocking (`route.fulfill()`) closes the response body immediately, which breaks streaming connections. Override `window.fetch` to return a `Response` whose body is a long-lived `ReadableStream`.

```ts
await page.addInitScript({
  fn: (arg) => {
    const origFetch = window.fetch;
    window.fetch = async (input, init) => {
      const url = String(input);
      if (url.includes('/api/stream/') && init?.method !== 'POST') {
        const body = new ReadableStream({
          start(controller) {
            const enc = new TextEncoder();
            for (const evt of arg.events) controller.enqueue(enc.encode(evt));
            // DO NOT call controller.close() — keep the stream open.
          },
        });
        return new Response(body, {
          headers: { 'Content-Type': 'text/event-stream', 'Cache-Control': 'no-cache' },
        });
      }
      return origFetch(input, init);
    };
  },
  arg: { events: ['event: connected\ndata: {"sessionId":"s1"}\n\n'] },
});
```

- **Never call `controller.close()`** — the client treats a closed stream as a disconnect.
- Keep test SSE frames aligned with the **real event names** the client expects.
- Pass through non-streaming requests (POST to send, etc.) to their own mocks.
- Revisit periodically: if the test runner adds native streaming support, this override may become unnecessary.

<!--
Fill in:
- The streaming URL pattern and the real event names (e.g. connected/chunk/done/error).
- The POST/companion request contract, if any.
-->
