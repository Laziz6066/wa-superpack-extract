# Local Open-Weight Coding LLMs and Software Stack (late October 2026)

> **Method note (important for the writer):** In this session, direct page fetching was blocked for every host I tried (huggingface.co, morphllm.com, pinggy.io, promptquorum.com all failed DNS under the session network allowlist). Every finding below comes from web-search result summaries, which pull from the cited pages. **Nothing was verified on a model card or primary page.** Most sources are secondary blogs or aggregators. Benchmark numbers are mostly vendor-reported, and sources often disagree. Please carry these caveats into the report. Research date: 2026-10-30.

## 1. Top open coding models in late 2026, their sizes, and what fits at each memory tier

### Takeaway
By late October 2026, the main local coding models are Alibaba's general Qwen 3.6/3.8 line and the Qwen3-Coder line. Qwen3.8-27B (dense) is the most-cited pick for 24–32 GB, and Qwen3.6-35B-A3B / Qwen3-Coder-Next (80B-A3B) are the picks for 48–64 GB. At 16 GB the usual choices are gpt-oss-20b and Devstral Small 2 (24B). At 96–128 GB, sources point to gpt-oss-120b, Laguna S 2.1 (118B) and Devstral 2 (123B), or a 2–3-bit quant of DeepSeek V4 Flash (284B-A13B). The frontier-class open models (DeepSeek V4-Pro, GLM-5.x, Kimi K2.6, Qwen3.5-397B) do not fit usefully in 128 GB.

