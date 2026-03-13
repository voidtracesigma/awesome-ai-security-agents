# excalibur
The paper studies **LLM-based penetration-testing agents** and evaluates whether architectural innovations or model capability primarily drive performance improvements.

**Evaluation setup.**
Five existing agents—PentestGPT, AutoPT, PentestAgent, VulnBot, and Cochise—are benchmarked using multiple frontier models. Experiments use three environments:

* **XBOW**: 104 web exploitation tasks. ([xbow.com][1])
* **PentestGPT benchmark**: 13 end-to-end vulnerable machines.
* **GOAD**: multi-host Active Directory attack environment.

**Empirical findings.**

1. Across benchmarks, **architectural differences between agents shrink as model capability increases**, indicating that many current design tricks compensate for model weaknesses rather than solving core pentesting challenges.
2. Failure analysis of **200 unsuccessful traces** shows two main categories:

   * **Capability gaps (~42%)**: missing tools, syntax errors, knowledge gaps.
   * **Complexity barriers (~58%)**: long-horizon planning, context loss, premature commitment, and exploration-exploitation failures.
3. Tool improvements significantly reduce capability failures (e.g., improved tool documentation increased success from **27% → 38%** on XBOW).
4. However, **complex multi-step environments (e.g., GOAD)** remain largely unsolved even with better tooling.

**Proposed direction.**
The paper introduces **PentestGPT-V2**, emphasizing **explicit search behavior (branching, backtracking, and hypothesis pruning)** to address long-horizon attack planning. This approach substantially improves success rates on web exploitation benchmarks compared with prior agents.

[1]: https://xbow.com/blog/benchmarks?utm_source=chatgpt.com "XBOW - XBOW validation benchmarks: show me the numbers!"



---

# 1. Problem Statements and Claims

### Claims about current LLM penetration-testing agents

1. Recent systems report strong results on benchmarks such as **CTF challenges and Hack The Box environments**. ([arXiv][1])
2. Some prior work has **discovered exploitable vulnerabilities in production software** using LLM agents. ([arXiv][1])
3. Reported **task completion rates range from single digits to 40–80%** depending on architecture and prompting sophistication. ([arXiv][1])
4. Existing agent designs focus on **compensating for model limitations rather than solving intrinsic penetration-testing challenges**. ([arXiv][1])

### Claim about model improvements

5. As LLM capabilities improve, **performance differences between architectures shrink**. ([arXiv][1])

### Claim about persistent vs transient challenges

6. Some difficulties are **transient model limitations**:

   * context window limits
   * instruction-following reliability
   * weak domain knowledge
   * tool-use reliability. ([arXiv][1])

7. Other difficulties are **persistent structural challenges**:

   * long-horizon planning across 10+ steps
   * exploration vs exploitation decisions
   * maintaining state outside the context window
   * assessing task difficulty during execution. ([arXiv][1])

### Claim (Finding 1)

8. Existing penetration-testing agents primarily **address transient model limitations rather than persistent task challenges**. ([arXiv][1])

---

# 2. Systems Evaluated

The study evaluates **five open-source penetration-testing agent systems**:

1. PentestGPT
2. AutoPT
3. PentestAgent
4. VulnBot
5. Cochise

Each system represents a different architecture type:

| System       | Type                         |
| ------------ | ---------------------------- |
| PentestGPT   | human-in-the-loop copilot    |
| AutoPT       | single-agent                 |
| PentestAgent | multi-agent with RAG         |
| VulnBot      | multi-agent tri-phase        |
| Cochise      | AD-focused specialized agent |

([arXiv][1])

---

# 3. Benchmarks Used

Three benchmark environments are used:

### 1. XBOW benchmark

* 104 web exploitation challenges
* Vulnerability types include:

  * SQL injection
  * Cross-site scripting
  * authentication bypass. ([arXiv][1])

### 2. PentestGPT Benchmark

* 13 machines
* derived from Hack The Box and VulnHub
* requires **end-to-end penetration testing**. ([arXiv][1])

### 3. GOAD benchmark

* Active Directory environment
* 5 hosts
* requires **multi-host chained attacks**. ([arXiv][1])

---

# 4. Models Used in Experiments

Each agent is tested with the following models:

1. GPT-4o
2. GPT-5
3. Gemini-3-Flash
4. Claude Sonnet 4

([arXiv][1])

Additional experiments evaluate:

5. GPT-5.2
6. Opus 4.5
7. Gemini 3 Pro

for extended-reasoning comparisons. ([arXiv][1])

---

# 5. Experimental Protocol

1. Temperature is set to **0**.
2. Results are reported using **best-of-three trials**.
3. The reason for best-of-three: **penetration testing is inherently non-deterministic**. ([arXiv][1])

---

# 6. Experiment Results — Baseline Systems

## 6.1 XBOW benchmark (104 tasks)

| System       | GPT-4o | GPT-5 | Gemini | Claude |
| ------------ | ------ | ----- | ------ | ------ |
| PentestGPT   | 27%    | 42%   | 36%    | 39%    |
| AutoPT       | 28%    | 40%   | 35%    | 37%    |
| PentestAgent | 34%    | 49%   | 42%    | 46%    |
| VulnBot      | 39%    | 45%   | 44%    | 46%    |
| Cochise      | 34%    | 43%   | 39%    | 39%    |

