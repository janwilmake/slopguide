# Generate Typedoc

This will need to be done on vercel and can be done when filtering on ts(x) and then finding the common basepath:

https://www.npmjs.com/package/typedoc
https://www.npmjs.com/package/typedoc-plugin-markdown

This will provide super accurate docs for all functions in a short format, and it's pretty much free to do.

1. typedoc-zipobject.vercel.app using zipobject.vercel.app
2. make available in context.forgithub.com

# Generate OpenAPI

If we can generate an OpenAPI programatically, we have a huge moat as it's not that straightforward. How this should be done:

1. Identify all code files
2. If it's more than 50k tokens, fail it for now. Codebase too large. ❌
3. Determine if it's a server or not using an analysis question returning a boolean. If `false` cancel early ❌
4. Figure out the server with domain.zipobject.com. If we have no domain, cancel early. ❌
5. Determine if the server proxies a response from another server making the type interfaces unclear. Cancel early for this case ❌
6. Ask Deepseek to generate the OpenAPI spec

This ties into https://github.com/janwilmake/slopguide perfectly. Let's allow generating the openapi spec via uithub somehow. Main learning: forgithub.analysis is a bit too generic for most interesting use-cases.

# Generate SLOP Guides

This can be done separately and is fun! For any codebase, I can:

- If server, get the openapi and with that, the overview SLOP for it
- If not server, get the typedoc (or similar for other languages)
- Use `guides.json` (if present at server root)
- If no guides.json, generate `type Guides = { usecase: string, operationIds: string[] }[]` from overview SLOP.
- For each usecase, get the context full openapi context required for it as YAML. For typedoc we can use function names being the operationIds.
- Generate the usecase guide using that context.

For every codebase (focus on major packages and APIs of popular repos), I could use this to generate guides for major programming languages, and make it available in uithub.

The next step would be to require all guides of all your dependencies and api-dependencies for any codebase, via `guides.zipobject.com`. An LLM will now have a much easier time to follow instructions because it can first pick a guide, then follow it.
