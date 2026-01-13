# Background
The following repository is a repository that contains Typescript code.
The repository may be either a single module or a monorepo comprising several modules
Each module will have its own `package.json` file - and there is likely a top-level module with its own top-level `package.json` file.


# Typescript best practices
- Do not use `any`. Any is not a typesafe value, and therefore, the benefits of Typescript are thrown away when this is used. If you really believe you have a valid reason to use any, you should always ask the user's permission to use it.
- Whenever you work on a module, it is important to use TypeScript `typecheck` scripts regularly to ensure that the code you are writing is not incorrect. Again, if you do not respect types in TypeScript. This is will throw away the benefits of the language.
- If there are no `typecheck` commands for some reason, you probably should let the user know, but you can instead opt to use whatever typechecker seems reasonable.
- Speaking of `package.json`, typically the most important commands are stored in there. If at all possible, you should always look there first and opt to use the `package.json` commands BEFORE deciding to run them directly (for example using `npx`)
- Additionally, avoid typecasting where possible, e.g. `as type`. Ideally, all types can be inferred, and it shouldn't need to be cast. If you believe the user's repository is insufficient and requires a typecast, then you should let them know this and ask if its ok.
- Use `as const` for literal inference instead of widened types
- Validate external data at runtime boundaries (e.g., with Zod)
- Under no circumstances should you use @ts-ignore unless the user has strictly asked for it.
- Never just copy and paste new type definitions. Instead, deriving them (typeof, ReturnType<T>, mapped types)
- Wherever you can favour using `Suspense` and `ErrorBoundary` so that you can handle loading and errors gracefully without needing extra complicated and repeated logic.
- Also, consider useMemo when it would have decent performance gains.
- Try to split Large components into smaller ones if it makes sense to, and if there are potentially reusable aspects of the component, or if you can separate out logic for sub-components to improve clarity.
- Always favour using an existing component for something if one exists - you should check - and consider even modifying components slightly to fit more use cases if that makes sense in the context of the problem.

# Understanding Complicated Frameworks with CONTEXT7 MCP (IF YOU DON'T HAVE ACCESS TO THI'S TELL THE USER)
- Web is complicated and often requires importing tens or even hundreds of packages. Good developers look at documentation before implementing to ensure they are using best practices.
- You, as a good developer, should use the CONTEXT7 MCP whenever you need to look into any framework or library at all. Never, ever, guess syntax or best practices and always look up the appropriate version of the library as per the version specified in `package.json`.

# Tanstack Router Specific
- Tanstack router gives you the option to get parameters like `isError` from queries. Ideally, instead of doing this, handle these cases inside the query itself by using the `onError` and `onSuccess` handlers when appropriate. Note this is not always reasonable, but often with things like `useMutation` it is very beneficial.
- Similarly, Suspense in React is really powerful - don't do checks for `isLoading` - just suspend until the response comes back and handle errors gracefully.
- Always use appropriate QueryKeys to ensure that queries refetch when specific values change.
