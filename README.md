# Root.io AI Engineer - Home Assignment

## Overview

This assignment evaluates your ability to **build autonomous AI agents** that can analyze code, identify vulnerabilities, and determine appropriate fixes.

**The Challenge:** Build an AI agent that discovers and fixes a CWE-22 (Path Traversal) vulnerability without being told what the vulnerability is or how to fix it.

## What You're Given

1. **Vulnerable Code**: `file_reader.py` - contains a security vulnerability
2. **Test Suite**: `test_file_reader.py` - defines expected security behavior (2 tests currently FAIL)
3. **Context**: The vulnerability is CWE-22 related (for your research)

**Resources for your research:**
- [CWE-22 Details](https://cwe.mitre.org/data/definitions/22.html)
- [OWASP Path Traversal](https://owasp.org/www-community/attacks/Path_Traversal)

## Your Goal

**Build an autonomous agent (`agent.py`) that:**

1. **Analyzes** the code to identify what vulnerability exists and where
2. **Determines** what type of fix is needed based on its analysis
3. **Generates** and applies the appropriate fix
4. **Validates** that all tests pass

## Key Requirement: Autonomy

⚠️ **Critical:** Your agent must autonomously analyze and determine the fix.

**What this means:**
- ✅ Agent reads the code and identifies the vulnerability through analysis
- ✅ Agent determines the fix strategy based on its understanding
- ✅ Agent can explain what it found and why its fix is appropriate
- ❌ Do NOT hardcode the vulnerability type in your agent's logic
- ❌ Do NOT hardcode fix instructions in your prompts (e.g., "use pathlib and resolve()")
- ❌ Do NOT tell the LLM what CWE-22 is or how to fix it

**Think of it this way:** If we replaced `file_reader.py` with a different vulnerability (SQL injection, XSS, etc.), would your agent still work? If not, it's not truly autonomous.

## What We're Evaluating

**Autonomous AI agent capability** - Does your agent analyze, determine, and report on its findings independently?

## Getting Started

### 1. Setup Environment

```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 2. Verify the Vulnerability Exists

```bash
pytest test_file_reader.py -v
```

You should see 2 tests **FAIL**.

### 3. Research CWE-22

- Understand what path traversal vulnerabilities are
- Learn about common attack patterns
- Research remediation approaches
- **Use this knowledge to inform your agent's design, not to hardcode solutions**

### 4. Build Your Agent

Your agent should have distinct phases:

**Analysis Phase:**
- Read and analyze `file_reader.py`
- Identify security issues
- Determine vulnerability type

**Fix Generation Phase:**
- Based on the analysis, determine appropriate fix
- Generate secure code

**Validation Phase:**
- Apply the fix
- Run tests to verify

**Reporting Phase:**
- Generate REPORT.md with findings and analysis

### 5. Run and Verify

```bash
python agent.py                 # Should analyze, fix, and generate REPORT.md
pytest test_file_reader.py -v  # All tests should PASS
```

## Deliverables

### 1. `agent.py` - Your AI Agent

Your agent must:
- Analyze code to identify vulnerabilities
- Determine appropriate fixes autonomously
- Apply the fix to `file_reader.py`
- Generate a `REPORT.md` with its findings and analysis
- Be runnable via: `python agent.py`

### 2. `REPORT.md` - Auto-Generated Report

**Your agent should automatically generate this report** with:
- What vulnerability was identified and where
- How the agent analyzed the code
- What fix was determined and why
- Performance metrics (time, API calls, iterations)
- Test results

See `REPORT_TEMPLATE.md` for the expected structure.

### 3. `requirements.txt`

List all dependencies your agent needs.

## Rules & Guidelines

- ✅ **Use any LLM APIs**: OpenAI, Anthropic, etc.
- ✅ **Use any libraries**: Static analysis tools, security scanners, etc.
- ✅ **Partial submissions OK**: Submit what you have if time runs out
- ⏱️ **Time limit**: Up to 3 hours
- 🚫 **Don't modify tests**: They define the security requirements
- 🚫 **Don't hardcode solutions**: Agent must discover and determine autonomously

## Common Pitfalls to Avoid

❌ **Prescriptive prompts** like:
```
"Fix the CWE-22 path traversal vulnerability using pathlib.resolve() 
and checking if the path is inside the base directory"
```

✅ **Autonomous prompts** like:
```
"Analyze this code for security vulnerabilities. Identify any issues 
and determine appropriate fixes."
```

❌ **Assuming vulnerability type**:
```python
# Don't do this:
prompt = "Fix the path traversal in file_reader.py"
```

✅ **Discovering vulnerability type**:
```python
# Do this:
analysis = agent.analyze_code("file_reader.py")
vulnerability_type = analysis.identify_vulnerabilities()
fix = agent.determine_fix(vulnerability_type)
```

## Questions?

Remember: We're evaluating your ability to build **autonomous AI agents**, not your ability to write prompts that instruct LLMs. Show us you can build systems that reason and analyze.

Good luck! 🚀
