# TermiAgent



**Essential information needed to understand the paper’s contribution (≤200 words):**

The paper addresses the gap between **CTF-style benchmarks and real-world penetration testing**. Existing AI pentesting agents are mostly evaluated on simplified CTF environments that embed prior knowledge and reduce environmental complexity, causing inflated performance estimates and poor real-world generalization. ([遇见数据集][1])

To address this, the authors introduce **TermiBench**, a real-world, agent-oriented pentesting benchmark where the goal is **obtaining an interactive system shell rather than finding flags**. The benchmark contains **510 hosts across 25 services and 30 CVEs (2015–2025)**. Each host includes one vulnerable service and up to seven benign services, forcing agents to perform **autonomous reconnaissance, service discrimination, and exploit execution without prior hints**. ([遇见数据集][1])

The paper also proposes **TermiAgent**, a multi-agent penetration-testing framework designed for this benchmark. Key components include:

* **Located Memory Activation (LMA)** to mitigate long-context forgetting during multi-step attacks.
* An **Arsenal module** that converts real exploit code into standardized modules using a **Unified Exploit Descriptor (UED)**, enabling reliable exploit execution. ([Emergent Mind][2])

Experiments show that existing pentesting agents rarely obtain shells under realistic conditions, while **TermiAgent achieves significantly higher success**, obtaining more shells than prior systems while reducing execution time and cost. ([Emergent Mind][2])

The paper contributes **(1) the first realistic autonomous pentesting benchmark and (2) a memory-augmented agent framework capable of operating in real-world-like environments.**

[1]: https://www.selectdataset.com/dataset/7f8f87f49985a836a25c6c116e3838d5?utm_source=chatgpt.com "TermiBench|渗透测试数据集|信息安全数据集"
[2]: https://www.emergentmind.com/topics/termibench?utm_source=chatgpt.com "TermiBench: Autonomous Pentest Benchmark"




---

# Concrete Claims

### About the problem and existing work

1. Traditional penetration testing is expensive, time-consuming, and dependent on expert human labor. ([arXiv][1])
2. Existing AI-driven pentesting research evaluates systems mainly in **CTF-style environments**. ([arXiv][1])
3. CTF benchmarks embed prior knowledge such as entry points and exploit paths. ([arXiv][2])
4. CTF setups reduce the complexity of real penetration testing environments. ([arXiv][1])
5. CTF-based evaluations therefore overestimate real-world performance of pentesting agents. ([arXiv][3])
6. Real-world pentesting requires autonomous reconnaissance and uncertainty handling. ([arXiv][2])
7. Real-world pentesting requires distinguishing benign services from exploitable ones. ([arXiv][1])
8. Achieving a system shell requires integrating multiple tools and reasoning steps. ([arXiv][2])

### Claims about evaluation findings

9. Existing pentesting agents **can hardly obtain system shells** under realistic conditions. ([arXiv][1])
10. Agents fail because they become lost in large amounts of exploratory information. ([arXiv][2])
11. Agents fail because they lack ready-to-use exploit capabilities. ([arXiv][2])

### Contributions claimed

12. The paper introduces **TermiBench**, a real-world pentesting benchmark. ([arXiv][1])
13. TermiBench is the **first real-world, agent-oriented pentesting benchmark**. ([arXiv][2])
14. TermiBench changes the goal from **flag finding to obtaining a system shell**. ([arXiv][1])
15. The benchmark requires autonomous reconnaissance without prior information. ([arXiv][2])
16. The paper proposes **TermiAgent**, a multi-agent penetration testing framework. ([arXiv][1])
17. TermiAgent addresses long-context forgetting via **Located Memory Activation (LMA)**. ([arXiv][1])
18. TermiAgent constructs an exploit arsenal using **structured code understanding rather than naive retrieval**. ([arXiv][1])
19. TermiAgent can run on **laptop-scale deployments**. ([arXiv][1])

---

# Benchmark Components (TermiBench)

### Dataset composition

20. TermiBench contains **510 hosts**. ([遇见数据集][4])
21. Hosts cover **25 software services**. ([遇见数据集][4])
22. The benchmark includes **30 CVEs**. ([遇见数据集][4])
23. Vulnerabilities span **2015–2025**. ([遇见数据集][4])

### Host configuration

24. Each host contains **one vulnerable service**. ([遇见数据集][4])
25. Each host may contain **up to seven benign services**. ([遇见数据集][4])

### Benchmark tiers

26. Tier 0: 0 benign services, 1 vulnerable service, 30 hosts. ([arXiv][3])
27. Tier 1: 1 benign service, 1 vulnerable service, 120 hosts. ([arXiv][3])
28. Tier 2: 3 benign services, 1 vulnerable service, 120 hosts. ([arXiv][3])
29. Tier 3: 5 benign services, 1 vulnerable service, 120 hosts. ([arXiv][3])
30. Tier 4: 7 benign services, 1 vulnerable service, 120 hosts. ([arXiv][3])

