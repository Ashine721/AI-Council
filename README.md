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

## 🔗 Resources & Access
## 📊 Datasets
* [/CIC-IDS2017](放入你的連結)
* [Thursday-WorkingHours-Morning-WebAttacks.pcap_ISCX.csv](放入你的連結)
## 📚 References
* Du et al., 2023 — *Improving Factuality and Reasoning in Language Models through Multiagent Debate*, **arXiv**: 2305.14325, Published at **ICML 2024**.
*   **Troubleshooting:** If unable to open any files in this repository, please access them directly via this [Alternative Drive Link](https://drive.google.com/drive/folders/1e1BX_kCJ8y1IGcTYbvcREbmsDA1eY0Gt?usp=drive_link).
