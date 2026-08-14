# RAG Eval Harness

> Retrieval evaluation metrics — precision@k, recall@k, MRR, and NDCG@k — implemented
> from first principles rather than imported, as the measurement layer for the RAG
> pipelines in [`rag-from-scratch`](https://github.com/Victorianukiry/rag-from-scratch)
> and [`rag-three-ways`](https://github.com/Victorianukiry/rag-three-ways).

## Status

**🚧 Metrics implemented and unit-checked. Golden set and baseline run in progress.**

The four metric functions are complete and correct. They are currently exercised against
a small illustrative golden set with **simulated retrieval results** — the live retriever
is not yet wired in, and no baseline has been measured. Nothing in this repo should be
read as a performance claim about the RAG pipelines.

Being explicit about that is the point. An evaluation repo that overstates what it has
measured defeats its own purpose.

## Why Write the Metrics By Hand?

Because the arguments happen at the margins, and you can't have those arguments about a
function you imported:

- **Precision@k** — denominator is `k`, not the number of results returned. If the
  retriever returns fewer than `k`, precision is understated. Deliberate, and worth
  knowing.
- **Recall@k** — measures coverage of the known-relevant set. This is the metric that
  moves when chunking or `k` changes, and the one that mattered in the pipeline repos.
- **MRR** — reciprocal rank of the *first* relevant result. Rewards getting one good
  chunk to the top; says nothing about the rest.
- **NDCG@k** — the only one of the four that is sensitive to the ordering of all relevant
  results, not just the first. IDCG is computed against a perfect ranking with binary
  relevance capped at `k`.

Knowing which metric responds to which change is the difference between tuning a
retriever and guessing at one.

## What's Here

- `retrieval_metrics_.ipynb` — the four metric functions, a worked example, and a
  golden-set evaluation loop driven by simulated retrieval output
- `README.md` — this file

## Roadmap

1. **Build a real golden set.** 20–30 questions answerable from the actual insurance
   corpus, with chunk IDs taken from the live FAISS index (166 chunks from-scratch /
   237 LangChain). The current 5-question set is a placeholder written to exercise the
   functions — its questions and chunk IDs do not correspond to the corpus.
2. **Wire in the real retriever**, replacing the simulated result lists.
3. **Run and publish the baseline.**
4. **Add hybrid search (BM25 + dense) and a reranker**, rerun, and publish the delta
   against that baseline.

Step 4 is the reason for the whole repo. Optimizations that aren't measured against a
recorded baseline are just changes.

## A Note on Golden Sets

I'm hand-building the golden set rather than generating it with an LLM. Synthetic sets
inherit the generator's blind spots: the questions it thinks to ask are the questions the
retriever is already likely to handle. Hand-building is slower and it's the step most
people skip, which is exactly why it's worth doing.

## Baseline Numbers

*Not yet measured. This section will be filled in once step 3 above is complete.*