([arXiv][1])

---

## 6.2 PentestGPT Benchmark (13 machines)

| System       | GPT-4o | GPT-5 | Gemini | Claude |
| ------------ | ------ | ----- | ------ | ------ |
| PentestGPT   | 5      | 7     | 6      | 6      |
| AutoPT       | 4      | 7     | 6      | 6      |
| PentestAgent | 6      | 7     | 6      | 6      |
| VulnBot      | 6      | 8     | 6      | 7      |
| Cochise      | 4      | 4     | 4      | 4      |

([arXiv][1])

---

## 6.3 GOAD Benchmark (5 hosts)

| System       | GPT-4o | GPT-5 | Gemini | Claude |
| ------------ | ------ | ----- | ------ | ------ |
| PentestGPT   | 0      | 1     | 1      | 1      |
| AutoPT       | 0      | 1     | 0      | 0      |
| PentestAgent | 0      | 1     | 0      | 1      |
| VulnBot      | 0      | 1     | 0      | 1      |
| Cochise      | 1      | 2     | 2      | 2      |

([arXiv][1])

---

# 7. Architectural Convergence Observation

### XBOW

* GPT-4o completion rates range **27%–39%** across agents.
* Relative spread **44%** between worst and best system. ([arXiv][1])

### GPT-5

* Completion rates **40%–49%**.
* Spread narrows to **22.5%**. ([arXiv][1])

### PentestGPT benchmark

* GPT-4o: **4–6 machines solved**.
* GPT-5: **7–8 machines solved**. ([arXiv][1])

Claim:

* **Architectural advantage shrinks as model capability increases**. ([arXiv][1])

---

# 8. Failure Mode Study

## Dataset

* 200 execution traces
* 40 traces per system
* traces sampled from unsuccessful runs. ([arXiv][1])

### Annotation method

* Two researchers independently coded failure modes.
* Disagreements resolved through discussion. ([arXiv][1])

---

# 9. Failure Categories

Two categories are defined.

## Type A — Capability Gaps (42%)

Examples:

* missing tool
* incorrect command syntax
* output parsing errors
* missing knowledge. ([arXiv][1])

Frequency:

| Failure type                    | Percentage |
| ------------------------------- | ---------- |
| Missing tool / incorrect syntax | 26%        |
| Output parsing / knowledge gap  | 16%        |

([arXiv][1])

---

## Type B — Complexity Barriers (58%)

Examples:

* context forgetting
* premature commitment
* exploration-exploitation imbalance
* multi-step chain failures. ([arXiv][1])

Frequency:

| Failure type                       | Percentage |
| ---------------------------------- | ---------- |
| Context forgetting                 | 18%        |
| Premature commitment               | 16%        |
| Exploration-exploitation imbalance | 12%        |
| Multi-step chain failures          | 12%        |

([arXiv][1])

---

# 10. Tooling Intervention Experiment

Experiment:

* Add missing tool documentation and usage instructions to PentestGPT.

Result:

* XBOW completion improves **27% → 38%**.

Relative improvement:

* **41% increase**. ([arXiv][1])

Claim:

* Type A failures respond to **capability engineering**. ([arXiv][1])

---

# 11. Complexity vs Task Depth Result

Observation:

Task complexity measured by number of attack steps.

### XBOW tasks

* typically **1–3 steps**
* **68% of failures resolvable via tooling**. ([arXiv][1])

### GOAD tasks

* require **5–10 attack steps**
* **79% of failures persist regardless of tooling improvements**. ([arXiv][1])

Claim:

* As task depth increases, **complexity failures dominate**. ([arXiv][1])

---

# 12. PENTESTGPT V2 Performance Results

### XBOW benchmark

| Model                  | Completion      |
| ---------------------- | --------------- |
| Opus 4.5 thinking mode | 91% (best-of-3) |
| GPT-5.2 thinking       | 85%             |

Statistics:

* Opus 4.5 mean: **89%**, σ = 2.1
* GPT-5.2 mean: **83%**, σ = 2.4. ([arXiv][1])

Comparison baseline:

* Best baseline system (PentestAgent) = **61%** mean success. ([arXiv][1])

Relative improvement:

* ~49% relative increase vs baseline. ([arXiv][1])

---

# 13. Search Behavior Metrics

Comparison between PentestGPT and PENTESTGPT V2.

| Metric                 | PentestGPT | PENTESTGPT V2 |
| ---------------------- | ---------- | ------------- |
| Branches explored      | 3.2        | 7.8           |
| Backtrack rate         | 8%         | 34%           |
| Avg depth before pivot | 12.4       | 5.1           |
| Successful pivots      | 0.4        | 2.6           |
| Pruned branches        | –          | 4.2           |

([arXiv][1])

---

# 14. Tool Layer Result

Observation:

* Tool-layer improvements **produce zero improvement on GOAD**, which remains **2 hosts compromised**. ([arXiv][1])

Claim:

* Complex environments require **planning improvements rather than capability improvements**. ([arXiv][1])

---
