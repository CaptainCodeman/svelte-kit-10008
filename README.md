## Example

Reproduction for [https://github.com/sveltejs/kit/issues/10008](https://github.com/sveltejs/kit/issues/10008)

Run `pnpm dev`, the expected `PUBLIC_API_KEY: my-personal-key-for-dev-only` appears on all pages.

Run `pnpm build` to compile with the Node adapter, then `pnpm start` to execute with a dynamic `.env` value. Initially the value is correct (`PUBLIC_API_KEY: proper-public-key`), but landing on the pre-rendered page (goto `http://localhost:3000/prerendered` and refresh) switches it to incorrectly use the dev-mode `.env` value for that and all subsequent pages.