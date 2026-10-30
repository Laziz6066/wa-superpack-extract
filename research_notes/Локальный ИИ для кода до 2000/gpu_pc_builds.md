# Discrete-GPU PC builds for local coding LLMs, ~$2000 USD budget (as of 30 Oct 2026)

Method note: research was done 30 Oct 2026 with web search plus a few page fetches. Several primary pages (insiderllm.com, runaihome.com, hardware-corner.net) could not be fetched from this sandbox (DNS blocked), so some figures come from search-result summaries of those pages. Most price figures come from price-tracker aggregators (bestvaluegpu, pcprice.watch, gpudojo, gpupoet, gpuprix), not first-hand retailer checks. Treat every price as approximate and volatile: the 2025–2026 memory shortage has pushed both GPU and RAM prices up sharply.

## 1. GPU candidates: current prices, VRAM, bandwidth, pros/cons

### Takeaway
Late-2026 prices are far above MSRP because of the DRAM/GDDR shortage. Used RTX 3090 24GB costs about $1,100–1,600 (sold median about $1,400). RTX 5060 Ti 16GB is about $800 and RTX 5070 Ti 16GB about $1,000–1,150. Intel Arc Pro B60 24GB is about $600–650, the cheapest new 24GB card. AMD Radeon AI PRO R9700 32GB is $1,300 MSRP and $1,300–1,700 street. Used RX 7900 XTX 24GB is about $825–1,200. The RTX 50 Super cards with more VRAM have NOT launched as of late Oct 2026. Used datacenter cards are cheapest per GB of VRAM but have software limits.

