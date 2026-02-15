# UNIFIED AI HEALTH PLATFORM - ARCHITECTURE DIAGRAMS

This document contains Mermaid diagrams for the Unified AI Health Intelligence Platform architecture.

---

## 1. HIGH-LEVEL SYSTEM ARCHITECTURE

```mermaid
graph TB
    subgraph "User Layer"
        CLI[Clinicians]
        ADM[Administrators]
        RES[Researchers]
        PUB[Public Health Officials]
        PAT[Patients]
    end
    
    subgraph "Interface Layer"
        UI1[Clinical Dashboard]
        UI2[Operations Dashboard]
        UI3[Research Portal]
        UI4[Public Health Console]
        UI5[Patient Portal]
    end
    
    subgraph "AI Agent Layer"
        CC[Clinical Copilot]
        OB[Operations Brain]
        RB[Research Brain]
        TI[Trial Intelligence]
        MH[Mental Health AI]
        PH[Public Health AI]
    end
    
    subgraph "Medical Knowledge & Reasoning Core"
        LLM[Medical LLM<br/>GPT-4 / Llama 3]
        RAG[RAG Engine]
        VDB[(Vector Database<br/>Pinecone/Weaviate)]
        CONF[Confidence Scorer]
        EMB[Embedding Model<br/>PubMedBERT]
    end
    
    subgraph "Trust & Compliance Infrastructure"
        EXP[Explainability Engine]
        AUDIT[Audit Logger]
        BIAS[Bias Monitor]
        FED[Federated Learning]
        SEC[Security & Access Control]
    end
    
    subgraph "Data Sources"
        EHR[(EHR Systems<br/>Epic/Cerner)]
        LIT[(PubMed<br/>35M+ Articles)]
        DRUG[(Drug Databases<br/>RxNorm/DrugBank)]
        GUIDE[(Clinical Guidelines<br/>AHA/ADA/NCCN)]
        IMG[(Imaging Data<br/>DICOM)]
        GEN[(Genomic Data<br/>ClinVar)]
    end
    
    CLI --> UI1
    ADM --> UI2
    RES --> UI3
    PUB --> UI4
    PAT --> UI5
    
    UI1 --> CC
    UI2 --> OB
    UI3 --> RB
    UI3 --> TI
    UI5 --> MH
    UI4 --> PH
    
    CC --> LLM
    OB --> LLM
    RB --> LLM
    TI --> LLM
    MH --> LLM
    PH --> LLM
    
    LLM --> RAG
    RAG --> EMB
    EMB --> VDB
    LLM --> CONF
    
    LLM --> EXP
    LLM --> AUDIT
    LLM --> BIAS
    LLM --> SEC
    
    VDB --> LIT
    VDB --> DRUG
    VDB --> GUIDE
    VDB --> IMG
    VDB --> GEN
    
    FED -.->|Model Updates| LLM
    EHR -.->|Privacy-Preserved| FED
    
    style LLM fill:#4A90E2,stroke:#2E5C8A,stroke-width:3px,color:#fff
    style RAG fill:#4A90E2,stroke:#2E5C8A,stroke-width:2px,color:#fff
    style VDB fill:#50C878,stroke:#2E7D4E,stroke-width:2px,color:#fff
    style FED fill:#E94B3C,stroke:#A33327,stroke-width:2px,color:#fff
```

---

## 2. RAG PIPELINE DETAILED FLOW

```mermaid
graph LR
    A[User Query] --> B[Query Processing]
    B --> C[Entity Extraction]
    C --> D[Generate Embeddings]
    D --> E[Vector Search<br/>Top-K=10]
    E --> F[Cross-Encoder<br/>Reranking]
    F --> G[Context Assembly<br/>Top-5]
    G --> H[LLM Generation<br/>with Citations]
    H --> I[Confidence Scoring]
    I --> J[Explanation<br/>Generation]
    J --> K[Audit Logging]
    K --> L[Response to User]
    
    style A fill:#E8F4F8
    style L fill:#C8E6C9
    style H fill:#4A90E2,color:#fff
    style I fill:#FFA726,color:#fff
    style J fill:#AB47BC,color:#fff
```

