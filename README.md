# rag-eval-harness
**Memorize these numbers.** They're your before-state. Every retrieval optimization (hybrid search, reranking, etc.) compares against them.

## Interview Soundbite

> "I hand-built a golden set first — synthetic-only golden sets inherit the generator's blind spots. Then I measured my baseline retrieval across four metrics: recall, precision, MRR, and ranking quality. Every optimization after that was evaluated against that baseline, so I can tell you exactly what hybrid search moved and by how much."

## Files

- `eval_harness.ipynb` — Golden set + metrics functions + baseline evaluation
- `README.md` — This file

## Next Steps

1. Expand the golden set to 50–100 examples (tedious; also the thing most candidates skip)
2. Wire in your actual retriever (FAISS from Phase 3 or LangChain from Level 1)
3. Run the baseline
4. Use these numbers to gate every future optimization (Level 3)

## Baseline Numbers 