### Cited Findings
**Used RTX 3090 24GB (GDDR6X)**
- US eBay sold median about $1,408 (236 sold listings over 90 days). The cheapest listing shipping to the US is about $1,094 delivered. — [pcprice.watch](https://www.pcprice.watch/search/RTX3090/US/GPU)
- BestValueGPU lists $1,199 used (US eBay, checked about Oct 21, 2026) and about €1,409 in the EU (Oct 29). — [bestvaluegpu US](https://bestvaluegpu.com/history/new-and-used-rtx-3090-price-history-and-specs/); [bestvaluegpu EU](https://bestvaluegpu.com/en-eu/history/new-and-used-rtx-3090-price-history-and-specs/)
- GPUDojo lists used from about $1,300 on eBay US (Oct 30). Asking prices run near $1,800, so sold and asking prices differ widely. — [gpudojo](https://gpudojo.com/rtx-3090)
- ResalePrices gives a "fair asking range" of $1,497–1,603 (341 listings). — [resaleprices](https://resaleprices.com/gpu/nvidia-rtx-3090)
- InsiderLLM's buying guide (search snippet only) gives about $1,400–1,550 used and calls it the cheapest 24GB option for local LLMs. — [insiderllm](https://insiderllm.com/guides/used-rtx-3090-buying-guide/)
- September 2026 average about $1,242 (gpupoet). — [gpupoet Sept 2026](https://gpupoet.com/gpu/learn/price/september-2026/nvidia-geforce-rtx-3090)

**RTX 5060 Ti 16GB**
- US median price about $805 (Aug 2026), up from about $570 in June (+39% in two months). Launch MSRP was $429. — [DigitalCitizen](https://www.digitalcitizen.life/nvidia-rtx-5060-ti-16gb-median-price-reaches-805-as-rtx-50-series-costs-keep-rising/); [TweakTown](https://www.tweaktown.com/news/113088/geforce-rtx-5060-ti-16gb-pricing-hits-800-in-the-us-as-memory-crisis-takes-hold/index.html)
- Japan: cheapest about ¥137,800 (about $871), +26% in 30 days. — [Guru3D](https://www.guru3d.com/story/alert-geforce-rtx-5060-ti-16gb-reaches-at-japanese-retailer-up-in-30-days/)
- The 16GB SKUs are hit hardest because they use twice the memory chips of the 8GB models. ASUS said in Jan 2026 that it would stop production, then reversed; NVIDIA says it still ships all SKUs. — [Club386](https://www.club386.com/?p=130313); [Slashdot/Engadget](https://tech.slashdot.org/story/26/01/15/2126254)

**RTX 5070 Ti 16GB**
- Median about $1,099.99 (Aug 2026), flat over the period, versus $749 MSRP. — [DigitalCitizen](https://www.digitalcitizen.life/nvidia-rtx-5060-ti-16gb-median-price-reaches-805-as-rtx-50-series-costs-keep-rising/)
- PriceDropChecker (Jul 29, 2026): minimum about $1,009, average about $1,148. GPU Poet: July 2026 lowest average about $875; no October data recorded. — [gpupricehistory](https://gpupricehistory.com/us/rtx-5070-ti); [gpupoet Jul 2026](https://gpupoet.com/gpu/learn/price/july-2026/nvidia-geforce-rtx-5070-ti); [gpupoet Oct 2026](https://gpupoet.com/gpu/learn/price/october-2026/nvidia-geforce-rtx-5070-ti)

**RTX 50 Super (24GB 5070 Ti Super / 5080 Super; 18GB 5070 Super)**
- These cards are not released as of late Oct 2026. The launch slipped from Q1 to Q3 2026, and the latest rumors point to early 2027 because of the GDDR7 shortage. All of this is leak-based, with no NVIDIA announcement. — [Instant Gaming news](https://news.instant-gaming.com/en/articles/20052-the-rtx-50-super-series-may-finally-come-out-in-early-2027); [igor'sLAB](https://www.igorslab.de/en/nvidia-geforce-rtx-50-super-allegedly-postponed-to-q3-2026/); [Notebookcheck](https://www.notebookcheck.net/Nvidia-RTX-50-Super-series-launch-tipped-once-again-later-than-expected.1317926.0.html)

**RTX 4090 / 5090**
- No current price was gathered. Given used 3090s cost about $1,400, both are clearly far over a $2,000 *total* build budget (inference). An OLX.uz (Samarkand) listing titled "MSI SUPRIM X RTX 3090, 4090" was about 13.6M UZS (Aug 24, 2026); the model is ambiguous. — [OLX.uz](https://www.olx.uz/elektronika/q-rtx-4090-видеокарта/)

**Intel Arc Pro B60 24GB**
- First retail listing was $599 (ASRock, Central Computers). gpuprix shows a US low of about $650 (page updated Oct 3, 2026) and a 12-month low of $600. UK low about £753. — [Guru3D](https://www.guru3d.com/story/intel-arc-pro-b60-workstation-gpu-listed-at-with-24gb-memory); [gpuprix US](https://gpuprix.com/us/gpus/arc-pro-b60)
- No measured LLM tokens/s for the B60 was found in this pass (gap).

**AMD Radeon AI PRO R9700 32GB (GDDR6)**
- Launch price was $1,299 US. Street price is about $1,300 per ComputingForGeeks, but one tracker shows $1,700 (Oct 1, 2026). UK price £1,249.99–1,499.99. — [CGM](https://www.cgmagonline.com/news/amd-pricing-radeon-ai-pro-r9700/); [aiindigo](https://aiindigo.com/hardware/amd-radeon-ai-pro-r9700-32gb); [Scan UK](https://www.scan.co.uk/shops/amd-radeon-ai-pro)

**AMD RX 7900 XTX 24GB (used)**
- About $975 used on eBay (Oct 1, 2026), up from about $919 in early Aug. A verified used listing was $824.99 (Aug 1). GPUDojo shows about $1,200. — [aiindigo](https://aiindigo.com/hardware/amd-radeon-rx-7900-xtx-24gb); [videocardprices digest](https://videocardprices.com/digest/2026-08-01/); [gpudojo](https://gpudojo.com/rx-7900-xtx)

**Used datacenter cards**
- Tesla P40 24GB: eBay US median ask $385 (Oct 19, 2026), typical $360–420. Cheap listings sell within a day. — [gpudojo market note](https://gpudojo.com/market-notes/2026-10-19-p40-v100-cheap-end)
- Tesla V100 32GB: median ask $954 (Oct 19), typical $880–1,110. Another tracker had $694.99 on eBay (Oct 9). — [gpudojo market note](https://gpudojo.com/market-notes/2026-10-19-p40-v100-cheap-end); [gpupoet V100](https://gpupoet.com/gpu/learn/price/october-2026/nvidia-tesla-v100-32gb)
- Software limits: CUDA 13 can no longer build for the P40, P100 or V100, and vLLM refuses all three. — [gpudojo market note / computingforgeeks](https://computingforgeeks.com/best-used-datacenter-gpu-local-ai/)
- AMD MI50 32GB: price reports conflict. Some aggregators claim $120–250 / €220, but more careful guides say live eBay listings are about $580–630 (Aug 2026, unverified against sold prices) or $500–650 after the late-2025 surge. The card runs through llama.cpp Vulkan or a community gfx906 fork; AMD has dropped support. — [pasqualepillitteri](https://pasqualepillitteri.it/en/news/10761/used-server-gpu-local-llm-prices-europe); [openclawdc MI50](https://openclawdc.com/blog/amd-mi50-32gb-local-llm/); [aliteq](https://aliteq.com/amd-instinct-mi50-32gb-worth-it-local-ai-2026)

### Inferences
- Approximate memory bandwidth (manufacturer specs from background knowledge, not re-verified this pass): RTX 3090 about 936 GB/s; 4090 about 1,008; 5090 about 1,792; 5070 Ti about 896; 5060 Ti 16GB about 448; 4060 Ti 16GB about 288; Arc B580 12GB about 456; Arc Pro B60 about 456; RX 9070 XT 16GB about 640; 7900 XTX about 960; R9700 about 640; P40 about 347; V100 about 900; MI50 about 1,024. Decode speed for models that fit in VRAM scales roughly with bandwidth.
- Value ranking in late 2026 (VRAM per $): Arc Pro B60 (24GB, about $650) > P40 (24GB, about $385, slow/old) > 7900 XTX (24GB, about $975) > used 3090 (24GB, about $1,200–1,400) > R9700 (32GB, about $1,300+) > 5060 Ti (16GB, about $805) > 5070 Ti (16GB, about $1,100). For CUDA maturity and prompt-processing speed, the 3090 remains the safe default.
- The used 3090 has nearly doubled from typical 2024–2025 prices (about $700–800, background knowledge). It no longer leaves budget for much RAM in a $2,000 build.

### Gaps
- No current RTX 4060 Ti 16GB, RX 9070 XT, Arc B580 or Arc Pro B50 price was gathered.
- No measured Arc Pro B60 or dual-B60 LLM benchmarks were found.
- Uzbekistan retail prices (olx.uz, texnomart) were not reliably found. Only one ambiguous Samarkand listing (about 13.6M UZS, roughly $1,050–1,100 at about 12.5–13k UZS/USD, exchange rate not verified).

## 2. Multi-GPU (2× RTX 3090, 2× 5060 Ti) within $2000

### Takeaway
At late-2026 prices neither dual setup fits $2,000 total. Two used 3090s alone cost about $2,200–2,800, and two 5060 Ti 16GB cost about $1,600 before CPU, RAM and PSU. The only ≥32GB-VRAM options near budget are one R9700 32GB (about $1,300+), two Arc Pro B60s (about $1,200–1,300 for 48GB, immature software), or used datacenter cards (MI50/P40/V100) with their software caveats.

### Cited Findings
- 3090 sold median about $1,408; cheapest about $1,094 delivered → two cards cost about $2,200–2,800. — [pcprice.watch](https://www.pcprice.watch/search/RTX3090/US/GPU)
- 5060 Ti 16GB median about $805 → two cards cost about $1,610. — [DigitalCitizen](https://www.digitalcitizen.life/nvidia-rtx-5060-ti-16gb-median-price-reaches-805-as-rtx-50-series-costs-keep-rising/)
- Arc Pro B60 about $600–650 each. — [gpuprix](https://gpuprix.com/us/gpus/arc-pro-b60)
- P40 about $385 each (two P40s = 48GB for about $770, but Pascal is old, slow, and CUDA 13 dropped it). — [gpudojo](https://gpudojo.com/market-notes/2026-10-19-p40-v100-cheap-end)

### Inferences
- With llama.cpp layer split, dual-GPU decode speed is roughly that of one card on a model twice the size; it pools VRAM, not bandwidth. Tensor parallelism (vLLM) would help, but vLLM refuses P40/V100.
- Dual 3090 needs a 1000–1200W PSU and a board with two x8/x16 slots (from background knowledge), adding cost.

### Gaps
- No measured 2×5060 Ti or 2×B60 coding-model benchmarks were found in this pass.

## 3. Hybrid CPU+GPU offload of MoE models (--n-cpu-moe) and the DRAM price spike

### Takeaway
Hybrid MoE offload works well technically. One 24GB GPU plus system RAM runs gpt-oss-120b at about 15 tok/s generation even on DDR4, and DDR5 should be somewhat faster. But the 2025–2026 DRAM spike is a budget killer: 64GB DDR5 now costs about $880–1,120 (versus about $190 in mid-2025) and 128GB about $3,400. So a "16–24GB GPU + 64–128GB DDR5" build cannot fit $2,000 in late 2026 unless the RAM is reused or bought used.

### Cited Findings
- **gpt-oss-120b, RTX 3090 + 64GB DDR4-3200, `--n-cpu-moe 24`, -ngl 99, 32k context, flash-attn:** about 15 tok/s generation, about 50 tok/s prompt processing. Nearly filled VRAM and RAM; `--n-cpu-moe 26` suggested for headroom. This is one user report via a bookmark aggregator. — [scuttle.klotz.me](https://scuttle.klotz.me/tags/rtx%203090+120b)
- **gpt-oss-120b, RTX 5090 32GB, `--n-cpu-moe 21`:** about 30 tok/s at zero context (RAM type not stated). — [llama.cpp discussion #15396](https://github.com/ggml-org/llama.cpp/discussions/15396)
- **Offload penalty example (gpt-oss-20b, RX 7900 XT 20GB, 32GB DDR4-3200):** full GPU 94 tok/s; 4 MoE layers on CPU 60; 8 layers 38; 16 layers 25–27; all MoE on CPU about 20 tok/s. — [llama.cpp discussion #15396](https://github.com/ggml-org/llama.cpp/discussions/15396)
- RTX 3060 12GB + 32GB RAM, gpt-oss-20b with partial expert offload: about 31 tok/s. — [llama.cpp discussion #15396](https://github.com/ggml-org/llama.cpp/discussions/15396)
- **DRAM prices:**
  - A 64GB DDR5-5600 kit went from $191 to $1,118 (+485%) between Aug 2025 and Aug 2026. — [Tom's Hardware RAM price index](https://tomshardware.com/pc-components/ram/ram-price-index-2026-lowest-price-on-ddr5-and-ddr4-memory-of-all-capacities)
  - Lowest 64GB DDR5-6000 is about $989 (Oct 2026); cheapest 64GB kit about $880 (Sept 2026). — per search summary of [datacenterdisk](https://datacenterdisk.com/ram/ddr5/64gb) and [gamegpu](https://en.gamegpu.com/news/zhelezo/tseny-na-ddr5-vzleteli-za-18-mesyatsev-na-500-i-prevysili-usd1250-za-64-gb)
  - 32GB DDR5 kits reach about $450. — [DigitalCitizen](https://www.digitalcitizen.life/ddr5-ram-prices-surge-in-2026-as-32gb-kits-reach-450-amid-global-memory-shortage/)
  - A 128GB DDR5 kit went from $329 to $3,399. — [HWBusters](https://hwbusters.com/?p=111430)
  - German DDR5 index is at 486% of the July 2025 level (Aug 2026). — [Guru3D](https://www.guru3d.com/story/german-ddr5-prices-approach-five-times-their-july-2025-level/); [TrendForce](https://www.trendforce.com/news/2026/08/17/news-germany-ddr5-prices-near-5x-yoy-in-august-china-reportedly-sees-14-wow-jump-as-global-rally-continues/)
  - Prices are reportedly stabilizing at high levels. TrendForce forecast +13–18% QoQ contract increases (Jul 2026). — [TechRadar](https://www.techradar.com/pro/good-news-ram-prices-seem-to-have-finally-stabilized-bad-news-its-probably-because-memory-prices-are-so-high-that-its-forcing-most-of-us-to-give-up-buying-anything)

### Inferences
- Qwen3-Coder-30B-A3B (about 18.6GB at Q4_K_M) fits fully on a 24GB card. On a 16GB card a few expert layers spill to RAM, and 32GB system RAM suffices. The spill penalty is moderate (see the 7900 XT scaling above): expect roughly 40–70 tok/s on a 5060 Ti with light offload. This is an estimate, not measured.
- gpt-oss-120b (about 63GB MXFP4) needs at least 64GB RAM plus 16–24GB VRAM. GLM-4.5-Air (about 106B total / 12B active, about 60–70GB at Q4) needs a similar footprint and has more active params, so it is slower than gpt-oss-120b. Expect roughly 8–15 tok/s generation on a single 3090 plus dual-channel DDR5 (inference from the figures above). Prompt processing in hybrid mode is slow (about 50 tok/s reported on DDR4 with a 3090), which hurts agentic coding with large contexts.
- The DRAM spike also hits unified-memory mini PCs (their RAM is soldered LPDDR5X). Compare current mini PC prices, not 2025 prices.
- An unverified LocalClaw page claims GLM-4.5-Air Q4_K_M is "~9GB". That is wrong for the 106B model and was excluded. — [localclaw](https://localclaw.io/models/glm4.5-air)

### Gaps
- No verified DDR5-based --n-cpu-moe benchmark for Qwen3-Coder-30B-A3B, gpt-oss-120b or GLM-4.5-Air on a 16GB card was found. ktransformers numbers were not found.

## 4. Measured tokens/s on these GPUs (coding-relevant models)

### Takeaway
For MoE coding models that fit in VRAM, consumer GPUs are 2–5× faster than unified-memory mini PCs at generation and much faster at prompt processing.
- gpt-oss-20b generation (tg128, llama.cpp): RTX 5060 Ti about 112 tok/s, 3090 about 162, 5070 Ti about 189, 4090 about 222, 5090 about 282.
- R9700 32GB: about 127–156 tok/s on a 35B-A3B MoE, but prompt processing is 2.6–3.4× slower than NVIDIA.

### Cited Findings
- **llama.cpp gpt-oss-20b tg128, full GPU:** 3090 about 162; 4090 about 222–225; 4080 Super about 186; 5060 Ti about 112; 5070 Ti about 189; 5080 about 205; 5090 about 282 tok/s. — [llama.cpp discussion #15396](https://github.com/ggml-org/llama.cpp/discussions/15396)
- **RTX 5060 Ti 16GB (Hardware Corner, March 2026):**
  - gpt-oss-20b MXFP4 generation: about 92 tok/s at 4k context, 73 at 32k, 44 at 128k (fits at 128k context).
  - Qwen3 14B prompt processing about 943 tok/s at 4k.
  - Source: per search summary, page not fetched. — [hardware-corner](https://www.hardware-corner.net/gpu-llm-benchmarks/rtx-5060-ti-16gb/)
- **R9700 32GB:**
  - Qwen3.5-35B-A3B Q4 decode about 127–156 tok/s; Qwen3.5-27B dense Q4 about 29–33 tok/s; prompt processing 2.6–3.4× slower than NVIDIA. — [RunAIHome](https://runaihome.com/blog/amd-radeon-ai-pro-r9700-local-ai-hardware-guide-2026/) (search summary)
  - Qwen3 32B Q4_K_M about 25 tok/s. — [LocalAIMaster](https://localaimaster.com/blog/radeon-ai-pro-r9700-local-ai)
  - Vulkan is faster than ROCm (Llama 2 7B Q4_0 about 153 vs 98 tok/s). — [OpenClaw DC](https://openclawdc.com/blog/best-local-llm-r9700/)
- **MI50 32GB:**
  - Llama-7B Q4_0 about 1,200–1,300 tok/s prompt processing and about 100–110 tok/s generation (hobbyist). — [wtarreau blog via scour](https://scour.ing/@matmat/p/http://wtarreau.blogspot.com/2025/12/amd-radeon-instinct-mi50-32gb-best-ai.html)
  - Qwen3-30B-A3B about 73 tok/s (secondhand figure). — [localaimaster MI50](https://localaimaster.com/blog/amd-mi50-local-llm)
- **Qwen3-Coder-30B-A3B on RTX 5090:** about 241 tok/s at 1k (versus 43.8 on GB10 / DGX Spark-class). — [HF dataset](https://huggingface.co/datasets/mreltera/qwen3-coder-gb10-vs-rtx5090-benchmark)
- The "~99 tok/s Qwen3-30B-A3B on 3090" figure from willitrunai is a calculator estimate, not a measurement. — [willitrunai](https://willitrunai.com/de/can-run/qwen-3-30b-a3b-on-rtx-3090-24gb)

### Inferences
- Since gpt-oss-20b and Qwen3-Coder-30B-A3B both have about 3–4B active params, expect Qwen3-Coder-30B-A3B Q4 on a 3090 at roughly 120–160 tok/s and on a 7900 XTX roughly 100–130 tok/s. On a 5060 Ti (light spill) expect roughly 50–80 tok/s. These are inferences, not measured.
- Dense 32B coders (Qwen2.5-Coder-32B class) at Q4 run about 30–35 tok/s on a 3090 (background knowledge, consistent with the R9700's 25–33 tok/s above). They do not fit on 16GB cards.

### Gaps
- Arc Pro B60, 7900 XTX, P40 and V100 coding-model benchmarks were not gathered. localscore.ai was not checked.

## 5. Example builds (~$2000) and upgradeability / power / noise vs mini PCs

### Takeaway
At late-2026 prices, $2,000 buys about 16–24GB VRAM plus only 32GB system RAM. Big-MoE hybrid builds (64GB+ RAM) push the total to about $2,400–2,700+. Component prices other than the GPU and RAM are estimates (not verified this pass) and are marked "~est".

### Cited Findings (price inputs)
- GPU and RAM prices as cited in sections 1 and 3. DDR5 32GB is about $450 ([DigitalCitizen](https://www.digitalcitizen.life/ddr5-ram-prices-surge-in-2026-as-32gb-kits-reach-450-amid-global-memory-shortage/)) and 64GB about $880–1,118 ([Tom's Hardware](https://tomshardware.com/pc-components/ram/ram-price-index-2026-lowest-price-on-ddr5-and-ddr4-memory-of-all-capacities)).
- AI demand has also pushed NAND (SSD) prices up. Memory makers pre-sold 2026 NAND/DRAM output to AI customers. — [tech-insider CA](https://tech-insider.org/ca/ram-ddr5-ssd-price-shortage-canada-2026/)

### Example builds (CPU, motherboard, PSU, SSD and case prices are ~est, unverified)

**Build A — "Used 3090 coder box" (best all-round, about $2,100–2,300)**
- Used RTX 3090 24GB: $1,100–1,400 (cited)
- 32GB DDR5 (2×16): about $450 (cited)
- Ryzen 5 7600 / B650 board: ~est $300
- 850–1000W PSU: ~est $120
- 1TB NVMe: ~est $100–150
- Case: ~est $70
- Runs Qwen3-Coder-30B-A3B Q4 fully in VRAM with long context, and dense 32B Q4.
- Cannot run gpt-oss-120b / GLM-4.5-Air without 64GB+ RAM (+$500–650 more).
- Saving tip: buy a used AM4 system with DDR4, which is cheaper (DDR4 prices not verified).

**Build B — "New 16GB budget" (about $1,700–1,900)**
- RTX 5060 Ti 16GB: about $805 (cited)
- 32GB DDR5: about $450
- Rest: ~est $550
- gpt-oss-20b at about 92–112 tok/s. Qwen3-Coder-30B-A3B with slight offload.
- Lowest power (about 180W GPU board power, background knowledge) and quiet.

**Build C — "Cheap new 24GB" (about $1,550–1,700)**
- Arc Pro B60 24GB: about $600–650 (cited)
- 32GB DDR5 + rest: about $1,000
- 24GB at the lowest new price. But Intel software (SYCL/Vulkan/IPEX-LLM) is less mature, and no measured tok/s was found. A second B60 later gives 48GB.

**Build D — "32GB VRAM" (about $2,100–2,500, over budget)**
- Radeon AI PRO R9700 32GB: $1,300–1,700 (cited)
- 32GB DDR5 + rest: about $1,000
- MoE coders at 127–156 tok/s and dense 27–32B at 25–33 tok/s, but weak prompt processing. Blower cooler (loud), ROCm/Vulkan.

**Build E — "Hybrid MoE" (about $2,600–2,900, clearly over budget)**
- RTX 5060 Ti 16GB or used 3090 + 64GB DDR5 ($880–1,118)
- gpt-oss-120b at about 15+ tok/s generation.
- Only viable on budget if the buyer already owns 64GB RAM or finds used DIMMs.

**Wildcard — used datacenter card**
- e.g. a used PC + MI50 32GB ($500–650) or 2× P40 (about $770). Cheapest VRAM, but passive cooling needs a fan shroud (loud), old architectures, and dropped vendor support (CUDA 13 / vLLM exclude P40 and V100).

### Inferences
- **Upgradeability:** A tower can add a second GPU, more RAM when prices fall, and swap GPUs when the RTX 50 Super (24GB) eventually ships (rumored early 2027). Mini PCs with soldered memory cannot be upgraded.
- **Power and noise** (background knowledge, not cited):
  - A 3090 draws about 350W under load (can be power-limited to about 250–280W with little LLM speed loss), and the system draws about 450–500W.
  - A 5060 Ti system draws about 250W.
  - Strix Halo-class mini PCs draw about 120–150W and are much quieter.
  - Tower GPUs are noisier under sustained load, but LLM inference is bursty.
- **Versus a unified-memory mini PC (128GB):** the GPU PC wins on generation speed for models that fit in VRAM (e.g. 3090 about 162 vs GB10 about 44 tok/s class figures above) and by a large margin on prompt processing. The mini PC wins on capacity for 100B+ MoE models (gpt-oss-120b, GLM-4.5-Air) at a similar price, given the current DRAM prices.
- **Uzbekistan/CIS:**
  - New NVIDIA/AMD cards are generally available via local retailers and olx.uz, but typically at a premium.
  - Workstation cards (Arc Pro B60, R9700) and datacenter cards would likely need import (AliExpress/eBay forwarding), with customs costs.
  - The used 3090 market exists on olx.uz (one ambiguous listing around 13.6M UZS). Not verified.

### Gaps
- No verified CPU, motherboard, PSU or SSD prices for Oct 2026.
- No PCPartPicker build snapshots.
- No measured power or noise figures were gathered.
- Uzbekistan retail pricing was not verified.