---

## 3. CLINICAL COPILOT DATA FLOW

```mermaid
sequenceDiagram
    participant C as Clinician
    participant UI as Clinical Dashboard
    participant CC as Clinical Copilot
    participant MKC as Medical Knowledge Core
    participant VDB as Vector Database
    participant LLM as Medical LLM
    participant EXP as Explainability Engine
    participant AUDIT as Audit Logger
    
    C->>UI: Enter patient symptoms
    UI->>CC: Submit diagnosis request
    CC->>MKC: Query with patient context
    MKC->>VDB: Retrieve relevant evidence
    VDB-->>MKC: Top-K documents
    MKC->>LLM: Generate diagnosis with context
    LLM-->>MKC: Differential diagnosis
    MKC->>MKC: Calculate confidence score
    MKC->>EXP: Generate explanation
    EXP-->>MKC: Reasoning steps + evidence
    MKC->>AUDIT: Log decision
    MKC-->>CC: Complete response
    CC-->>UI: Display results
    UI-->>C: Show diagnosis + explanation
    
    Note over C,AUDIT: Total time: <2 seconds
```

---

## 4. FEDERATED LEARNING ARCHITECTURE

```mermaid
graph TB
    subgraph "Institution A"
        DA[(Local Data)]
        MA[Local Model]
        TA[Training Process]
        DA --> TA
        TA --> MA
    end
    
    subgraph "Institution B"
        DB[(Local Data)]
        MB[Local Model]
        TB[Training Process]
        DB --> TB
        TB --> MB
    end
    
    subgraph "Institution C"
        DC[(Local Data)]
        MC[Local Model]
        TC[Training Process]
        DC --> TC
        TC --> MC
    end
    
    subgraph "Central Aggregator"
        AGG[Secure Aggregator]
        DP[Differential Privacy<br/>ε=1.0]
        POISON[Poisoning Detector]
        GLOBAL[Global Model]
        
        AGG --> DP
        DP --> POISON
        POISON --> GLOBAL
    end
    
    MA -->|Encrypted Gradients| AGG
    MB -->|Encrypted Gradients| AGG
    MC -->|Encrypted Gradients| AGG
    
    GLOBAL -.->|Updated Model| MA
    GLOBAL -.->|Updated Model| MB
    GLOBAL -.->|Updated Model| MC
    
    style DA fill:#E8F4F8
    style DB fill:#E8F4F8
    style DC fill:#E8F4F8
    style AGG fill:#E94B3C,color:#fff
    style DP fill:#FFA726,color:#fff
    style GLOBAL fill:#4A90E2,color:#fff
    
    note1[Raw data never<br/>leaves institution]
    note2[Privacy-preserving<br/>aggregation]
    
    DA -.-> note1
    AGG -.-> note2
```

---

## 5. MULTI-AGENT ECOSYSTEM

```mermaid
graph TB
    subgraph "Shared Intelligence Core"
        CORE[Medical Knowledge<br/>& Reasoning Core]
    end
    
    subgraph "Specialized Agents"
        CC[Clinical Copilot<br/>Diagnosis & Treatment]
        OB[Operations Brain<br/>Resource Optimization]
        RB[Research Brain<br/>Drug Discovery]
        TI[Trial Intelligence<br/>Patient Matching]
        MH[Mental Health AI<br/>Risk Assessment]
        PH[Public Health AI<br/>Outbreak Prediction]
    end
    
    subgraph "Use Cases"
        UC1[Emergency Dept<br/>Chest Pain]
        UC2[Hospital Bed<br/>Management]
        UC3[Literature<br/>Synthesis]
        UC4[Clinical Trial<br/>Recruitment]
        UC5[Crisis<br/>Detection]
        UC6[Disease<br/>Surveillance]
    end
    
    CORE --> CC
    CORE --> OB
    CORE --> RB
    CORE --> TI
    CORE --> MH
    CORE --> PH
    
    CC --> UC1
    OB --> UC2
    RB --> UC3
    TI --> UC4
    MH --> UC5
    PH --> UC6
    
    UC1 -.->|Learning| CORE
    UC2 -.->|Learning| CORE
    UC3 -.->|Learning| CORE
    UC4 -.->|Learning| CORE
    UC5 -.->|Learning| CORE
    UC6 -.->|Learning| CORE
    
    style CORE fill:#4A90E2,stroke:#2E5C8A,stroke-width:4px,color:#fff
    style CC fill:#50C878,color:#fff
    style OB fill:#50C878,color:#fff
    style RB fill:#50C878,color:#fff
    style TI fill:#50C878,color:#fff
    style MH fill:#50C878,color:#fff
    style PH fill:#50C878,color:#fff
```