### Task requirements

31. Agents must perform reconnaissance to discover services. ([arXiv][1])
32. Agents must identify exploitable services among benign ones. ([arXiv][1])
33. Agents must perform vulnerability exploitation. ([arXiv][1])
34. The final objective is **obtaining an interactive system shell**. ([arXiv][1])

---

# Method Components (TermiAgent)

### Overall architecture

35. TermiAgent is a **multi-agent penetration testing system**. ([arXiv][1])
36. It follows a **perception–action loop** for pentesting tasks. ([arXiv][3])
37. The system decomposes pentesting into multi-step subtasks. ([arXiv][3])

### Core modules

38. Memory Module. ([arXiv][3])
39. Arsenal Module. ([arXiv][3])

### Memory Module

40. Uses **Located Memory Activation (LMA)**. ([arXiv][3])
41. LMA activates relevant memory segments during decision making. ([arXiv][2])
42. LMA mitigates long-context forgetting. ([arXiv][1])
43. LMA dynamically activates memories related to the current target component. ([arXiv][3])

### Arsenal Module

44. Collects in-the-wild exploit code. ([arXiv][2])
45. Uses **Unified Exploit Descriptor (UED)**. ([arXiv][3])
46. UED standardizes heterogeneous exploit implementations. ([arXiv][3])
47. Exploits are packaged into reproducible modules. ([arXiv][3])

---

# Exploit Dataset and Processing

48. Exploits are gathered from GitHub repositories. ([arXiv][3])
49. 231 repositories corresponding to the 30 CVEs were analyzed. ([arXiv][3])

### Exploit type distribution

50. Packet-based exploits: 123. ([arXiv][3])

51. Packet-based exploit proportion: 5.97%. ([arXiv][3])

52. Packet-based exploit success rate: 94.31%. ([arXiv][3])

53. Packet-based exploit average runtime: 41.28 seconds. ([arXiv][3])

54. Script-based exploits: 1825. ([arXiv][3])

55. Script-based exploit proportion: 88.55%. ([arXiv][3])

56. Script-based exploit success rate: 63.51%. ([arXiv][3])

57. Script-based exploit average runtime: 83.76 seconds. ([arXiv][3])

---

# Experimental Setup

### Models used

58. GPT-5. ([arXiv][3])
59. DeepSeek-V3-0324. ([arXiv][3])

### Example cost parameters

60. GPT-5 input cost: $1.25 per 1M tokens. ([arXiv][3])
61. GPT-5 output cost: $10 per 1M tokens. ([arXiv][3])
62. DeepSeek-V3 input cost: 2 RMB per 1M tokens. ([arXiv][3])
63. DeepSeek-V3 output cost: 8 RMB per 1M tokens. ([arXiv][3])

---

# Experimental Results

### Performance comparison

64. TermiAgent solves **~1.7× more CTF challenges** than previous agents. ([arXiv][3])
65. TermiAgent solves **>8× more real-world pentesting tasks** than previous agents. ([arXiv][3])

### Efficiency

66. TermiAgent requires **<1/5 the execution time** of prior agents. ([arXiv][3])
67. TermiAgent requires **~1/10 the financial cost** of prior agents. ([arXiv][3])

### Exploit coverage

68. TermiAgent’s exploit arsenal covers **1.8× more RCE CVEs than Metasploit**. ([arXiv][3])

### Failure analysis

69. Many failures occur on hosts with **8 services**. ([arXiv][3])
70. This indicates multi-service environments significantly increase complexity. ([arXiv][3])
71. Located Memory Activation improves performance in these complex scenarios. ([arXiv][3])

---

# Practical Deployment Claims

72. TermiAgent can run on **laptop-scale hardware**. ([arXiv][1])
73. Experiments were conducted in **isolated environments**. ([arXiv][2])
74. Only **publicly disclosed CVEs** were exploited. ([arXiv][2])
75. The system does **not generate new exploits**; it packages existing ones. ([arXiv][2])

---

If you want, I can also produce a **“research distillation” version (≈150–200 words)** that extracts only the **core novelty and contributions**, which is useful when building literature reviews or benchmarking tables for **LLM pentesting agents**—something directly relevant to your work studying autonomous security agents.

[1]: https://arxiv.org/abs/2509.09207?utm_source=chatgpt.com "Shell or Nothing: Real-World Benchmarks and Memory-Activated Agents for Automated Penetration Testing"
[2]: https://arxiv.org/html/2509.09207v1?utm_source=chatgpt.com "Real-World Benchmarks and Memory-Activated Agents for ..."
[3]: https://arxiv.org/pdf/2509.09207?utm_source=chatgpt.com "Shell or Nothing: Real-World Benchmarks and Memory- ..."
[4]: https://www.selectdataset.com/dataset/7f8f87f49985a836a25c6c116e3838d5?utm_source=chatgpt.com "TermiBench|渗透测试数据集|信息安全数据集"
