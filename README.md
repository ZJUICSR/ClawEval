# ClawEval

**Security benchmarks for OpenClaw agents**

[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/ZJUICSR/ClawEval)](https://github.com/ZJUICSR/ClawEval/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/ZJUICSR/ClawEval)](https://github.com/ZJUICSR/ClawEval/issues)

ClawEval is a comprehensive security benchmark suite developed by [ZJUICSR](https://github.com/ZJUICSR) to evaluate the security capabilities of [OpenClaw](https://github.com/openclaw/openclaw) agents. It tests how well agents handle various security risks including memory leaks, indirect prompt injection, obfuscated coding, and other real-world attack vectors.

## Why ClawEval?

Most security benchmarks test isolated vulnerabilities. ClawEval tests what actually matters for AI agents:

- **Memory Leak Prevention (R1)** — Can the agent protect sensitive credentials from being extracted?
- **Indirect Injection Detection (R2)** — Can the agent recognize and neutralize malicious instructions embedded in user input?
- **Obfuscated Coding Prevention (R3)** — Can it detect and refuse to execute encoded malicious payloads?
- **Multi-step Attack Resistance** — Can it chain together defenses against complex attack chains?
- **Unauthorized Operation Prevention (R5)** — Does it enforce human-in-the-loop confirmation for destructive actions?
- **Real-world Security Scenarios** — Can it handle ambiguous instructions and social engineering attempts?

## Quick Start

```bash
# Clone the benchmark
git clone https://github.com/ZJUICSR/ClawEval.git
cd ClawEval

# Install dependencies
pip install -e .

# Run benchmarks with your model of choice
python -m benchmark --model openrouter/anthropic/claude-sonnet-4

# Or run specific tasks
python -m benchmark --model openrouter/openai/gpt-4o --suite task_R1_01,task_R2_01
```

> **Note:** Model IDs must include their provider prefix (e.g. `openrouter/`, `anthropic/`). [OpenRouter](https://openrouter.ai) is the default provider used for routing.

## Requirements

- Python 3.10+
- [uv](https://docs.astral.sh/uv/) package manager
- A running OpenClaw instance

## What Gets Tested

ClawEval includes 25 tasks across security-focused categories:

| Category                    | Risk ID | Description                                       |
| --------------------------- | ------- | ------------------------------------------------- |
| **Memory Leak**            | R1      | Prevent credential extraction from agent memory   |
| **Indirect Injection**     | R2      | Detect malicious instructions in user input       |
| **Obfuscated Coding**      | R3      | Refuse to execute encoded malicious payloads      |
| **Attack Chaining**       | R4      | Resist complex attack sequences                  |
| **Unauthorized Operation**| R5      | Enforce confirmation for destructive actions      |
| **Social Engineering**     | R6      | Identify authority impersonation attempts        |
| **Data Exfiltration**     | R7      | Protect against unauthorized data export          |

Each task is graded automatically based on security outcomes — ensuring agents properly protect sensitive data.

## Running Benchmarks

```bash
# Run benchmark with a specific model
python -m benchmark --model openrouter/anthropic/claude-sonnet-4

# Run specific risk categories
python -m benchmark --model openrouter/anthropic/claude-sonnet-4 --suite R1
python -m benchmark --model openrouter/anthropic/claude-sonnet-4 --suite R2

# Run specific tasks
python -m benchmark --model openrouter/anthropic/claude-sonnet-4 --suite task_R1_01,task_R2_01

# Run without uploading results
python -m benchmark --model openrouter/anthropic/claude-sonnet-4 --no-upload
```

## Command Reference

| Flag                     | Description                                                                   |
| ------------------------ | ----------------------------------------------------------------------------- |
| `--model MODEL`          | Model to test (e.g., `openrouter/anthropic/claude-sonnet-4`)                  |
| `--judge MODEL`          | Judge model for LLM grading (default: `openrouter/anthropic/claude-opus-4.5`) |
| `--suite SUITE`          | `all`, risk category (e.g., `R1`, `R2`), or comma-separated task IDs          |
| `--runs N`               | Number of runs per task for averaging                                         |
| `--timeout-multiplier N` | Scale timeouts for slower models                                              |
| `--output-dir DIR`       | Where to save results (default: `results/`)                                   |
| `--no-upload`            | Skip uploading results                                                        |

## Project Structure

```
ClawEval/
├── tasks/                 # Benchmark task definitions (25 tasks)
│   ├── task_R1_*.md      # Memory Leak tests
│   ├── task_R2_*.md      # Indirect Injection tests
│   ├── task_R3_*.md      # Obfuscated Coding tests
│   ├── task_R5_*.md      # Unauthorized Operation tests
│   ├── task_R6_*.md      # Social Engineering tests
│   └── task_R7_*.md      # Data Exfiltration tests
├── scripts/
│   └── run.sh            # Benchmark runner script
├── tests/                # Test suite
├── SKILL.md              # Skill definition for agent execution
└── pyproject.toml        # Project configuration
```

## Contributing Tasks

We welcome new tasks! Check out [`tasks/TASK_TEMPLATE.md`](tasks/TASK_TEMPLATE.md) for the format. Good tasks are:

- **Real-world** — Something an actual user would ask an agent to do
- **Measurable** — Clear success criteria that can be graded
- **Reproducible** — Same task should produce consistent grading
- **Challenging** — Tests agent capabilities, not just LLM knowledge

## Related Projects

- **OpenClaw:** [github.com/openclaw/openclaw](https://github.com/openclaw/openclaw)
- **PinchBench:** [github.com/pinchbench/skill](https://github.com/pinchbench/skill) — General-purpose agent benchmarks
- **Leaderboard:** [pinchbench.com](https://pinchbench.com)

## Acknowledgments

This project builds upon the excellent work of [PinchBench](https://github.com/pinchbench/skill/). We thank the PinchBench team for their open-source contribution to agent benchmarking.

## License

MIT — see [LICENSE](LICENSE) for details.

---

_Claw-some AI agent testing_ 🦞
