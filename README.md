# capnweb-better-types

Temporary package that ships a copy of `dist/index.d.ts` from:
https://github.com/cloudflare/capnweb/pull/142

Use this only until that PR is merged and released in `capnweb`.

## Install

```bash
npm i capnweb
npm i -D capnweb-better-types
```

## Use

### Option 1: Import utility types directly

Import types directly:

```ts
import type { RpcCompatible, Stub, Stubify, Provider } from "capnweb-better-types";
```

Runtime imports still come from `capnweb`.

### Option 2: Override `capnweb` type inference (recommended)

Add this to your project `tsconfig.json`:

```json
{
  "compilerOptions": {
    "paths": {
      "capnweb": ["./node_modules/capnweb-better-types/capnweb"]
    }
  }
}
```

This replaces only TypeScript's module declaration resolution for `"capnweb"`.
Runtime still resolves to the real `capnweb` package.

If you use `skipLibCheck: false`, current upstream build output may hit TypeScript `TS2574`.
Temporary workaround: set `skipLibCheck: true` until upstream release.

## How this file is obtained (future updates)

When you want to refresh this package with newer upstream types:

```bash
# from the capnweb repo root
npm run build
cp dist/index.d.ts capnweb-better-types/capnweb.d.ts
```

Then bump `capnweb-better-types` version and publish.
