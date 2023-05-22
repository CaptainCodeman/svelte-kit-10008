## Example

Reproduction for [https://github.com/sveltejs/kit/issues/10008](https://github.com/sveltejs/kit/issues/10008)

Run `pnpm dev`, the expected `PUBLIC_API_KEY: my-personal-key-for-dev-only` appears on all pages.

Run `pnpm build` to compile with the Node adapter, then `pnpm start` to execute with a dynamic `.env` value. Initially the value is correct (`PUBLIC_API_KEY: proper-public-key`), but landing on the pre-rendered page (goto `http://localhost:3000/prerendered` and refresh) switches it to incorrectly use the dev-mode `.env` value for that and all subsequent pages.

The pre-rendered page has the dev mode `.env` value embedded, effectively changing it to be a static value. This can break the app and risks exposing something that wasn't _intended_ to be made public (despite it being a public variable).

```html
<script>
  {
    __sveltekit_o5vefy = {
      base: new URL(".", location).pathname.slice(0, -1),
      env: {"PUBLIC_API_KEY":"my-personal-key-for-dev-only"}
    };
```