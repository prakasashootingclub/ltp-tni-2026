## graphify

This project's real backend code lives in `gas/` (gitignored -- never committed to git,
contains scanner/payment passwords and bank account details in CONFIG). The knowledge
graph was built pointing AT `gas/` specifically (not project root), using `--code-only`
(local AST extraction only, zero LLM/API calls, zero token cost -- confirmed in
GRAPH_REPORT.md). Graph lives at `gas/graphify-out/`, NOT `graphify-out/` at project root.

Rules:
- For codebase questions about the backend (Code.js, GantiJadwal.js, etc.), first run `graphify query "<question>" --graph gas/graphify-out/graph.json` when gas/graphify-out/graph.json exists. Use `graphify path "<A>" "<B>" --graph gas/graphify-out/graph.json` for relationships and `graphify explain "<concept>" --graph gas/graphify-out/graph.json` for focused concepts.
- Read gas/graphify-out/GRAPH_REPORT.md only for broad architecture review or when query/path/explain do not surface enough context.
- After modifying code in gas/, run `graphify update gas --code-only` to keep the graph current (AST-only, no API cost, no LLM exposure of the passwords/bank details embedded in Code.js).
- Do NOT run a plain `/graphify` or `graphify .` at project root -- it will skip gas/ (gitignored) and produce an empty/useless graph.
