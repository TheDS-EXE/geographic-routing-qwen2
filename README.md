# Circuit Localization in a Tiny Language Model: Geographic Routing in Qwen2-0.5B

This repository contains the code, experiments, and final report for the research project:  
**"Circuit Localization in a Tiny Language Model: Geographic Routing and Representational Depth in Qwen2-0.5B"**  
by **Abdelrahman Elamarawy**.

The project utilizes mechanistic interpretability techniques—specifically activation patching, ablation, and path patching via the `TransformerLens` library—to investigate how small-scale LLMs (Qwen2-0.5B) store, route, and recall geographic associations.

## Repository Structure

The repository is divided into two main directories: **`core_experiments`** (containing the main research methodology and results) and **`diagnostics`** (containing exploratory/validation notebooks not used in the final paper).

```text
├── core_experiments/
│   ├── Experiment1.ipynb           # Multi-trigger convergence (Economic, Landmark, Cultural)
│   ├── Experiment2.ipynb           # Geographic Bias Audit (Western vs MENA routing depths)
│   ├── Experiment3.ipynb           # Causal Ablation (Layer-wise damage measurement)
│   ├── PathPatching.ipynb          # Head-level causal attribution and damage matrix
│   ├── Control.ipynb               # Syntactic control tasks verifying Layer 17's specific role
│   ├── induction_head_test.ipynb   # Attention head circuit visualizations
│
└── diagnostics/
    ├── activation_patching_nutrition.ipynb   # Diagnostic patching for a simple "Nutrition" circuit
    └── activation_patching_sentiment.ipynb   # Diagnostic patching for a simple "Sentiment" circuit
```

## Core Experiments

The `core_experiments` folder houses the notebooks that produced the quantitative data and visualizations reported in the paper:

- **`Experiment1.ipynb`** – Investigates multi‑trigger convergence. Tests whether different cues (e.g., economic currencies, landmarks, cultural items) utilize the same internal circuitry to route to a target geographic location. Highlights Layer 17 as a critical hub.

- **`Experiment2.ipynb`** – An audit of geographic bias. Compares the representational depth and recovery curves between Western associations (e.g., Euro → Europe) and MENA associations (e.g., EGP → Egypt).

- **`Experiment3.ipynb`** – Performs causal ablation by zeroing out selected final‑token residual states to measure the “damage” to target‑vs‑competitor logit differences, further isolating critical decision layers.

- **`PathPatching.ipynb`** – Drops down to the attention‑head level, patching individual head outputs from corrupted to clean runs to identify the specific components driving the geographic routing (e.g., L17H7).

- **`Control.ipynb`** – Runs baseline syntactic and transformation tasks (e.g., uppercase/lowercase mapping) to prove that the identified geographic circuit is specialized, rather than just a general late‑stage processing layer.

- **`induction_head_test.ipynb`** – Uses `circuitsvis` to render and validate general attention head behaviors within the model.


##  Diagnostics

The `diagnostics` folder contains early‑stage sanity checks used to validate the activation patching methodology before applying it to the complex geographic prompts. These files are **not** part of the final experimental results.

- **`activation_patching_nutrition.ipynb`** – Validates patching on a basic food/nutrition prompt structure.

- **`activation_patching_sentiment.ipynb`** – Validates patching on a basic positive/negative sentiment prompt structure.

Hardware / Technical Notes
Base Model: Qwen/Qwen2-0.5B

Framework: TransformerLens (HookedTransformer)

Precision: Computed in float32. The scripts will automatically default to cuda if available, or fallback to cpu.

Note on Weights: As per Qwen2's architecture, LayerNorm is skipped in some writing weight centering functions, which is normal and handled safely by the scripts. Interactive Plotly graphs will be generated and saved as .html files in your working directory when running the notebooks.
