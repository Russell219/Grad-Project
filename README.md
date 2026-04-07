# Arabic MUSER: Fake News Detection System

This project implements a multi-step retrieval system (MUSER) optimized for the Arabic language. It uses **AraBERT** for embeddings and **FAISS** for efficient vector searching.

## System Architecture

```mermaid
graph TD
    %% Define Styles
    classDef arabic fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef logic fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef phase fill:#fcfcfc,stroke:#333,stroke-dasharray: 5 5

    subgraph Phase1 [PHASE 1: KNOWLEDGE BASE BUILD]
        A[(Arabic Data)] --> B[Pre-processing<br/>Normalization]:::arabic
        B --> C[AraBERT Model]:::arabic
        C --> D[(FAISS Index)]
    end

    subgraph Phase2 [PHASE 2: MUSER RETRIEVAL LOOP]
        E([User Claim]) --> F[Initial Query]
        
        subgraph Loop [Iterative Reasoning]
            G{Vector Search}:::logic
            H[Ranking &<br/>Lambda Check]:::logic
            I[Query Reformulation<br/>C + SEP + Snippet]:::logic
            
            G --> H
            H -- "Below Threshold" --> I
            I --> G
        end
        
        F --> G
        H -- "Sufficient" --> J[Evidence Integration]
    end

    subgraph Phase3 [PHASE 3: VERDICT]
        J --> K[NLI Verification]:::logic
        K --> L[/Final Verdict: TRUE or FALSE/]
    end

    class Phase1,Phase2,Phase3 phase
```

## Tech Stack
* **Language:** Python
* **Embeddings:** AraBERT (HuggingFace)
* **Vector Store:** FAISS
* **Framework:** LangChain
