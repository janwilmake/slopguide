# Generate 'SLOP Guides'

> Dependant on openapi and typedoc work as zipobject plugins

This can be done separately and is fun! For any codebase, I can:

- If server, get the openapi and with that, the overview SLOP for it
- If not server, get the typedoc (or similar for other languages)
- Use `guides.json` (if present at server root)
- If no guides.json, generate `type Guides = { usecase: string, operationIds: string[] }[]` from overview SLOP.
- For each usecase, get the context full openapi context required for it as YAML. For typedoc we can use function names being the operationIds.
- Generate the usecase guide using that context.

For every codebase (focus on major packages and APIs of popular repos), I could use this to generate guides for major programming languages, and make it available in uithub.

The next step would be to require all guides of all your dependencies and api-dependencies for any codebase, via `guides.zipobject.com`. An LLM will now have a much easier time to follow instructions because it can first pick a guide, then follow it.
