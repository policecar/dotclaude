Run the cpp-guidelines-auditor agent to audit C++ code against the C++ Core Guidelines.

Target: $ARGUMENTS

If no target is specified, audit the entire codebase. If a directory or file path is provided, focus the audit on that scope.

Load the guideline definitions from `.claude/agents/cpp-cg-auditor/CppCoreGuidelines.md` before auditing. Each guideline sections contains the official reasoning, examples, exceptions, and enforcement guidance.

Produce a structured audit report with:
- Executive summary (files analyzed, compliance score, issue counts)
- Findings by guideline (violations with file:line references, severity, suggested fixes)
- Summary statistics table
- Prioritized recommendations