---

## 6. EXPLAINABILITY ENGINE ARCHITECTURE

```mermaid
graph TB
    A[AI Decision] --> B[Explainability Engine]
    
    B --> C[Chain-of-Thought<br/>Extraction]
    B --> D[Attention<br/>Visualization]
    B --> E[SHAP Values<br/>Feature Importance]
    B --> F[Evidence<br/>Mapping]
    B --> G[Counterfactual<br/>Generation]
    
    C --> H[Reasoning Steps]
    D --> I[Influential Inputs]
    E --> J[Feature Rankings]
    F --> K[Source Citations]
    G --> L[Alternative Scenarios]
    
    H --> M[Natural Language<br/>Summary]
    I --> M
    J --> M
    K --> M
    L --> M
    
    M --> N[Human-Readable<br/>Explanation]
    
    style B fill:#AB47BC,color:#fff
    style M fill:#FFA726,color:#fff
    style N fill:#C8E6C9
```

---

## 7. BIAS MONITORING SYSTEM

```mermaid
graph LR
    subgraph "Data Collection"
        A[AI Decisions]
        B[Patient Demographics]
        C[Outcomes]
    end
    
    subgraph "Analysis Engine"
        D[Demographic<br/>Stratification]
        E[Metric Calculation]
        F[Disparate Impact<br/>Detection]
    end
    
    subgraph "Metrics"
        G[Accuracy by Race]
        H[Accuracy by Gender]
        I[Accuracy by Age]
        J[Accuracy by SES]
        K[FP/FN Rates]
        L[Confidence Distributions]
    end
    
    subgraph "Mitigation"
        M[Bias Alert]
        N[Reweighting]
        O[Adversarial Debiasing]
        P[Fairness Constraints]
    end
    
    A --> D
    B --> D
    C --> D
    
    D --> E
    E --> F
    
    F --> G
    F --> H
    F --> I
    F --> J
    F --> K
    F --> L
    
    G --> M
    H --> M
    I --> M
    J --> M
    K --> M
    L --> M
    
    M --> N
    M --> O
    M --> P
    
    style M fill:#E94B3C,color:#fff
    style F fill:#FFA726,color:#fff
```

---

## 8. MVP TECHNICAL STACK

```mermaid
graph TB
    subgraph "Frontend"
        REACT[React 18 + TypeScript]
        TAIL[Tailwind CSS]
        CHART[Recharts]
        QUERY[React Query]
    end
    
    subgraph "Backend"
        FAST[FastAPI]
        PYD[Pydantic]
        OPENAI[OpenAI SDK]
        PINE[Pinecone Client]
    end
    
    subgraph "External APIs"
        GPT[OpenAI GPT-4]
        EMB[OpenAI Embeddings]
        VEC[Pinecone Vector DB]
        PUB[PubMed API]
        RX[RxNorm API]
    end
    
    subgraph "Infrastructure"
        DOCK[Docker Compose]
        CLOUD[AWS/GCP/Azure]
        GIT[GitHub]
    end
    
    REACT --> FAST
    TAIL --> REACT
    CHART --> REACT
    QUERY --> REACT
    
    FAST --> OPENAI
    FAST --> PINE
    PYD --> FAST
    
    OPENAI --> GPT
    OPENAI --> EMB
    PINE --> VEC
    FAST --> PUB
    FAST --> RX
    
    FAST --> DOCK
    DOCK --> CLOUD
    FAST --> GIT
    
    style FAST fill:#4A90E2,color:#fff
    style GPT fill:#50C878,color:#fff
    style VEC fill:#50C878,color:#fff
```

