Run the cpp-cg-tidy agent to audit C++ code against the C++ Core Guidelines.

Target: $ARGUMENTS

If no target is specified, audit the entire codebase. If a directory or file path is provided, focus the audit on that scope.

The agent will fetch guideline definitions on-demand from `CppCoreGuidelines.md` using the anchor-based lazy-loading approach defined in AGENT.md.

Produce a structured audit report with:
- Executive summary (files analyzed, compliance score, issue counts)
- Findings by guideline (violations with file:line references, severity, suggested fixes)
- Summary statistics table
- Prioritized recommendations
