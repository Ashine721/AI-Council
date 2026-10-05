# AI Council: Multi-Agent Cybersecurity Threat Assessment

## Abstract
This project explores the implementation and performance of an "AI Council"—a multi-agent system designed for cybersecurity threat analysis. Built on the `Llama-3.1-8B-Chinese-Chat` base model and utilizing the `CIC-IDS2017` dataset, the system simulates a diverse intelligence council by intentionally segmenting the information provided to different agent roles.

## Agent Roles & Architecture
To ensure independent reasoning paths, the pipeline assigns distinct input perspectives and responsibilities to three specialized agents, ultimately culminating in a final decision-maker:

*   **Analyst Agent:** 
    Receives raw network traffic behavioral features (e.g., TCP flag statistics, flow counts, and ports). Its primary responsibility is objective observation—describing exactly *"what happened"* during the event.
*   **Hunter Agent:** 
    Analyzes high-level traffic pattern features (e.g., packet length statistics and window size) and leverages Retrieval-Augmented Generation (RAG) to query MITRE ATT&CK threat intelligence. Its role is to formulate actionable *attack hypotheses*.
*   **Auditor Agent:** 
    Does not access raw data directly. Instead, it receives the deductive outputs from both the Analyst and the Hunter during pipeline execution. It acts as a critical reviewer, identifying logical flaws or uncertain assumptions, and outputs a calibrated *confidence score*.
*   **Judge Agent:** 
    Synthesizes the findings and critiques from the three preceding agents to deliver the *final threat classification* and actionable *response recommendations*.

## Core Contribution
The core innovation of this system lies in its **Information Segmentation Design**. By restricting and tailoring the input data for each role, the agents are forced into divergent reasoning paths. This guarantees that even when sharing the identical base model, the system generates a genuine multi-perspective analysis—effectively overcoming the limitations of single-LLM approaches.

## File Descriptions & Notes
*   **`week14_report`**: Corresponds to the code in `week_14.ipynb`.
*   **Week 15 Note**: The progress for Week 15 was primarily executed and completed on LLaMA Factory. As the source code was not downloaded, there is no corresponding code file provided for this week.
*   **`final_report`**: Also corresponds to the code in `week_14.ipynb`.

## Evaluation Prompts
| 測試項目 | 測試語句 (Test sentence) |
| :--- | :--- |
| 正常流量測試 測試 1 — BENIGN | Analyze the following network traffic and classify it: Flow Duration: 119261000, Total Fwd Packets: 20, Total Backward Packets: 18, Flow Bytes/s: 1024.5, Flow Packets/s: 45.2, SYN Flag Count: 1, ACK Flag Count: 35 |
| 攻擊流量測試 測試 2 — DDoS | Analyze the following network traffic and classify it: Flow Duration: 2341, Total Fwd Packets: 1500, Total Backward Packets: 0, Flow Bytes/s: 985432.1, Flow Packets/s: 6408.4, SYN Flag Count: 1500, ACK Flag Count: 0 |
| 測試 3 — PortScan | Analyze the following network traffic and classify it: Flow Duration: 51000, Total Fwd Packets: 1, Total Backward Packets: 0, Flow Bytes/s: 78.4, Flow Packets/s: 19.6, SYN Flag Count: 1, RST Flag Count: 1, Destination Port: 445 |
| 測試 4 — Brute Force (FTP) | Analyze the following network traffic and classify it: Flow Duration: 302000, Total Fwd Packets: 8, Total Backward Packets: 6, Flow Bytes/s: 231.5, Flow Packets/s: 12.3, SYN Flag Count: 1, ACK Flag Count: 13, Destination Port: 21 |
| 測試 5 — Bot | Analyze the following network traffic and classify it: Flow Duration: 7200000000, Total Fwd Packets: 3, Total Backward Packets: 2, Flow Bytes/s: 0.8, Flow Packets/s: 0.0007, SYN Flag Count: 1, ACK Flag Count: 4, Destination Port: 6667 |

## Results

| 測試 | 正確標籤 | 模型預測 | 結果 |
| :--- | :--- | :--- | :--- |
| 測試 1 | BENIGN | BENIGN | ✅ 完全正確 |
| 測試 2 | DDoS | BENIGN | ❌ 完全錯誤 |
| 測試 3 | PortScan | Web Attack ◆ Sql Injection | ❌ 大方向錯誤 |
| 測試 4 | Brute Force (FTP) | Web Attack ◆ XSS | ❌ 大方向錯誤 |
| 測試 5 | Bot | BENIGN | ❌ 完全錯誤 |

## Future Work

Due to the limited scale of the data in this experiment, the hyperparameters during the fine-tuning process were not systematically verified and optimized. Future work plans to expand the size of the training dataset to investigate the correlation between different fine-tuning parameter settings and the capabilities of the AI Council. Concurrently, we will dedicate efforts to introducing or establishing a standardized and objective evaluation benchmark to ensure the rigor of the experimental results.

## 🔗 Resources & Access
## 📊 Datasets
* [/CIC-IDS2017](放入你的連結)
* [Thursday-WorkingHours-Morning-WebAttacks.pcap_ISCX.csv](放入你的連結)
## 📚 References
* Du et al., 2023 — *Improving Factuality and Reasoning in Language Models through Multiagent Debate*, **arXiv**: 2305.14325, Published at **ICML 2024**.
*   **Troubleshooting:** If unable to open any files in this repository, please access them directly via this [Alternative Drive Link](https://drive.google.com/drive/folders/1e1BX_kCJ8y1IGcTYbvcREbmsDA1eY0Gt?usp=drive_link).