---

## 9. SECURITY & COMPLIANCE LAYERS

```mermaid
graph TB
    subgraph "Application Layer"
        APP[AI Agents]
    end
    
    subgraph "Security Controls"
        AUTH[Authentication<br/>OAuth 2.0 + MFA]
        AUTHZ[Authorization<br/>RBAC]
        ENCRYPT[Encryption<br/>AES-256 at rest<br/>TLS 1.3 in transit]
    end
    
    subgraph "Compliance"
        HIPAA[HIPAA<br/>Audit Logs<br/>Access Controls]
        GDPR[GDPR<br/>Right to Deletion<br/>Data Portability]
        GXP[GxP<br/>Validation Docs<br/>Change Control]
        FDA[FDA SaMD<br/>Clinical Validation<br/>Post-Market Surveillance]
    end
    
    subgraph "Monitoring"
        AUDIT[Audit Logging]
        ALERT[Security Alerts]
        VULN[Vulnerability Scanning]
    end
    
    APP --> AUTH
    AUTH --> AUTHZ
    AUTHZ --> ENCRYPT
    
    ENCRYPT --> HIPAA
    ENCRYPT --> GDPR
    ENCRYPT --> GXP
    ENCRYPT --> FDA
    
    HIPAA --> AUDIT
    GDPR --> AUDIT
    GXP --> AUDIT
    FDA --> AUDIT
    
    AUDIT --> ALERT
    AUDIT --> VULN
    
    style ENCRYPT fill:#E94B3C,color:#fff
    style AUDIT fill:#FFA726,color:#fff
```

---

## 10. DEPLOYMENT ARCHITECTURE (MVP)

```mermaid
graph TB
    subgraph "Client"
        BROWSER[Web Browser]
    end
    
    subgraph "Load Balancer"
        LB[AWS ALB / GCP LB]
    end
    
    subgraph "Application Tier"
        API1[FastAPI Instance 1]
        API2[FastAPI Instance 2]
        API3[FastAPI Instance 3]
    end
    
    subgraph "External Services"
        OPENAI[OpenAI API]
        PINECONE[Pinecone]
        PUBMED[PubMed API]
    end
    
    subgraph "Monitoring"
        LOGS[CloudWatch / Stackdriver]
        METRICS[Prometheus]
    end
    
    BROWSER --> LB
    LB --> API1
    LB --> API2
    LB --> API3
    
    API1 --> OPENAI
    API1 --> PINECONE
    API1 --> PUBMED
    
    API2 --> OPENAI
    API2 --> PINECONE
    API2 --> PUBMED
    
    API3 --> OPENAI
    API3 --> PINECONE
    API3 --> PUBMED
    
    API1 --> LOGS
    API2 --> LOGS
    API3 --> LOGS
    
    API1 --> METRICS
    API2 --> METRICS
    API3 --> METRICS
    
    style LB fill:#4A90E2,color:#fff
    style OPENAI fill:#50C878,color:#fff
    style PINECONE fill:#50C878,color:#fff
```

---

## NOTES

These diagrams can be rendered using:
- Mermaid Live Editor: https://mermaid.live
- GitHub (native Mermaid support in markdown)
- VS Code with Mermaid extension
- Documentation tools (GitBook, Docusaurus, etc.)

For the hackathon presentation, consider:
1. Animating the RAG pipeline flow
2. Highlighting the unified core in the multi-agent diagram
3. Emphasizing privacy in the federated learning diagram
4. Using these in pitch deck slides