### Cited Findings
**Qwen family**
- Qwen3.8-27B is described as a dense 27B vision-language model under Apache-2.0 with 262K native context. It scores 61.7 on SWE-bench Pro (up from 53.5 for Qwen3.6-27B) and 73.0 on Terminal-Bench 2.1 (Terminus), up from 63.4. All are vendor figures, and Qwen ran SWE-bench Pro with Claude Code as the harness. I found no official SWE-bench Verified number. A Hugging Face discussion questions whether the benchmark table can be trusted. — [morphllm Qwen 3.8](https://www.morphllm.com/qwen-3-8); [Northflank](https://northflank.com/blog/qwen3-8-27b-performance-benchmarks-gpu-requirements-and-how-to-run-it); [HF FP8 card](https://huggingface.co/qwen/qwen3.8-27b-fp8); [kingy.ai](https://kingy.ai/blog/qwen3-8-27b-specs-benchmarks-local-hardware/)
- Several Oct-2026 guides name Qwen3.8-27B the top local pick for a 24 GB GPU or a 32 GB Mac, saying it runs in about 18 GB (quant not specified, likely ~Q4). — [Tembo](https://www.tembo.io/blog/best-local-llm-for-coding); [Atomic Chat](https://atomic.chat/blog/guides/best-local-llms-for-coding); [PromptQuorum](https://www.promptquorum.com/local-llms/best-local-llms-for-coding)
- Qwen3.6-27B is reported at 77.2 on SWE-bench Verified (secondary source). A separate claim of 90.0% comes from an unofficial custom harness and is not credible as a comparison. — [insiderllm Qwen guide](https://insiderllm.com/guides/qwen-models-guide/); [HF discussion](https://huggingface.co/Qwen/Qwen3.6-27B/discussions/33)
- Qwen3.6-35B-A3B has 35B total and 3B active parameters. Qwen's table gives it 73.4 on SWE-bench Verified, 67.2 on SWE-bench Multilingual and 49.5 on SWE-bench Pro. It is a general model, not a coding specialist. — [Medium review](https://medium.com/data-science-in-your-pocket/qwen3-6-35b-a3b-the-tiny-active-open-model-that-thinks-codes-and-agents-like-a-much-bigger-one-486d535e372e); [buildfastwithai](https://www.buildfastwithai.com/blogs/qwen3-6-35b-a3b-review); [Labellerr](https://www.labellerr.com/blog/qwen3-6-35b-a3b-open-source-ai-model/)
- A Hacker News user reports that Qwen 3.6 35B-A3B solved only 11 of 98 "Power Ranking" tasks. This is an anecdotal reality check against the headline scores. — [HN](https://news.ycombinator.com/item?id=47798382)
- Qwen3-Coder-Next has 80B total and 3B active parameters. It scores about 70.6% on SWE-bench Verified with SWE-Agent (71.3% with OpenHands), and a community reproduction got 68.4%. Unsloth says it needs about 46 GB at 4-bit and 85 GB at 8-bit. Q4_K_M is about 48.4 GB and runs at roughly 28 tok/s on an M4 Max 128GB. All 80B weights must be resident, so a 24 GB GPU needs CPU offload. — [Unsloth](https://unsloth.ai/docs/models/qwen3-coder-next); [willitrunai](https://willitrunai.com/models/qwen-3-coder-next); [runaihome](https://runaihome.com/blog/qwen3-coder-next-local-ai-hardware-guide-2026/); [openaitoolshub](https://www.openaitoolshub.org/en/blog/qwen3-coder-next-review-local-coding)
- The older Qwen3-Coder line includes 30B-A3B (30.5B total, 3.3B active) and the 480B-A35B flagship. I found no dedicated "Qwen3.5-Coder". The Qwen3.5 family is general-purpose, from 0.8B up to 397B-A17B. Its medium sizes are 27B dense, 35B-A3B and 122B-A10B, and Qwen3.5-397B reports 76.4 and Qwen3.5-27B 72.4 on SWE-bench Verified. — [insiderllm](https://insiderllm.com/guides/qwen-models-guide/); [morphllm Qwen 3.5](https://www.morphllm.com/qwen-3-5); [digitalapplied](https://www.digitalapplied.com/blog/qwen-3-5-medium-model-series-benchmarks-pricing-guide)

**OpenAI gpt-oss**
- gpt-oss-120b has 117B total and 5.1B active parameters, and gpt-oss-20b has 21B total and 3.6B active. Both are Apache 2.0 with native MXFP4 weights. OpenAI reports 62.4 (120b) and 60.7 (20b) on SWE-bench Verified at high reasoning. These are Aug-2025 models, and I found no successor as of Oct 2026. — [OpenAI model card PDF](https://cdn.openai.com/pdf/419b6906-9da6-406c-a19d-1bb078ac7637/oai_gpt-oss_model_card.pdf); [SemiAnalysis InferenceX](https://inferencex.semianalysis.com/model/gptoss-120b)
- Guides still recommend gpt-oss-20b for 16 GB VRAM and gpt-oss-120b for 64 GB and up. — [Tembo](https://www.tembo.io/blog/best-local-llm-for-coding); [KDnuggets](https://www.kdnuggets.com/top-7-coding-models-you-can-run-locally-in-2026)

**Mistral Devstral**
- Devstral 2 is a 123B dense model with 256K context under a modified MIT license, and Mistral reports 72.2% on SWE-bench Verified. Devstral Small 2 is 24B under Apache 2.0 at 68.0%. Mistral released them alongside its Vibe CLI. One comparison table lists Devstral Small 2 at about 58%, which conflicts with Mistral's figure. Memory estimates for the 123B model range from a ~75 GB Ollama pull to 128 GB. — [Mistral](https://mistral.ai/news/devstral-2-vibe-cli/); [DigitalOcean](https://www.digitalocean.com/community/tutorials/devstral-2-mistral-coding-open-weight-model); [canirun.ai](https://www.canirun.ai/model/devstral-2-123b/); [localaimaster](https://localaimaster.com/models/devstral)

**Poolside Laguna (new in 2026, US lab)**
- Laguna XS 2.1 is a ~33B MoE with about 3B active, sized for a single desktop or laptop GPU. Laguna S 2.1 is 118B and runs on one DGX Spark, with weights in BF16, FP8, INT4 and NVFP4 under OpenMDW-1.1. Official GGUF and MLX builds are planned. Laguna M.1 is 225B. Benchmarks are self-reported and not yet independently verified, and sources give conflicting release dates (July 21 vs Aug 24, 2026). — [HPCwire](https://hpcwire.com/aiwire/2026/08/24/poolside-launches-laguna-s-2-1-open-weight-coding-model); [OpenSourceForU](https://www.opensourceforu.com/2026/07/poolside-ai-launches-open-weight-laguna-coding-models/); [runtimewire](https://runtimewire.com/article/poolside-laguna-s-2-1-open-weight-coding-model); [HF poolside](https://huggingface.co/poolside)

**DeepSeek V4 family**
- V4-Pro is about 1.6T parameters (MoE, MIT license), with weights on HF since April 2026. Newer V4-Pro-0813 and V4.1-Flash weights are also listed. — [mindstudio](https://www.mindstudio.ai/blog/deepseek-v4-open-source-frontier-model-review); [Medium V4 review](https://medium.com/@leucopsis/deepseek-v4-review-a23ce940151c)
- V4-Flash is about 284B total and 13B active, with 1M context. antirez's GGUFs range from about 81 GiB (q2) to 153 GiB (q4). He suggests q2 for 128 GB Macs and q4 for machines with 256 GB or more. Unsloth's builds are 103 GB at 3-bit and 162 GB at 8-bit. On a 128 GB Mac you need to raise the wired limit (`sudo sysctl iogpu.wired_limit_mb=114688`), and context will be modest. — [antirez GGUF](https://huggingface.co/antirez/deepseek-v4-gguf); [antirez/ds4](https://github.com/antirez/ds4); [Unsloth V4](https://unsloth.ai/docs/models/deepseek-v4); [terminalbytes](https://terminalbytes.com/run-deepseek-v4-flash-at-home/); [mindstudio Dwarf Star](https://www.mindstudio.ai/blog/run-deepseek-v4-flash-locally-dwarf-star-macbook)
- V4.1-Flash (released Sept 10, 2026) is much larger: Unsloth describes it as a ~552B backbone plus 196B "Engram" parameters, with a 1-bit quant of about 250 GB. There is also an arXiv paper on its KV-cache compression. — [Unsloth V4.1 Flash](https://unsloth.ai/docs/models/deepseek-v4.1-flash); [arXiv 2609.19969](https://arxiv.org/pdf/2609.19969); [Tech Insider](https://tech-insider.org/deepseek-v4-1-flash-uncensored-abliterated-huggingface-2026/)

**Large open models (cloud/server class, not ≤128 GB)**
- GLM-5.2 (June 2026) is a 753B open-weight model with 1M context under MIT. It scores 62.1 on SWE-bench Pro, against 58.6 for GPT-5.5 and 69.2 for Claude Opus 4.8. GLM-5 (base) reports 77.8% on SWE-bench Verified against 81.4% for Opus 4.6. GLM-5.3 exists, and its open weights were announced for a later date. — [digitalapplied GLM-5.2](https://www.digitalapplied.com/blog/glm-5-2-benchmarks-open-weights-vs-claude-opus); [morphllm GLM-5.2](https://www.morphllm.com/glm-5-2); [danilchenko](https://www.danilchenko.dev/posts/glm-5-2-review/); [atoms.dev GLM-5.3](https://atoms.dev/blog/glm-5-3-benchmarks-api-coding-open-weights); [serenitiesai GLM-5.1](https://serenitiesai.com/articles/glm-5-1-zhipu-coding-benchmark-claude-opus-comparison-2026)
- A May 2026 guide places MiniMax M2.5 (80.2%), DeepSeek V4-Pro-Max (80.6%) and Kimi K2.6 (80.2%) in the "80% band" on SWE-bench Verified. I found no primary source for these. Older MiniMax M2 was 69.4%. — [aimadetools/Devstral guide and related comparisons via search](https://www.aimadetools.com/blog/devstral-2-complete-guide/)
- I found no 2026-specific data on Seed-OSS or Kimi K2 sizes. See Gaps.

### Inferences
- **Rough memory rule of thumb:** Q4_K_M is about 0.55–0.6 bytes per parameter and Q8 about 1.05 bytes per parameter, plus 2–10 GB for KV cache and runtime. This is consistent with the Qwen3-Coder-Next figures (80B at 46–48 GB Q4 and 85 GB Q8).
- **Tier map (my synthesis):**
  - **16 GB:** gpt-oss-20b (MXFP4, ~13–14 GB) or Devstral Small 2 24B (Q4 ~14 GB, tight with context). Qwen3.8-27B at Q3 or with KV offload is a stretch.
  - **24–32 GB:** Qwen3.8-27B at Q4–Q6 (the consensus pick), Devstral Small 2 at Q6–Q8, or Qwen3.6-35B-A3B at Q4 (~20 GB).
  - **48–64 GB:** Qwen3-Coder-Next 80B-A3B at Q4 (~48 GB), Qwen3.8-27B at Q8, or Qwen3.6-35B-A3B at Q8. On 64 GB, gpt-oss-120b (~63 GB MXFP4) leaves almost no room for context.
  - **96–128 GB:** gpt-oss-120b, Qwen3-Coder-Next at Q8 (85 GB), Laguna S 2.1 at INT4, Devstral 2 123B at Q4 (~75 GB), Qwen3.5-122B-A10B at Q4, or DeepSeek V4-Flash at q2–q3 (81–103 GB, tight).
- **What does not fit even at Q4 in 128 GB:** Qwen3-Coder-480B, Qwen3.5-397B, GLM-5.x (753B), DeepSeek V4-Pro (1.6T), V4.1-Flash and Kimi K2.x (~1T). These are "API or server" models.
- **Speed:** MoE models with ~3B active (Qwen3.6-35B-A3B, Coder-Next, Laguna XS) are much faster on Macs and with CPU offload than dense 27B or 123B models. This matters for agentic loops.

### Gaps
- I could not open any model card directly, so sizes and quant footprints are from secondary pages.
- I found no Seed-OSS 2026 update, no exact Kimi K2.6 or MiniMax M2.5 parameter counts or licenses from primary sources, and no GGUF size for Qwen3.6-35B-A3B or Laguna.
- Sources disagree on Qwen3.8-27B's release date.

## 2. Benchmarks: local-sized models vs Claude/GPT, and whether "Opus-level DeepSeek" holds up

### Takeaway
On SWE-bench Verified, the best ≤128 GB-runnable models sit around 68–77% (vendor-reported). The best open frontier models (DeepSeek V4-Pro, Kimi K2.6, MiniMax M2.5, GLM-5) sit around 78–81%. Current Claude Opus (4.7/4.8/5.x) is reported at about 87–89%. "Opus-level DeepSeek" is roughly true only against Opus 4.6 (Feb-2026 era, ~80–81%), and only for DeepSeek V4-Pro, a ~1.6T model you cannot run on a $2000 machine. The 91% claims are unverified.

### Cited Findings
- A tracker-based source puts DeepSeek-V4-Pro-Max at 80.6% on SWE-bench Verified, against 80.8% for Claude Opus 4.6 and 87.6% for Opus 4.7, and warns the harness may use a loose verifier. A blog claim of about 91.2% for V4-Pro (vs 93.9% for Opus 4.7) looks unverified. Another comparison lists Opus 4.8 at 88.6%. — [nxcode](https://www.nxcode.io/resources/news/deepseek-v4-release-specs-benchmarks-2026); [buildfastwithai V4-Pro](https://www.buildfastwithai.com/blogs/deepseek-v4-pro-review-2026); [mindstudio](https://www.mindstudio.ai/blog/deepseek-v4-open-source-frontier-model-review)
- An arXiv paper reports that V4.1-Flash beats "Opus-5" on the DeepSWE benchmark, which is a different benchmark from SWE-bench Verified. — [arXiv 2609.19969](https://arxiv.org/pdf/2609.19969); [DeepSWE arXiv 2607.07946](https://arxiv.org/pdf/2607.07946)
- On SWE-bench Pro, GLM-5.2 scores 62.1, GPT-5.5 58.6 and Claude Opus 4.8 69.2. — [digitalapplied](https://www.digitalapplied.com/blog/glm-5-2-benchmarks-open-weights-vs-claude-opus)
- On Terminal-Bench 2.1, Qwen3.8-27B scores 73.0 (vendor, Terminus harness) against 78.2 for Opus 4.6 Max. — [morphllm Qwen 3.8](https://www.morphllm.com/qwen-3-8)
- Local-sized SWE-bench Verified scores: Qwen3.6-27B 77.2 (secondary), Qwen3.6-35B-A3B 73.4, Devstral 2 72.2, Qwen3.5-27B 72.4, Qwen3-Coder-Next 70.6 (reproduced at 68.4), Devstral Small 2 68.0, gpt-oss-120b 62.4, gpt-oss-20b 60.7. — sources as in section 1
- OpenAI published a note titled "Why SWE-bench Verified no longer measures frontier coding capabilities" (Feb 2026). I saw only the title in reference lists. SWE-bench Pro and Terminal-Bench are now the more commonly cited benchmarks. — [arXiv SWE-Bench Pro Verified](https://arxiv.org/pdf/2609.08149)
- GLM-5.1 is marketed as reaching "94.6% of Claude Opus 4.6 coding performance". — [serenitiesai](https://serenitiesai.com/articles/glm-5-1-zhipu-coding-benchmark-claude-opus-comparison-2026)

### Inferences
- Benchmark numbers from different harnesses (Claude Code, OpenHands, SWE-Agent, vendor scaffolds) are not directly comparable, and contamination plus saturation of SWE-bench Verified make the gaps look smaller than they feel in practice. The HN 11/98 anecdote and the reproduction gap of about 2 points support this.
- Practical ladder: ≤128 GB local models ≈ frontier from roughly 12–18 months earlier (Claude Sonnet 4 / GPT-5-mini class). Open trillion-parameter models ≈ Opus 4.6. Current Claude Opus 5.x and GPT-5.5 remain ahead, especially on long-horizon agentic work.
- I did not find Aider polyglot or LiveCodeBench numbers for the 2026 models in these searches. See Gaps.

### Gaps
- I have no current Aider polyglot or LiveCodeBench leaderboard values, because the leaderboard pages could not be fetched.
- There is no official SWE-bench Verified score for Opus 5 or 5.5 in my sources.
- The scores for Kimi K2.6 and MiniMax M2.5 have no primary source.

## 3. "Uncensored DeepSeek" (2026) and abliterated models

### Takeaway
Yes. Within hours of DeepSeek V4.1-Flash's release (Sept 10, 2026, MIT license), community "abliterated/uncensored" forks appeared on Hugging Face, for example dealignai/DeepSeek-V4.1-Flash-UNCENSORED-FP8 and a -1017 variant. Earlier V4-Flash abliterated builds also exist. These are community forks, not DeepSeek releases, and they are far too large for a $2000 PC: a V4-Flash Q4 is about 154 GB, and V4.1-Flash is much larger. The measured quality loss is modest (about 4 MMLU points).

### Cited Findings
- Abliterated and uncensored forks of V4.1-Flash hit HF within hours of the Sept 10, 2026 release. There were about 31 builds, and dealignai's FP8 build was the most-downloaded tracked fork at about 2,254 downloads by mid-October. — [Tech Insider](https://tech-insider.org/deepseek-v4-1-flash-uncensored-abliterated-huggingface-2026/); [pasqualepillitteri](https://pasqualepillitteri.it/en/news/16070/deepseek-41-flash-uncensored-abliterated-builds); [HF dealignai](https://huggingface.co/dealignai/DeepSeek-V4.1-Flash-UNCENSORED-FP8); [HF dealignai 1017](https://huggingface.co/dealignai/DeepSeek-V4.1-Flash-1017-UNCENSORED-FP8)
- The maker's card reports MMLU of 83.77% for the uncensored build vs 87.63% for the base. Another writeup gives 82.7% vs 87.0% and says the loss is concentrated in moral scenarios and professional law. The card also warns that low-bit versions should redo abliteration at the target precision rather than quantizing the FP8 bundle. — [DEV.to testing](https://dev.to/purpledoubled/deepseek-v41-flash-uncensored-what-weight-level-abliteration-costs-and-what-we-saw-in-testing-2o8n); [HF dealignai](https://huggingface.co/dealignai/DeepSeek-V4.1-Flash-UNCENSORED-FP8)
- One tester saw broken vision output on the uncensored build. — [DEV.to](https://dev.to/purpledoubled/deepseek-v41-flash-uncensored-what-weight-level-abliteration-costs-and-what-we-saw-in-testing-2o8n)
- An X user notes that "regular DeepSeek already refuses far less than Claude on a lot of technical work" and that abliteration doesn't seem to hurt coding much. This is anecdotal. — [X post](https://x.com/yuhasbeentaken/status/2114709332570816891)
- V4-Flash abliterated is described as "the most downloaded uncensored model of 2026". Its Q4 GGUF is about 154 GB and needs the 192 GB memory class. There is also a 2× DGX Spark abliterated build. — [locallyuncensored](https://locallyuncensored.com/blog/deepseek-v4-flash-abliterated.html); [NVIDIA forums](https://forums.developer.nvidia.com/t/deepseek-v4-flash-dspark-abliterated-uncensored-2x-dgx-spark/376500)
- Abliterated GGUFs by VRAM exist for Qwen 3.6, Gemma 4 and Llama. There is also a Qwen3.6-35B-A3B "Claude 4.6 Opus Reasoning Distilled" fine-tune. Such distills are community fine-tunes, not Anthropic products. — [locallyuncensored guide](https://locallyuncensored.com/blog/abliterated-models-guide.html); [HF hesamation](https://huggingface.co/hesamation/Qwen3.6-35B-A3B-Claude-4.6-Opus-Reasoning-Distilled)

### Inferences
- **Abliteration explained:** it finds the "refusal direction" in the model's activations and projects it out of the weights. No retraining is involved. The model stops refusing, at a small capability cost of a few MMLU points here, with larger risk at low-bit quants.
- **Relevance for coding:** low. Coding prompts are rarely refused, and abliterated forks are unofficial, less tested and carry supply-chain trust risk.

### Gaps
- I found no coding-specific benchmark (SWE-bench, LiveCodeBench) for the abliterated DeepSeek builds.

## 4. Software stack: runtimes, editor and agent integration, Claude Code with local models, context and KV cache

### Takeaway
Ollama (0.14/0.15+), LM Studio (0.4.1+) and llama.cpp's `llama-server` all now speak the Anthropic Messages API natively. That means Claude Code can be pointed at a local model with `ANTHROPIC_BASE_URL` and no proxy. In the editor, Cline, Kilo Code (the successor to Roo Code, which was archived in May 2026), Continue, OpenCode and Aider all support local backends. Agentic coding needs 64K–128K+ of context, and KV cache for a 27B hybrid-attention Qwen costs about 4–8 GB at 128K.

### Cited Findings
- Ollama added Anthropic-API support in Jan 2026 (v0.14.0+). `ollama launch claude` auto-setup is listed for 0.15+. The manual setup is `ANTHROPIC_BASE_URL=http://localhost:11434` with `ANTHROPIC_AUTH_TOKEN=ollama`. — [morphllm Ollama+Claude Code](https://www.morphllm.com/ollama-claude-code); [vdf.ai](https://vdf.ai/blog/claude-code-local-llm-setup/)
- llama.cpp `llama-server` exposes `/v1/messages` plus a token-count endpoint, so Claude Code gets exact token counts. Run it with `--jinja`. LM Studio 0.4.1+ works on port 1234. — [vdf.ai](https://vdf.ai/blog/claude-code-local-llm-setup/); [DEV.to rosgluk](https://dev.to/rosgluk/claude-code-install-and-config-for-ollama-llamacpp-pricing-3842); [GitHub gist](https://gist.github.com/renezander030/39249215616a095d74fe6c66b0348641)
- Caveats: local inference is much slower than the Claude API, and a GitHub issue reports Claude Code hanging on an Ollama backend. Guides recommend at least 64K context. — [HF blog](https://huggingface.co/blog/GhostScientist/claude-code-with-local-models); [anthropics/claude-code #51239](https://github.com/anthropics/claude-code/issues/51239); [gist](https://gist.github.com/renezander030/39249215616a095d74fe6c66b0348641); [KDnuggets](https://www.kdnuggets.com/pairing-claude-code-with-local-models); [runlocalai](https://www.runlocalai.co/guides/claude-code-with-local-models)
- Qwen ran its own SWE-bench Pro evaluations of Qwen3.8 through Claude Code, which signals that Claude Code works as a harness for open models. Qwen also ships its own Qwen Code CLI. — [morphllm Qwen 3.8](https://www.morphllm.com/qwen-3-8); [qwen-code GitHub release](https://github.com/QwenLM/qwen-code/releases/tag/dsw-eas-full-20260821-r1)
- Mistral ships Vibe CLI alongside Devstral 2. — [Mistral](https://mistral.ai/news/devstral-2-vibe-cli/)
- Roo Code was archived in May 2026 (final release May 15, 2026), and Kilo Code is the recommended successor with compatible config. Aider reportedly has had no commits since May 22, 2026. Cline runs in VS Code, JetBrains, Cursor and Windsurf with BYOK and local models. OpenCode supports 75+ providers plus Ollama, LM Studio and llama.cpp. Continue + Ollama is cited as the go-to for air-gapped IDE use, though its maintenance status is disputed. — [baeseokjae comparison](https://baeseokjae.github.io/posts/open-source-ai-coding-agents-2026/); [baeseokjae Cline alternatives](https://baeseokjae.github.io/posts/cline-alternatives-2026/); [insiderllm](https://insiderllm.com/guides/local-alternatives-claude-code-2026/); [nimbalyst](https://nimbalyst.com/blog/best-local-first-ai-coding-tools-2026/); [morphllm open-source assistants](https://www.morphllm.com/ai-coding-assistant-open-source)
- Qwen 27B-class (3.5/3.8) uses hybrid attention: 48 linear plus 16 full-attention layers, so only 16 layers hold a growing KV cache. That is about 64 KB per token at f16, or 8 GB at 128K. At q8_0 it is about 34 KiB per token (~4.25 GB at 128K, my arithmetic). With Q8-K/Q4-V, one user reports about 2.5 GB at ~100K on a 16 GB RTX 5070 Ti. — [DEV.to Qwen 3.8 local](https://dev.to/purpledoubled/run-qwen-38-27b-locally-real-gguf-sizes-the-kv-cache-trick-and-the-template-trap-114j); [llama.cpp discussion](https://github.com/ggml-org/llama.cpp/discussions/28894); [Medium KV streaming](https://medium.com/@raymond860909/running-qwen-27b-on-16g-vram-with-full-context-length-building-adaptive-kv-cache-streaming-for-bf1e819116e9)
- For 16 GB GPUs at 128K, the cache can consume most of VRAM. The advice is to use a GQA or hybrid model, a Q8 (or tested Q4) KV cache, and a single sequence. Measured llama.cpp allocations matched the formula (e.g. 972 MiB at 32K and 3,888 MiB at 128K for one model). — [glukhov](https://www.glukhov.org/llm-performance/optimization/kv-cache-16gb-long-context/); [sotaaz](https://sotaaz.com/post/kv-cache-by-model-en)
- The "template trap": wrong chat or tool-call templates break agentic tool use for Qwen 3.8 GGUFs, so use `--jinja` and the official template. — [DEV.to](https://dev.to/purpledoubled/run-qwen-38-27b-locally-real-gguf-sizes-the-kv-cache-trick-and-the-template-trap-114j)

### Inferences
- **Stack recommendation:**
  - NVIDIA: llama.cpp `llama-server` or Ollama, with vLLM for multi-user or FP8/AWQ serving.
  - Mac: LM Studio (MLX backend) or llama.cpp.
  - Front ends: Claude Code, OpenCode or Qwen Code in the CLI; Cline, Kilo or Continue in the IDE.
- Claude Code's system prompt and tool definitions are large (tens of thousands of tokens). This, together with the 64K minimum context, is why small-VRAM setups struggle with it. Lighter harnesses (Aider, OpenCode) may suit 16 GB better.
- Older full-attention models (e.g. dense GQA without hybrid layers) can need 10–20+ GB of KV at 128K. Model choice affects context budget as much as weight size does.

### Gaps
- I could not confirm current version numbers for Ollama, LM Studio, MLX or vLLM, or Zed's local-model support details.
- I found no source on Zed specifically, and no primary documentation was fetched.

## 5. Cost comparison: APIs and subscriptions vs ~$2000 local hardware

### Takeaway
Cheap Chinese APIs are extremely inexpensive: DeepSeek V4.1-Flash costs about $0.15/$0.60 per million tokens off-peak, and the GLM Coding Plan starts at $18/month. Claude Pro is $20/month and Max $100–200/month. A $2000 machine amortized over 3 years is about $55/month before electricity, and it runs models a tier or two below what $18–20/month subscriptions give access to. Local wins on privacy, offline use and unlimited usage, not on cost or quality.

### Cited Findings
- DeepSeek introduced peak/off-peak billing on Aug 16, 2026. V4(.1)-Flash costs $0.30/$1.20 at peak and $0.15/$0.60 off-peak, and V4-Pro $1.32/$3.96 at peak and $0.66/$1.98 off-peak. Earlier rates were Flash $0.14/$0.28 and Pro $1.74/$3.48, with a 75% promo bringing Pro to $0.435/$0.87. These figures come from third-party pages and were not confirmed on the official DeepSeek docs. — [techjacksolutions](https://techjacksolutions.com/ai-tools/deepseek/deepseek-pricing/); [costgoat](https://costgoat.com/pricing/deepseek-api); [cloudzero](https://www.cloudzero.com/blog/deepseek-pricing/); [spheron](https://www.spheron.network/blog/deepseek-api-vs-self-hosted-llms-cost-privacy-2026/); [cabina](https://cabina.ai/blog/deepseek-api-pricing/)
- GLM API pricing is about $1.00/$3.20 per million tokens for GLM-5 and about $1.40/$4.40 for GLM-5.2. GLM Coding Plan: Lite $18, Pro $72 and Max $160 per month (checked July 22, 2026), and it includes GLM-5.3. — [morphllm GLM-5.2](https://www.morphllm.com/glm-5-2); [danilchenko](https://www.danilchenko.dev/posts/glm-5-2-review/); [diego-rodriguez](https://www.diego-rodriguez.work/blog/glm-coding-model-2026-benchmarks-guide); [saascrmreview](https://saascrmreview.com/glm-review/)
- Claude Pro is $20/month ($17/month billed annually), and Max is $100 (5×) or $200 (20×). Opus 5 API pricing is $5/$25 per million tokens (batch $2.50/$12.50). Several blogs list Opus 5.5 at $4/$20 (released around Sept 22, 2026) and Sonnet at about $2 input. These come from third-party blogs and were not verified on anthropic.com. An unverified claim says Max includes $100/$200 in API credits since Oct 7, 2026. — [screenapp](https://screenapp.io/blog/claude-ai-pricing); [eesel](https://www.eesel.ai/blog/claude-opus-5-pricing); [metacto](https://www.metacto.com/blogs/anthropic-api-pricing-a-full-breakdown-of-costs-and-integration); [benchlm](https://benchlm.ai/anthropic/api-pricing); [sentra](https://www.sentra.app/articles/claude-api-pricing)
- One review frames the self-hosting trade-off as "local coding models want a great deal of unified memory", which is a real cost. — [airstreet](https://press.airstreet.com/p/poolsides-laguna)

### Inferences (my arithmetic, not sourced)
- **$2000 amortized:** about $55.6/month over 36 months, or $83/month over 24 months. Add electricity at roughly 300–450 W under load, a few hours a day: about $5–15/month at $0.15–0.25/kWh.
- **What $2000 buys:** roughly a 24 GB-class GPU PC, or a 32–64 GB Mac or unified-memory mini-PC. That realistically means the 24–32 GB tier (Qwen3.8-27B, Qwen3.6-35B-A3B) and maybe 64 GB (Qwen3-Coder-Next Q4). 128 GB machines (e.g. Strix Halo, M-series Max) usually cost more than $2000. Hardware prices were not researched here.
- **Token-equivalent:** $55/month buys about 90M output tokens (or around 350M input tokens) of DeepSeek V4.1-Flash off-peak, a model stronger than anything that fits in 64 GB. The same money buys about 2.75M Opus 5 output tokens, or just covers Claude Pro plus the GLM Lite plan.
- **Honest conclusion:** local is cost-competitive only for heavy, continuous use, for privacy, compliance or air-gapped needs, or if the hardware is already owned or doubles as a gaming or work machine. For pure quality per dollar, an $18–20/month plan or a cheap API wins. A hybrid works well: local for autocomplete, chat and sensitive code, with cloud Opus or GLM for hard agentic tasks.

### Gaps
- The official DeepSeek, Z.ai and Anthropic pricing pages were not reachable, so all prices are third-party and may be outdated.
- No hardware price data (GPU, Mac, Strix Halo, DGX Spark) was collected for October 2026.
- No measured tokens/sec on $2000-class hardware for the 27B dense models.
