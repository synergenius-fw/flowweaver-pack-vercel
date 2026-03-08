# @synergenius/flow-weaver-pack-vercel

Vercel Serverless Functions export target for [Flow Weaver](https://github.com/synergenius-fw/flow-weaver).

Generates Vercel-compatible serverless functions with file-based routing from Flow Weaver workflows.

## Installation

```bash
npm install @synergenius/flow-weaver-pack-vercel
```

This package is a **marketplace pack** — once installed, Flow Weaver automatically discovers it via `createTargetRegistry()`.

## Usage

### CLI

```bash
# Export a workflow as a Vercel serverless function
npx flow-weaver export my-workflow.ts --target vercel

# With options
npx flow-weaver export my-workflow.ts --target vercel --production --docs
```

### Programmatic

```typescript
import { createTargetRegistry } from '@synergenius/flow-weaver/deployment';

const registry = await createTargetRegistry(process.cwd());
const vercel = registry.get('vercel');

const artifacts = await vercel.generate({
  sourceFile: 'my-workflow.ts',
  workflowName: 'myWorkflow',
  displayName: 'my-workflow',
  outputDir: './dist/vercel',
  production: true,
});
```

## What it generates

- `api/<name>.ts` — Vercel handler (file-based routing)
- `vercel.json` — Function configuration
- `package.json` — Dependencies and scripts
- Optional: Swagger UI docs at `/api/docs`

Supports single workflow, multi-workflow (catch-all router), node type services, and bundle exports.

## Requirements

- `@synergenius/flow-weaver` >= 0.14.0

## License

See [LICENSE](./LICENSE).
