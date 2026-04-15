# Multi-Model Convergence via Accumulated Embeddings

Multi-model workflows discard intermediate embeddings — collecting and feeding them to the final model produces richer, more human-like comprehension than output-only pipelines.

- Current practice: workflow engineers read only the final model's output, discarding all intermediate embedded data from prior models in the chain
- Proposed approach: accumulate all intermediate embeddings from every model in the workflow and pass the full set to the final model
- Extended approach: final output is a comparison across multiple model groups, each producing additional embedded data, iterated in a round-robin until convergence
- Halting criterion: iteration stops when data ranks highly — emergent consensus, not a fixed step count
- Analogy to vivify: the co-occurrence graph is the accumulated embedding; it grows with each inference pass and stabilizes when concepts are genuinely central
- Analogy to human reasoning: humans do not discard what they thought along the way — intermediate reasoning is part of the final judgment

## Why current workflows lose meaning

Chunking and output-only pipelines are rational abstractions that destroy the sense layer — the holistic, analogical context that carries human meaning.

- Chunking severs relationships and arguments that span chunk boundaries
- Output-only pipelines discard the semantic accumulation that built the final answer
- Each model in a workflow embeds the input differently — that diversity is signal, not noise
- Throwing away intermediate embeddings is equivalent to reading only a conclusion without the reasoning

## The round-robin convergence model

A group of models each processes the same input, produces embedded data, and passes that data to the next model — iterating until the output stabilizes.

- Each model brings a different semantic angle: some more analogical, some more analytical
- Intermediate outputs feed forward as context, not just as prompts
- Convergence is detected when successive iterations produce high-ranking, low-divergence outputs
- This mirrors the vivify tension score: low tension across iterations signals stable beneficial structure

## Connection to vivify pipeline

The vivify-inferences pipeline implements a single-model version of this idea across time rather than across simultaneous models.

- Each inference pass adds keywords to the co-occurrence graph
- The graph is the accumulated embedding — it grows and stabilizes across sessions
- High co-occurrence counts are the convergence signal
- The tension score between left and right keywords measures divergence — the same signal the round-robin uses to halt

## Implementation direction

A multi-model convergence layer sits above the vivify pipeline and feeds accumulated embeddings downward.

- Each model in the workflow writes its intermediate embeddings as inference units to vivify
- The final model receives the full vivified graph, not just the last output
- Comparison between model groups becomes a tension score across their keyword sets
- Halting when the graph stabilizes is the same as halting when tension stops changing

<!-- llm: claude-sonnet-4-6 | 2026-04-15 | repos/pillars/MULTI_MODEL_CONVERGENCE.md | created — multi-model convergence via accumulated embeddings, round-robin halting, vivify connection -->
