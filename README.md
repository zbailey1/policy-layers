# policy-layers
Layering of different liability policy structures 

```mermaid
flowchart TD

    %% ===== Ground-Up Loss Stack =====
    L[Loss Occurs<br/>(Ground-Up)] --> R[Deductible or SIR]

    R -->|After Retention| P[Primary GL Policy<br/>Per-Occurrence Limit]
    P -->|If Exhausted| E[Excess / Umbrella Policy]

    %% ===== Deductible vs SIR Notes =====
    R --- D1[Deductible:<br/>Insurer pays first<br/>Insured reimburses]
    R --- D2[SIR:<br/>Insured pays first<br/>Insurer attaches after]

    %% ===== Aggregate Deductible Accumulation =====
    AD1[Claim 1<br/>Deductible Paid] --> AD2[Claim 2<br/>Deductible Paid]
    AD2 --> AD3[Claim 3<br/>Deductible Paid]
    AD3 --> AD4[Claim 4<br/>Deductible Paid]

    AD4 --> ADCAP[Aggregate Deductible Reached]

    ADCAP --> ADSTOP[Future Claims<br/>No Deductible Applies]

    %% ===== Aggregate Limit Erosion =====
    O1[Occurrence 1<br/>Erodes Aggregate] --> O2[Occurrence 2<br/>Erodes Aggregate]
    O2 --> O3[Occurrence 3<br/>Erodes Aggregate]

    O3 --> AGGEX[General Aggregate Exhausted]

    AGGEX --> NOCOV[No Further Primary GL Coverage]

    %% ===== Logical Grouping =====
    subgraph Retention
        L
        R
    end

    subgraph Primary_Coverage
        P
        O1
        O2
        O3
    end

    subgraph Aggregates
        AD1
        AD2
        AD3
        AD4
        ADCAP
        ADSTOP
        AGGEX
    end

    subgraph Excess
     
        E
    end
```
