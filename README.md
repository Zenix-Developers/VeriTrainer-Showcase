<div align="center">

<img src="assets/banner.svg" alt="VeriTrainer" width="100%">

<br>

![Verified learning](https://img.shields.io/badge/Verified_learning-00b14f?style=for-the-badge)
![Real tests](https://img.shields.io/badge/Real_tests-16a34a?style=for-the-badge)
![Honest exams](https://img.shields.io/badge/Honest_exams-22c55e?style=for-the-badge)
![Local first](https://img.shields.io/badge/Local_first-15803d?style=for-the-badge)

*A model training engine where the model practises, real tests check every answer, and only proven work is ever trained on.*

</div>

---

> **A showcase repository.** It contains no source code, only a tour of what VeriTrainer is and the experience it creates.
>
> 🔑 **VeriTrainer is in private early access.** It brings together proven ideas from published research into one effortless, end-to-end engine, so you do not have to assemble the pieces yourself.

## The idea

Most training pipelines learn from whatever data they are handed. VeriTrainer learns from what a model can actually **prove**. The model practises on real tasks, real tests grade every answer, a teacher gives gentle hints when it stumbles, and only answers that pass (and pass again without the hint) become training material. Every round ends with a fair, leak-checked exam, so progress is measured rather than assumed.

## The learning loop

```mermaid
flowchart LR
    A([Real tasks]) --> B[Model attempts once]
    B --> C{Real tests pass?}
    C -- Yes --> G[Verified answer]
    C -- No --> D[Teacher offers a hint, H1 to H5]
    D --> E[Model solves again without the hint]
    E --> F{Tests pass?}
    F -- Yes --> G
    F -- No --> H[Not used for training]
    G --> I[Train on proven work only]
    I --> J[Fair held-out exam]
    J --> K([A stronger model])
    style A fill:#00b14f,color:#fff,stroke:none
    style G fill:#16a34a,color:#fff,stroke:none
    style K fill:#15803d,color:#fff,stroke:none
```

Hints are gentle and never give the answer away: they get more specific one level at a time, and they are only ever shown while practising, never baked into what the model learns.

## Highlights

| | Feature | What it feels like |
|---|---|---|
| ✅ | **Learns only from proof** | Real tests grade every answer before it can teach anything |
| 🪜 | **Escalating hint ladder** | Five levels of hints from a nudge to a strong pointer, each checked so it never leaks the solution |
| 🔁 | **Hint-free re-solve** | A hint only counts if the model can then succeed on its own |
| 🧪 | **Fair, paired exams** | Every round is scored on a held-out set, compared against the previous best, and leak-checked |
| 🎯 | **Honesty tracking** | Measures whether a model's confidence matches its results |
| 🛡️ | **Dataset audit** | Friendly flags catch problems before a run starts: empty training masks, template mismatches, duplicate-heavy data, possible leaks between training and exam, truncation, sensitive data |
| 📦 | **Frozen manifests** | Every dataset version is fingerprinted, so any result can be traced back to exactly what it learned from |
| 🧰 | **Pluggable verifiers** | Code graders and test runners plug in behind one simple interface |
| 🔌 | **Bring your own models** | Student, teacher and judge roles are each swappable for any compatible endpoint |
| 🧑‍✈️ | **An LLM operator** | An assistant reads the reports and proposes the next round, while clear rules keep the decisions safe |
| 🌐 | **Spread across machines** | Practice runs shard across remote GPUs, so work finishes sooner |
| 🏁 | **Eval-gated promotion** | A new model is promoted only if it beats the last one on the exam |
| 🗂️ | **Adapter registry** | Every trained adapter is stored with its lineage, dataset version and exam report |

## Two kinds of datasets

```mermaid
flowchart TB
    T[Task datasets<br>problem plus verifier] --> P[Practise, verify, train on passes]
    D[Demonstration datasets<br>finished conversations] --> S[Standard fine-tuning<br>with the same audit and exam]
    P --> R[(Adapter registry)]
    S --> R
    style T fill:#00b14f,color:#fff,stroke:none
    style D fill:#16a34a,color:#fff,stroke:none
    style R fill:#15803d,color:#fff,stroke:none
```

## Early results

On a held-out set of 231 coding problems, an 8B-class open model improved markedly after a single verified round:

| Model | First try | After self-repair |
|---|---|---|
| Base | 21.6% | 25.5% |
| **After one verified round** | **35.5%** | **44.2%** |

That is a statistically significant gain on a leak-checked exam, from only 582 verified training rows. The next round adds the hint ladder and honesty training.

## The control room

A local web app gives training a calm, ride-tracker feel: service tiles on the home screen, a live tracker for each run, a receipt for every exam, side-by-side model comparison, a flags page, model and endpoint management, and dataset upload with an instant audit.

```mermaid
flowchart LR
    H[Home tiles] --> R[Run tracker]
    R --> X[Exam receipt]
    X --> C[Compare models]
    H --> F[Flags]
    H --> M[Models and endpoints]
    H --> U[Upload and audit]
    style H fill:#00b14f,color:#fff,stroke:none
```

## The shape of the engine

```mermaid
flowchart LR
    I[Ingest] --> A[Audit] --> Z[Freeze manifest] --> Q[Job queue]
    Q --> W[Remote workers<br>practise and verify]
    W --> L[(Event log)]
    L --> O[Operator LLM<br>advisory]
    L --> T[Trainer]
    T --> E[Exam gate]
    E --> G[(Adapter registry)]
    style I fill:#00b14f,color:#fff,stroke:none
    style G fill:#15803d,color:#fff,stroke:none
```

---

<div align="center">

**VeriTrainer** · crafted by [Zenix Developers](https://github.com/Zenix-Developers)

*The source code is private. Interested in a closer look? Get in touch.*

</div>
