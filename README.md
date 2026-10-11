# DecodingTrust evaluation of Phi-3.5-mini-instruct

Code and report for 1RT730 Hand-in Assignment 2, "Evaluating and Improving LLM Trustworthiness".

We evaluate `microsoft/Phi-3.5-mini-instruct` on three DecodingTrust dimensions (toxicity, stereotype bias, privacy). Then we mitigate privacy leakage, the weakest dimension.

> **Warning:** the notebooks and the report contain offensive model outputs and PII from the public Enron corpus.

## Notebooks

| Notebook | Part | What it does |
|---|---|---|
| `LLM_A2_revision.ipynb` | A | Runs the three DecodingTrust subsets and scores the replies. **Toxicity:** RealToxicityPrompts and GPT-3.5/GPT-4 toxic prompts, scored with Detoxify. **Stereotype bias:** agreement rate. **Privacy:** Enron PII leak and refusal rates. |
| `LLM_A2_Mitigation1.ipynb` | B | Compares the Part A privacy baseline with three mitigations: S1 refusal policy (system prompt), S2 PII scrubbing (regex output filter) and S1+S2. It also runs a utility check and a paired McNemar test. |

Both notebooks are saved with all cell outputs.

### Running them

1. Open the notebook in Google Colab and select a T4 GPU.
2. Add a Hugging Face token as the Colab secret `HF_TOKEN`, or set it as an environment variable.
3. Run all cells. The first cell installs the dependencies (`transformers`, `accelerate`, `datasets`, `detoxify`, `pandas`, `matplotlib`, and others).

Part B reuses the privacy results of Part A for its baseline, so run Part A first.

## Report

| File | Content |
|---|---|
| `assignment2.tex` | Report source |
| `assignment2.pdf` | Compiled report |
| `appendix_failures.tex` | Appendix with failure examples (included by the report) |
| `figures/` | Figures used in the report |

### Compiling the report

You need a LaTeX distribution (TeX Live or MacTeX) and Python with `pygments`. The `minted` package needs both.

```bash
pip install pygments
pdflatex -shell-escape assignment2.tex
pdflatex -shell-escape assignment2.tex
```

Run `pdflatex` twice so that figure, table and appendix references resolve. The `-shell-escape` flag is required by `minted`.

You can also upload the folder to Overleaf. It compiles there without changes, because Overleaf enables shell escape by default.
