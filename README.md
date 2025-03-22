# Trackeo AI

AI-powered platform for streamlining software development from idea to product.

## What's inside?

This monorepo uses [PNPM](https://pnpm.io) as a package manager and [Turborepo](https://turbo.build/repo) as a build system.

### Apps and Packages

- `apps/web`: Next.js application
- `apps/docs`: Storybook documentation
- `packages/ui`: Shared UI components
- `packages/config`: Shared configurations (eslint, typescript, etc.)
- `packages/utils`: Shared utilities

### Build

To build all apps and packages, run the following command:

```bash
pnpm build
```

### Develop

To develop all apps and packages, run the following command:

```bash
pnpm dev
```

### Remote Caching

Turborepo can use a technique known as Remote Caching to share cache artifacts across machines, enabling you to share build caches with your team and CI/CD pipelines.

By default, Turborepo will cache locally. To enable Remote Caching you will need to login to your Vercel account with:

```bash
npx turbo login
```

## Useful Links

Learn more about the power of Turborepo:

- [Tasks](https://turbo.build/repo/docs/core-concepts/monorepos/running-tasks)
- [Caching](https://turbo.build/repo/docs/core-concepts/caching)
- [Remote Caching](https://turbo.build/repo/docs/core-concepts/remote-caching)
- [Filtering](https://turbo.build/repo/docs/core-concepts/monorepos/filtering)
- [Configuration Options](https://turbo.build/repo/docs/reference/configuration)
- [CLI Usage](https://turbo.build/repo/docs/reference/command-line-reference)