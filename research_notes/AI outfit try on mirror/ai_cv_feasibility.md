# AI and Computer-Vision Feasibility of a Home Try-On Smart Mirror (as of October 2026)

How these notes were made (16 Oct 2026): licenses, VRAM and speed figures come mainly from the primary LICENSE/README/doc files in each project's GitHub repo, and from the MediaPipe model cards on storage.googleapis.com, all read directly. Cloud GPU prices come from SkyPilot's auto-generated price catalogs on GitHub. API prices and the newest 2026 papers come from a small number of web searches. The shared web-search budget ran out partway through. Most vendor sites (fal.ai, fashn.ai, arxiv.org, huggingface.co, runpod.io, e2enetworks.com) could not be fetched from this environment. As a result, several API, latency and video-model numbers are listed under Gaps rather than guessed.

---

## 1. Real-time approaches: 2D garment warping, 3D body + 3D garment simulation, and AR lenses. What quality and latency do they reach, and what does each garment need?

### Takeaway
Real-time (≥30 fps) try-on on live video is possible today only with non-generative methods:
- **2D warping networks.** Distilled flow-based models run at about 40 fps on a datacenter T4, but only at low resolution and with visible artifacts. The fastest open one, DM-VTON, is non-commercial.
- **Snap's Garment Transfer.** This is a shipping real-time feature driven by a single 2D garment image, but it covers upper-body garments only.
- **3D body + 3D garment simulation.** This gives the most stable, pose-following result, but each garment needs a simulation-ready 3D asset, which is impractical for a personal wardrobe.

On the 3D route, the standard SMPL/SMPL-X body model is non-commercial, while Meta's newer MHR body model is Apache-2.0.

### Cited Findings
- **DM-VTON (2D warping).** DM-VTON ("Distilled Mobile Real-time Virtual Try-On") "can achieve 40 frames per second on a single Nvidia Tesla T4 GPU and only take up 37 MB of memory" — [DM-VTON README](https://github.com/KiseKloset/DM-VTON)
- **DM-VTON vs other 2D warping models.** On the VITON benchmark DM-VTON reports 23.3 ms runtime, 37.8 MB memory and FID 28.2. For comparison: PF-AFN 35.8 ms (FID 27.3), FS-VTON 37.5 ms (FID 26.5), ACGPN 153.6 ms (FID 33.3). All of these are 2-stage warping + generator, parser-free models — [DM-VTON README](https://github.com/KiseKloset/DM-VTON)
- **DM-VTON license.** CC BY-NC-SA 4.0: "The use of this code is for academic purposes only." **NON-COMMERCIAL** — [DM-VTON README](https://github.com/KiseKloset/DM-VTON)
- **Snap Garment Transfer (AR lens).** A Lens Studio template/custom component that takes an image of an upper-body garment (static or animated) and transfers it to a live video output. It includes a carousel to switch between reference images — [Snap Lens Studio docs](https://developers.snap.com/lens-studio/features/try-on/garment-transfer)
- **Garment Transfer categories and history.** Lens Studio 4.34 notes say it renders upper garments (T-shirts, hoodies, jackets) onto a body from a single 2D image. Later docs add coats and hoodies. Snap says it released this patented solution in 2022 — [Lens Studio 4.34](https://ar.snap.com/lens-studio-4.34); [Snap blog, July 2024](https://ar.snap.com/blog/lens-studio-5.0.17)
- **Garment Transfer patent.** The underlying patent is "Real-time upper-body garment exchange" (US11880947B2, assigned to Snap Inc.). It covers segmenting the upper-body garment and swapping its pixels into a target video while keeping the person's motion — [Google Patents](https://patents.google.com/patent/US11880947)
- **SMPL-X license.** SMPL-X/SMPLify-X are licensed "for non-commercial scientific research purposes". "Any other use, in particular any use for commercial ... purposes is prohibited. This includes ... incorporation in a commercial product, use in a commercial service". Commercial licensing is via ps-license@tue.mpg.de. **NON-COMMERCIAL by default** — [smplx LICENSE](https://github.com/vchoutas/smplx/blob/main/LICENSE)
- **Meta MHR body model.** Meta's MHR (Momentum Human Rig) body model is Apache-2.0 and ships tools to convert between MHR and SMPL/SMPL-X — [MHR repo](https://github.com/facebookresearch/MHR)
- **SAM 3D Body.** Meta's SAM 3D Body is "a promptable model for single-image full-body 3D human mesh recovery" that uses MHR assets. It is released under the SAM License (dated 19 Nov 2025). That license grants a "royalty-free limited license ... to use, reproduce, distribute, copy, create derivative works", with restrictions on trade controls, ITAR/military uses and reverse engineering — [SAM 3D Body README](https://github.com/facebookresearch/sam-3d-body); [SAM License](https://github.com/facebookresearch/sam-3d-body/blob/main/LICENSE)
- **MediaPipe BlazePose GHUM.** Predicts 33 3D landmarks plus a background segmentation mask on the whole body from RGB. This is usable as a real-time skeleton for driving a 2D or 3D overlay — [MediaPipe Pose docs](https://github.com/google-ai-edge/mediapipe/blob/master/docs/solutions/pose.md)

### Inferences
- **Per-garment assets by approach:**
  - 2D warping (DM-VTON class) and Snap Garment Transfer need **one 2D garment image** per item. This fits a "photograph your wardrobe" workflow.
  - 3D simulation needs a **simulation-ready 3D garment** (sewing pattern + fabric parameters, e.g. authored in CLO3D/Marvelous Designer) per item. Expect hours of skilled work per garment. That is viable for a retailer's catalogue (the FXMirror-style model) but not for a consumer's own clothes.
- **Quality ranking for live video:**
  - 3D sim: most temporally stable and follows the body well, but looks "game-like" and misfits real-world garment detail unless the asset is excellent.
  - 2D warping: photo texture, but jitter, low resolution, and breaks on side/back views, arms crossing and occlusion.
  - None of the real-time options approach diffusion-level photorealism.
- **Most realistic live path.** A 2D-warp or segmentation-based overlay driven by pose + clothing segmentation (see Q6). For commercial use, the open real-time warping models would need retraining under a commercial license. Snap's tech is only reachable through Snap's own apps/Camera Kit terms.
- **3D body licensing.** If a 3D body is used, MHR (Apache-2.0) avoids the SMPL-X licensing problem. SAM 3D Body's license appears to allow commercial use but should get legal review.

### Gaps
- No verifiable source was retrieved for FXMirror's (FXGear) current hardware, sensor (depth camera), latency or per-garment asset pipeline. Search budget ran out. Its use of pre-built 3D garments and depth sensing is common knowledge but unverified here.
- No measured fps for SAM 3D Body, or for any real-time SMPL-X/MHR regressor on edge hardware, was found.
- No published glass-to-glass latency was found for Snap Garment Transfer or for any commercial 3D mirror.
- Device requirements for Garment Transfer and Camera Kit availability on non-phone hardware (e.g., a mirror PC) were not confirmed.

---

## 2. Image-based generative virtual try-on (single photo): licenses, VRAM, seconds per image, quality

### Takeaway
Almost every well-known open research VTON model is **non-commercial**: CC BY-NC-SA 4.0 for IDM-VTON, OOTDiffusion, CatVTON, StableVITON and FitDiT, and the FLUX.1-dev non-commercial weights license for OmniTry, Any2AnyTryon and CatVTON-FLUX. The open-weight options that are commercial-friendly are:
- **FASHN VTON v1.5** (2026, Apache-2.0). Its bundled human parser is under NVIDIA's non-commercial SegFormer license and must be swapped out.
- **Leffa** (MIT code).
- **General multi-reference editors** that would need try-on fine-tuning: FLUX.2 [klein] 4B and Qwen-Image-Edit, both Apache-2.0.

Typical inference cost is seconds per image on a datacenter GPU (Leffa: about 6 s on an A100) with 8–40+ GB VRAM.

### Cited Findings
- **IDM-VTON.** "The codes and checkpoints in this repository are under the CC BY-NC-SA 4.0 license." **NON-COMMERCIAL** — [IDM-VTON README](https://github.com/yisol/IDM-VTON)
- **OOTDiffusion.** The LICENSE file is Creative Commons Attribution-NonCommercial-ShareAlike 4.0. **NON-COMMERCIAL** — [OOTDiffusion LICENSE](https://github.com/levihsu/OOTDiffusion/blob/main/LICENSE)
- **CatVTON license.** "All the materials, including code, checkpoints, and demo, are made available under the Creative Commons BY-NC-SA 4.0 license." **NON-COMMERCIAL** — [CatVTON README](https://github.com/Zheng-Chong/CatVTON)
- **CatVTON size and VRAM.** 899.06M parameters in total, 49.57M trainable. "When using bf16 precision, generating results with a resolution of 1024x768 only requires about 8G VRAM" — [CatVTON README](https://github.com/Zheng-Chong/CatVTON)
- **StableVITON.** "Licensed under the CC BY-NC-SA 4.0 license." **NON-COMMERCIAL** — [StableVITON README](https://github.com/rlawjdghek/StableVITON)
- **Leffa license.** The code is MIT-licensed (LICENSE: "MIT License, Copyright (c) 2024 Zijian Zhou") — [Leffa LICENSE](https://github.com/franciszzj/Leffa/blob/main/LICENSE)
- **Leffa speed.** "09/Jan/2025. Inference defaults to float16, generating an image in 6 seconds (on A100)". A 2 Jan 2025 update added "ref unet acceleration, boosting prediction speed by 30%" — [Leffa README](https://github.com/franciszzj/Leffa)
- **FitDiT license.** CC BY-NC-SA 4.0. "This model can only be used for non-commercial use. For commercial use, please visit Tencent Cloud." **NON-COMMERCIAL** — [FitDiT README](https://github.com/BoyuanJiang/FitDiT)
- **FitDiT pipeline.** Two steps: mask generation, then try-on in the mask. It is SD3-based (`gradio_sd3.py`), with modes for bf16 without offload ("fastest inference and most memory"), fp16 + CPU offload, and aggressive offload ("slowest inference and less memory"). The default online-demo resolution is 1152x1536 — [FitDiT README](https://github.com/BoyuanJiang/FitDiT)
- **OmniTry license.** The code is Apache-2.0 (LICENSE file), but the README requires downloading FLUX.1-Fill-dev weights — [OmniTry LICENSE](https://github.com/Kunbyte-AI/OmniTry/blob/main/LICENSE); [OmniTry README](https://github.com/Kunbyte-AI/OmniTry)
- **OmniTry VRAM.** "OmniTry requires at least 28GB of VRAM for inference under torch.bfloat16." The model is mask-free ("Virtual Try-On Anything without Masks") — [OmniTry README](https://github.com/Kunbyte-AI/OmniTry)
- **FLUX.1 [dev]-family license.** FLUX.1 [dev], Fill [dev], Kontext [dev], Redux [dev], etc. are under the "FLUX.1-dev Non-Commercial License". FLUX.1 [schnell] and the autoencoder are Apache-2.0 — [BFL flux README](https://github.com/black-forest-labs/flux)
- **FLUX.1-dev license terms.** "Non-Commercial Use Only. You may only access, use, Distribute, or create Derivatives of the FLUX.1 [dev] Model or Derivatives for Non-Commercial Purposes." Outputs themselves may be used for any purpose — [LICENSE-FLUX1-dev](https://github.com/black-forest-labs/flux/blob/main/model_licenses/LICENSE-FLUX1-dev)
- **Any2AnyTryon.** Ships LoRAs for FLUX.1-dev (test script uses `black-forest-labs/FLUX.1-dev`) and offers a `--group_offloading` option to save memory. No LICENSE file was found in the repo (checked LICENSE/LICENSE.md/LICENSE.txt on main and master) — [Any2AnyTryon README](https://github.com/logn-2024/Any2anyTryon)
- **CatVTON-FLUX (community).** Code is MIT, but "the model weights have the same license as Flux.1 Fill and VITON-HD". It needs "VRAM >= 40GB" — [catvton-flux README](https://github.com/nftblackmagic/catvton-flux)
- **FASHN VTON v1.5 overview.** Apache-2.0. "Efficient Maskless Virtual Try-On in Pixel Space". It "supports both model photos and flat-lay product shots as garment inputs", with categories tops / bottoms / one-pieces. Weights are about 2 GB in total and run in bf16 on Ampere+ GPUs (RTX 30xx/40xx, A100, H100) — [FASHN VTON v1.5 README](https://github.com/fashn-AI/fashn-vton-1.5)
- **FASHN VTON v1.5 dependencies.** Third-party components are DWPose (Apache-2.0), YOLOX (Apache-2.0) and fashn-human-parser — [FASHN VTON v1.5 README](https://github.com/fashn-AI/fashn-vton-1.5)
- **fashn-human-parser.** It is SegFormer-B4 (18 classes) and "inherits the NVIDIA Source Code License for SegFormer" — [fashn-human-parser README](https://github.com/fashn-AI/fashn-human-parser)
- **NVIDIA SegFormer license.** "non-commercially' means for research or evaluation purposes only" — [NVlabs SegFormer LICENSE](https://github.com/NVlabs/SegFormer/blob/master/LICENSE)
- **FastFit (2025).** Multi-reference try-on (tops, bottoms, dresses, shoes, bags in one pass) using cacheable reference KV for speed. Weights and code are under the "FastFit Non-Commercial License"; commercial use goes through LavieAI. **NON-COMMERCIAL** — [FastFit README](https://github.com/Zheng-Chong/FastFit)
- **Kolors / Kolors Virtual Try-On.** A Kolors-Virtual-Try-On demo was released on 1 Sep 2024 as a Hugging Face Space. Kolors base weights are "fully open for academic research"; commercial use requires a registration questionnaire. Code is Apache-2.0 — [Kolors README](https://github.com/Kwai-Kolors/Kolors)
- **FLUX.2 (Black Forest Labs).**
  - Licenses: FLUX.2 [klein] 4B (released 15 Jan 2026) is **Apache-2.0**. Klein 9B and FLUX.2 [dev] (32B, 25 Nov 2025) are under the FLUX Non-Commercial License.
  - Klein capabilities: single- and multi-reference image editing, "sub-second inference ... on modern hardware", and "Klein 4B fits in ~8GB VRAM (RTX 3090/4070 and up)".
  - Source: [FLUX.2 README](https://github.com/black-forest-labs/flux2)
- **Qwen-Image.** Apache-2.0. Qwen-Image-Edit-2509 (Sep 2025) and Qwen-Image-Edit-2511 (23 Dec 2025) support multiple image inputs and improved consistency — [Qwen-Image README](https://github.com/QwenLM/Qwen-Image); [Qwen-Image LICENSE](https://github.com/QwenLM/Qwen-Image/blob/main/LICENSE)

### Inferences
- **Commercially usable today (license-wise):**
  - FASHN VTON v1.5 weights, after replacing the SegFormer-based parser with a commercially licensed one, e.g. MediaPipe multiclass segmentation (Apache-2.0, see Q6).
  - Leffa (MIT code; the weights license on HF was not verified).
  - In-house fine-tunes (LoRA) of FLUX.2 [klein] 4B or Qwen-Image-Edit, both Apache-2.0.
- **Everything else needs a commercial license.** IDM-VTON, OOTDiffusion, CatVTON, StableVITON, FitDiT, FastFit, DM-VTON, and anything built on FLUX.1-dev/Fill/Kontext (OmniTry, Any2AnyTryon, CatVTON-FLUX) would require a negotiated license (e.g., Tencent Cloud for FitDiT, LavieAI for FastFit, BFL for FLUX.1-dev).
- **Hardware tiers:**
  - CatVTON-class (SD1.5-inpainting-sized, about 8 GB) and FLUX.2 klein 4B (about 8 GB) fit a 16–24 GB consumer or L4-class GPU.
  - FLUX.1-based models (OmniTry ≥28 GB, CatVTON-FLUX ≥40 GB) need 40–80 GB cards (A100/H100/L40S) or slow offloading.
- **Speed.** Expect roughly 5–20 s per image on a single datacenter GPU for 25–30-step diffusion VTON at about 1024x768. The anchor point is Leffa's 6 s on an A100. A dedicated edge box (Jetson Orin Nano Super, 8 GB shared memory) is not realistic for these models.

### Gaps
- No primary-source per-image timings or VRAM figures were found for IDM-VTON, OOTDiffusion, StableVITON, FitDiT, OmniTry, Any2AnyTryon or FASHN VTON v1.5. Their READMEs do not state them, and arXiv/HF could not be fetched.
- Hugging Face model-card licenses (e.g., Leffa weights, FashionCLIP weights) could not be read because huggingface.co was blocked from this environment.
- No verified information was retrieved on Google's own image try-on model internals or on try-on fine-tunes of FLUX/Qwen ("Nano Banana"-style editing used for try-on). Quality comparisons (FID/KID on VITON-HD/DressCode) across models were not compiled.

---

## 3. Video try-on models, and whether anything approaches real time on live video

### Takeaway
Offline video try-on (CatV2TON, MagicTryOn, built on large video DiTs such as Wan2.1-14B) is high quality but far from real time, and the open models are CC BY-NC-SA. The first claimed real-time video try-on, **LiveVVT (arXiv, 28 Aug 2026), reports 22.39 fps**, but its hardware and resolution were not verifiable.

Generic streaming video diffusion is real time only on large GPU clusters, and these pipelines restyle by prompt; they do not faithfully transfer a specific garment:
- StreamDiffusionV2: 58–64 fps on 4×H100, first frame in about 0.5 s.
- MotionStream: 17 fps at 480p on 1×H100.

### Cited Findings
- **CatV2TON.** A DiT-based method "for Vision-Based Virtual Try-On (V2TON) with Temporal Concatenation of Video Frames and Garment Condition". 256 and 512 weights were released on 24 Feb 2025; it is evaluated on the ViViD-S and VVT test sets. License CC BY-NC-SA 4.0. **NON-COMMERCIAL** — [CatV2TON README](https://github.com/Zheng-Chong/CatV2TON)
- **MagicTryOn model and releases.** "Adopts Wan2.1 diffusion Transformer as the backbone" with full spatiotemporal self-attention. Releases: 14B weights (Jun 2025), MagicTryOn-1.3B (26 Dec 2025) and MagicTryOn-Turbo (19 Apr 2026; inference config `wan_bidirectional_dmd_from_scratch`, i.e., distilled) — [MagicTryOn README](https://github.com/vivoCameraResearch/Magic-TryOn)
- **MagicTryOn license and data.** "All the materials, including code, checkpoints, and demo" are CC BY-NC-SA 4.0. **NON-COMMERCIAL**. It is trained on VITON-HD, DressCode and ViViD, and the authors invite in-the-wild training "to better support real-world virtual try-on scenarios" — [MagicTryOn README](https://github.com/vivoCameraResearch/Magic-TryOn)
- **MagicTryOn preprocessing.** Custom-video try-on needs offline per-frame preprocessing: frame extraction, agnostic masks, agnostic person representation, DensePose, then re-encoding to mask.mp4/agnostic.mp4/densepose.mp4 — [MagicTryOn README](https://github.com/vivoCameraResearch/Magic-TryOn)
- **LiveVVT ("High-Fidelity Video Virtual Try-On in Real Time", arXiv 2608.26714, submitted 28 Aug 2026).**
  - Throughput: reports 22.39 fps.
  - Latency and throughput vs baselines: "over 26×" lower latency than current SOTA, and about 11× higher throughput than similarly sized models.
  - Design: a rolling streaming design; MagicTryOn is the main baseline.
  - Hardware and resolution were not visible in the search result — [alphaXiv listing](https://www.alphaxiv.org/abs/2608.26714); [aimodels.fyi summary](https://www.aimodels.fyi/papers/arxiv/livevvt-high-fidelity-video-virtual-try-real)
- **Other 2025–26 video try-on work.** Eevee (close-up high-resolution video try-on, arXiv 2511.18957), TripVVT (large triplet dataset and coarse-mask baseline for in-the-wild video try-on, arXiv 2604.27958) and RealVVT (arXiv 2501.08682). None of their real-time figures were surfaced — [Eevee](https://arxiv.org/pdf/2511.18957); [TripVVT](https://arxiv.org/pdf/2604.27958); [RealVVT](https://arxiv.org/pdf/2501.08682)
- **StreamDiffusion (v1, Apache-2.0).** On an RTX 4090 + Core i9-13900K:
  - SD-turbo, 1 step: 93.9 fps img2img (106.2 fps txt2img).
  - LCM-LoRA + KohakuV2, 4 steps: 37.1 fps img2img.
  - It includes a real-time img2img webcam demo — [StreamDiffusion README](https://github.com/cumulo-autumn/StreamDiffusion)
- **StreamDiffusionV2 (Apache-2.0; MLSys 2026 Best Paper).** "Without TensorRT or quantization, StreamDiffusionV2 renders the first frame within 0.5s and attains 58.28 FPS with a 14B-parameter model and 64.52 FPS with a 1.3B-parameter model on four H100 GPUs". With more denoising steps it gives 31.62 fps (14B) and 61.58 fps (1.3B). Throughput is also reported on 4090s over PCIe — [StreamDiffusionV2 project page](https://streamdiffusionv2.github.io/); [repo](https://github.com/chenfengxu714/StreamDiffusionV2)
- **MotionStream** (motion-controlled generation, not try-on). Reports 17 fps at 480p and 10 fps at 720p with sub-second latency on a single H100, and up to 29 fps with optimized VAE decoders — [MotionStream arXiv 2511.01266](https://arxiv.org/html/2511.01266v5)

### Inferences
- **What is real time today.** As of Oct 2026, the only demonstrated real-time generative video pipelines run on 1–4 H100-class GPUs. They are general video-to-video restylers that do not preserve a specific garment's logo/pattern/fit. LiveVVT is the first try-on-specific real-time claim; until hardware, resolution, code and license are confirmed, treat it as a research signal, not a deployable component.
- **Consumer hardware.** Real-time photoreal generative try-on on a home edge box (Jetson-class, 8 GB) is not feasible in 2026. A cloud-streamed variant would need H100-class capacity per active user. That is likely multiple $/hour per concurrent user at the GPU prices in Q5 (inference from those prices).
- **Product framing.** Video try-on is best offered as an asynchronous "make me a 5-second clip" feature generated in the cloud, not as the live mirror view.

### Gaps
- Not verified: per-clip generation time and VRAM for ViViD, Tunnel Try-on (no public code found), CatV2TON, MagicTryOn (14B/1.3B/Turbo) and Dress&Dance. The search budget was exhausted, and arXiv/project pages were unreachable.
- LiveVVT: GPU type, resolution, license and code availability are unknown.
- Snap's real-time generative lenses (on-device diffusion) and Decart's real-time video models: no sources retrieved, so no claims can be made.

---

## 4. Commercial try-on APIs: price per image, latency, terms

### Takeaway
Hosted photoreal try-on costs about **$0.06–$0.08 per image** from all three major options: FASHN API, Google Vertex AI Virtual Try-On and Kling/Kolors. Latency is seconds, not frames. Pricing for Perfect Corp, Revery.ai, Pixelcut and Replicate was not verified.

### Cited Findings
- **FASHN API — on-demand.** $0.075 per image, with a $7.50 minimum purchase (100 images) — [FASHN help: API pricing](https://help.fashn.ai/plans-and-pricing/api-pricing)
- **FASHN API — commitment tiers:**
  - Tier I: $19/month, 282 images included, $0.0675 top-ups.
  - Tier II: $249/month, 4,150 images included, $0.0600 top-ups.
  - Source: [FASHN help: API pricing](https://help.fashn.ai/plans-and-pricing/api-pricing)
- **FASHN app (credit) pricing.** The app pricing table lists Try-On at 2 credits base cost. A third-party review says 1 credit (standard) / 4 (Try-On Max); FASHN's own table is more authoritative — [FASHN help: app pricing](https://help.fashn.ai/plans-and-pricing/app-pricing); [vantaige.io](https://vantaige.io/ai-tool/fashn)
- **FASHN v1.6 on fal.ai.** fal.ai's 2026 roundup lists FASHN v1.6 at $0.075 per generation on fal — [fal.ai: Best Virtual Try-On APIs 2026](https://fal.ai/learn/tools/best-virtual-try-on-apis-2026)
- **Google Vertex AI Virtual Try-On — models.** Models are documented as `virtual-try-on-001` and `virtual-try-on-preview-08-04`, with a maximum of 4 output images per prompt. The docs defer pricing to the Imagen section of the Vertex AI pricing page — [Vertex AI: Virtual Try-On 001](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/imagen/virtual-try-on-001); [Virtual Try-On Preview 08-04](https://cloud.google.com/vertex-ai/generative-ai/docs/models/imagen/virtual-try-on-preview-08-04?hl=en)
- **Google Vertex AI Virtual Try-On — price.** Third-party trackers list about $0.060 per output image; reseller Pixazo charges $0.063. **Not confirmed on Google's pricing page** — [cloudprice.net](https://cloudprice.net/models/google-virtual-try-on-1); [Picasso IA blog](https://blog.picassoia.com/virtual-try-on-api-pricing-clothes-glasses-and-gemini)
- **Kling / Kolors Virtual Try-On v1.5 — resellers.** $0.07 per generation on fal.ai and on inference.sh. CometAPI lists $0.06608 per request against an "official" $0.0826 — [fal.ai Kolors VTON](https://fal.ai/models/fal-ai/kling/v1-5/kolors-virtual-try-on/llms.txt); [inference.sh](https://inference.sh/apps/klingai); [CometAPI](https://www.cometapi.com/models/kling/kling-virtual-try-on/)
- **Kling direct API.** Sold in prepaid units: trial pack of 100 units for $4.90, 5,000 units for $350 (about $0.07/unit). The unit-to-image mapping is unconfirmed — [PricingSaaS: Kling AI](https://pricingsaas.com/companies/klingai)

### Inferences
- **Cost per household.** For a home mirror, a hosted API is the fastest route to photoreal snapshots, but usage costs scale per image. At $0.06–$0.075, a household generating 20 snapshots/day (about 600/month) costs about $36–$45/month in API fees. A consumer business model likely needs either self-hosting (Q5) or rationing high-quality renders.
- **Terms to check.** Commercial terms (data retention of user body photos, training on customer images, output ownership) must be reviewed per vendor. They were not retrieved here.

### Gaps
- Not retrieved: official latency per call for FASHN, Vertex and Kling; FASHN's docs could not be fetched.
- Not retrieved (search budget exhausted): Perfect Corp (YouCam API), Revery.ai, Pixelcut, and Replicate-hosted IDM-VTON/CatVTON pricing.
- Not confirmed: Google's official per-image price, and whether `virtual-try-on-001` is GA.
- Not confirmed: data-privacy/commercial clauses for every vendor.

---

## 5. Self-hosting cost: cloud GPU price per hour and implied cost per try-on image

### Takeaway
Single-GPU on-demand prices in October 2026 (SkyPilot catalog snapshot) range from about $0.59/h (RunPod L4) to $8.26/h (AWS Mumbai, 1×H100). Using Leffa's measured 6 s/image on an A100, a fully utilized $1.79–1.99/h A100 gives about **$0.003/image**, roughly 20× cheaper than hosted APIs. This only holds at high utilization. A GPU kept warm 24/7 for a few homes costs $430–$700/month, which breaks even with FASHN API pricing at roughly 6,000–9,000 images/month.

### Cited Findings
Prices below are from SkyPilot's auto-generated catalogs (v8, master branch, fetched 16 Oct 2026), not from provider pages.
- **AWS on-demand (spot in parentheses):**
  - g6.xlarge (1×L4): $0.8048/h in us-east-1 ($0.508 spot); $0.9664/h in ap-south-1 Mumbai ($0.546 spot).
  - g5.xlarge (1×A10G): $1.006/h us-east-1; $1.208/h Mumbai.
  - g6e.xlarge (1×L40S): $1.861/h us-east-1; $2.235/h Mumbai.
  - p5.4xlarge (1×H100): $6.88/h us-east-1; $8.256/h Mumbai ($3.92 / $4.25 spot).
  - g4dn.xlarge (1×T4): $0.526/h us-east-1; $0.579/h Mumbai.
  - Source: [SkyPilot AWS catalog](https://github.com/skypilot-org/skypilot-catalog/blob/master/catalogs/v8/aws/vms.csv)
- **Lambda (1×GPU):** A10 $1.29/h, A100 $1.99/h, H100 PCIe $3.29/h, H100 SXM5 $4.29/h, GH200 $2.29/h, B200 $6.99/h, A6000 $1.09/h — [SkyPilot Lambda catalog](https://github.com/skypilot-org/skypilot-catalog/blob/master/catalogs/v8/lambda/vms.csv)
- **RunPod Secure Cloud (1×GPU):** L4 $0.59/h, RTX 4090 $0.89/h, RTX 5090 $1.19/h, A40 $0.59/h, L40S $1.09/h, A100-80GB $1.79/h, H100 (PCIe) $2.89/h, H100 SXM $3.99/h. RunPod also lists Indian regions (AP-IN-1/2) — [SkyPilot RunPod catalog](https://github.com/skypilot-org/skypilot-catalog/blob/master/catalogs/v8/runpod/vms.csv)
- **GCP:**
  - L4 GPU: $0.560/h (us-central1) or $0.583/h (asia-south1 Mumbai), plus a g2-standard-4 VM at $0.147/h or $0.153/h.
  - H100 GPU: $9.80/h (us-central1) or $10.19/h (asia-south1).
  - Source: [SkyPilot GCP catalog](https://github.com/skypilot-org/skypilot-catalog/blob/master/catalogs/v8/gcp/vms.csv)
- **Speed anchor.** Leffa generates an image in about 6 s on an A100 (fp16) — [Leffa README](https://github.com/franciszzj/Leffa)

### Inferences
- **Implied cost/image formula:** (price per hour ÷ 3600) × seconds per image ÷ utilization. All results below are computed, not quoted.
- **Worked examples at 6 s/image (Leffa on A100, 100% utilization):**
  - RunPod A100 $1.79/h → **$0.0030/image**.
  - Lambda A100 $1.99/h → $0.0033.
  - AWS p4d per-GPU (about $2.74/h) → $0.0046.
  - At a realistic 30–50% utilization, multiply by 2–3×, giving about $0.006–0.014/image.
- **Always-on GPU, 730 h/month:**
  - RunPod L4: about $431/month.
  - AWS us-east-1 L4: about $588/month.
  - AWS Mumbai L4: about $705/month.
  - Break-even vs FASHN at $0.075: about 5,700 images/month (RunPod L4) and about 9,400 images/month (AWS Mumbai L4).
- **L4/A10G speed.** L4/A10G-class GPUs should handle 8 GB-class models (CatVTON-sized, FLUX.2 klein 4B, FASHN VTON 1.5 with about 2 GB weights). Per-image time on L4 is unmeasured; it is likely slower than an A100.
- **India deployment.** AWS ap-south-1 (Mumbai) is consistently about 20% above us-east-1 (L4 0.9664 vs 0.8048; A10G 1.208 vs 1.006; H100 8.256 vs 6.88 $/h), but cuts round-trip latency to Indian homes. RunPod also lists IN regions.

### Gaps
- E2E Networks (India) GPU pricing was not retrieved (site unreachable, search budget exhausted).
- The SkyPilot catalog is third-party, auto-generated; verify on the RunPod, Lambda and AWS pricing pages before committing. Some RunPod values (e.g., RTX 4090 at $0.89/h Secure) are higher than 2025 levels, and Community Cloud prices were not captured.
- No measured seconds/image on L4, A10G or RTX 4090 for any VTON model was found.

---

## 6. Real-time pose and segmentation on edge hardware (Jetson Orin Nano Super, Raspberry Pi 5 + Hailo, RK3588, phones)

### Takeaway
Pose and person/clothes segmentation at ≥30 fps is solved on all three edge platforms (Jetson Orin Nano Super, Pi 5 + Hailo, RK3588 NPU) and on phones:
- **Pose.** YOLO26n detection runs in 4.57 ms (TensorRT FP16) on a Jetson Orin Nano Super; this is a proxy, as no pose-variant figure was published for that board. YOLOv8s-pose runs at 107 fps on a Hailo-8L and 393 fps on a Hailo-8 (vendor host). YOLOv8n-pose runs at 58 fps on one RK3588 NPU core.
- **Segmentation.** MediaPipe's multiclass segmenter does have a **"clothes"** class.
- **SAM 2 is not an edge real-time option.** It runs 0.7 fps on an iPhone; EdgeTAM runs 16 fps there.
- **Licensing.** Ultralytics YOLO is **AGPL-3.0** (an enterprise license is needed for a closed product), and Robust Video Matting is **GPL-3.0**.

### Cited Findings
**Jetson Orin Nano Super**
- **Specs.** 67 TOPS, 1024-core Ampere GPU with 32 Tensor Cores, 8 GB 128-bit LPDDR5 at 102 GB/s — [Ultralytics Jetson guide](https://github.com/ultralytics/ultralytics/blob/main/docs/en/guides/nvidia-jetson.md)
- **YOLO26 detection, inference only (excludes pre/post-processing; Ultralytics 8.4.33):**
  - YOLO26n: TensorRT FP16 4.57 ms; INT8 3.80 ms (NCNN 47.5 ms; PyTorch 15.6 ms).
  - YOLO26s: FP16 7.17 ms.
  - YOLO26m: FP16 13.59 ms.
  - Source: [Ultralytics Jetson guide](https://github.com/ultralytics/ultralytics/blob/main/docs/en/guides/nvidia-jetson.md)

**YOLO26-pose (successor to YOLO11-pose), COCO keypoints, 640 px**
- YOLO26n-pose: mAP50-95 57.2; 40.3 ms CPU ONNX; 1.8 ms on a T4 (TensorRT10).
- YOLO26s-pose: 63.0; 85.3 ms; 2.7 ms.
- YOLO26m-pose: 68.8; 218 ms; 5.0 ms.
- YOLO26x-pose: 71.6; 565 ms; 12.2 ms.
- Source: [Ultralytics pose perf table](https://github.com/ultralytics/ultralytics/blob/main/docs/macros/yolo-pose-perf.md)
- **License.** Ultralytics is AGPL-3.0; "Request an Enterprise License for commercial use" — [Ultralytics LICENSE](https://github.com/ultralytics/ultralytics/blob/main/LICENSE); [Ultralytics README](https://github.com/ultralytics/ultralytics)

**Raspberry Pi 5 (CPU only)**
- YOLO26n NCNN: 67.03 ms/image. YOLO26s NCNN: 172.88 ms (detection) — [Ultralytics Raspberry Pi guide](https://github.com/ultralytics/ultralytics/blob/main/docs/en/guides/raspberry-pi.md)

**Raspberry Pi AI HAT+ / Hailo**
- **AI HAT+ variants.** Hailo-8L (13 TOPS INT8) or Hailo-8 (26 TOPS INT8).
- **AI HAT+ 2.** Hailo-10H (40 TOPS INT4) with its own 8 GB RAM, able to run LLMs/VLMs up to about 6B parameters.
- **AI Kit.** Equivalent to the Hailo-8L AI HAT+ and no longer in production.
- Source: [Raspberry Pi AI HAT+ docs](https://github.com/raspberrypi/documentation/blob/master/documentation/asciidoc/accessories/ai-hat-plus/about.adoc)
- **Hailo Model Zoo, Hailo-8L, 640x640** (measured on an Intel i5-9400 host over PCIe Gen3 x4, not on a Pi):
  - yolov8s_pose: **107 fps** (batch 1), 202 fps (batch 8).
  - yolov8m_pose: 48.5 / 81.9 fps.
  - Source: [HAILO8L pose table](https://github.com/hailo-ai/hailo_model_zoo/blob/master/docs/public_models/HAILO8L/HAILO8L_pose_estimation.rst)
- **Hailo-8L segmentation (same host):**
  - yolov8n_seg: 168 fps (b1).
  - yolov8s_seg: 88 fps.
  - yolov11n_seg: 149 fps.
  - Source: [HAILO8L instance segmentation table](https://github.com/hailo-ai/hailo_model_zoo/blob/master/docs/public_models/HAILO8L/HAILO8L_instance_segmentation.rst)
- **Hailo-8 pose (same host):** yolov8s_pose 393 fps; yolov8m_pose 68.6 fps (b1) — [HAILO8 pose table](https://github.com/hailo-ai/hailo_model_zoo/blob/master/docs/public_models/HAILO8/HAILO8_pose_estimation.rst)
- **Hailo's Pi examples.** Hailo's official Raspberry Pi 5 examples include a human pose estimation pipeline for the AI Kit/AI HAT — [hailo-rpi5-examples](https://github.com/hailo-ai/hailo-rpi5-examples)

**Rockchip RK3588 NPU**
- **RKNN Model Zoo** (single NPU core, INT8, inference only, max NPU frequency):
  - yolov8n-pose 640x640: **58.3 fps**.
  - yolov8n-seg: 63.2 fps.
  - yolo26n: 55.0 fps.
  - deeplabv3 (513x513): 34.7 fps.
  - MobileSAM tiny encoder (FP16): 10.3 fps.
  - Source: [RKNN Model Zoo](https://github.com/airockchip/rknn_model_zoo)
- **Ultralytics on Radxa Rock 5B (RK3588).** YOLO26n rknn INT8 41.2 ms (FP16 58.5 ms); YOLO26s INT8 61.9 ms. That is slower than the model-zoo figure, likely due to measurement method — [Ultralytics RKNN guide](https://github.com/ultralytics/ultralytics/blob/main/docs/en/integrations/rockchip-rknn.md)

**RTMPose (Apache-2.0, top-down, 256x192, latency excludes the person detector)**
- RTMPose-s: COCO AP 72.2; 4.48 ms ONNX Runtime on i7-11700 CPU; 1.39 ms TensorRT-FP16 on GTX 1660 Ti; 13.89 ms ncnn-FP16 on Snapdragon 865.
- RTMPose-m: AP 75.8; 11.06 / 2.29 / 26.44 ms on the same three platforms.
- Source: [RTMPose README](https://github.com/open-mmlab/mmpose/tree/main/projects/rtmpose)

**MediaPipe BlazePose GHUM**
- **Pixel 3 (TFLite GPU) latency:** Heavy 53 ms, Full 25 ms, Lite 20 ms.
- **MacBook Pro 15" 2017 latency:** 38 / 27 / 25 ms.
- Source: [MediaPipe Pose docs](https://github.com/google-ai-edge/mediapipe/blob/master/docs/solutions/pose.md)
- **Model card (Pixel 3):**
  - Lite: about 44 fps on CPU (XNNPack), about 49 fps on GPU.
  - Full: about 18 fps on CPU, about 40 fps on GPU.
  - Heavy: about 4 fps on CPU, about 19 fps on GPU.
  - Source: [BlazePose GHUM 3D model card](https://storage.googleapis.com/mediapipe-assets/Model%20Card%20BlazePose%20GHUM%203D.pdf)

**MediaPipe multiclass selfie segmentation (Apache-2.0)**
- **Classes.** Classifies each pixel as background, hair, body-skin, face-skin, **clothes**, or others (accessories).
- **Model.** A ViT with "customized bottleneck and decoder architecture for real-time performance", in 256x256 and 512x512 variants. It supports single or multiple people, and selfies or full-body images.
- **Limitations.** It "may not provide pixel perfect masks". Quality degrades with low light, backlit subjects, noise, fast motion and large occluders.
- Source: [Multiclass Segmentation model card](https://storage.googleapis.com/mediapipe-assets/Model%20Card%20Multiclass%20Segmentation.pdf)

**SAM 2.1 / EdgeTAM / EfficientTAM / RVM / BiRefNet**
- **SAM 2.1 (Apache-2.0)** on an A100 (torch 2.5.1, compiled): tiny 91.2 fps, small 84.8, base+ 64.1, large 39.5 — [SAM 2 README](https://github.com/facebookresearch/sam2)
- **EdgeTAM (Apache-2.0).**
  - "22× faster than SAM 2 and achieves 16 FPS on iPhone 15 Pro Max without quantization".
  - Video object segmentation: EdgeTAM 15.7 fps on iPhone vs SAM 2-B+ 0.7 fps; 150.9 fps on A100.
  - Source: [EdgeTAM README](https://github.com/facebookresearch/EdgeTAM)
- **EfficientTAM** is another Apache-2.0 lightweight SAM 2 alternative — [EfficientTAM README](https://github.com/yformer/EfficientTAM)
- **Robust Video Matting:**
  - RTX 3090 FP16: 172 fps (HD), 154 fps (4K).
  - RTX 2060 Super FP16: 134 / 108 fps.
  - GTX 1080 Ti FP32: 104 / 74 fps.
  - License: **GPL-3.0**.
  - Source: [RVM README](https://github.com/PeterL1n/RobustVideoMatting)
- **BiRefNet (MIT).** 17 fps at 1024x1024 using 3.45 GB on an RTX 4090 (FP16) — [BiRefNet README](https://github.com/ZhengPeng7/BiRefNet)

### Inferences
- **Recommended edge stack for the live mirror.** Pose plus clothes/body segmentation (MediaPipe multiclass 256, Apache-2.0) on a Jetson Orin Nano Super or RK3588 leaves ample headroom at 30 fps. Pose options:
  - BlazePose for 33 3D landmarks.
  - RTMPose-s (Apache-2.0).
  - YOLO-pose, only if an Ultralytics enterprise license is acceptable.
- **Pi 5 caveat.** Hailo's 107 fps (8L) figure is from a PCIe Gen3 x4 x86 host. On a Pi 5 (narrower PCIe link) expect lower throughput. CPU-only Pi 5 (about 67 ms for YOLO26n) is not enough for a full pipeline.
- **License hygiene.** Avoid GPL (RVM) and AGPL (Ultralytics) components in a closed product unless licensed. MediaPipe, RTMPose/MMPose, SAM 2, EdgeTAM and BiRefNet are permissive.

### Gaps
- Not found: pose-specific benchmarks on the Jetson Orin Nano Super. Detection numbers are the proxy.
- Not found: MediaPipe multiclass segmenter latency on any named device (the current ai.google.dev docs were unreachable).
- Not found: measured Hailo fps on an actual Raspberry Pi 5.
- Not found: recent-phone figures (2025–26 Snapdragon/Apple A-series) for RTMPose/MediaPipe.

---

## 7. Wardrobe digitization: background removal, attribute tagging, colour, and flat-lay/hanger-to-body quality problems

### Takeaway
Cutting out garment photos and tagging their attributes is mature, with permissive options:
- **Background removal:** BiRefNet (MIT) or SAM 2 (Apache-2.0).
- **Attribute tagging:** FashionCLIP (MIT code) or a VLM.

But the **default model in rembg (BRIA RMBG-2.0) requires a paid commercial agreement**. The hard part is the on-body try-on from a home flat-lay or hanger photo. Most VTON models are trained on studio product images (VITON-HD/DressCode), and real-world garments are a known weak spot. FASHN VTON v1.5 explicitly supports flat-lay inputs. "Try-off" models that recover a clean garment image (TryOffDiff) are SSPL-licensed.

### Cited Findings
- **rembg default model.** rembg's code is MIT, but its default model is now `bria-rmbg` (RMBG-2.0, about 1.02 GB, 1024x1024). RMBG-2.0 is "released under a BRIA license that requires a paid agreement for commercial use"; alternatives include `birefnet-*`, `isnet-general-use`, `u2net`, and `u2net_cloth_seg` (cloth parsing) — [rembg README](https://github.com/danielgatis/rembg)
- **BiRefNet.** MIT. FP16 inference uses about 3.5 GB, at 57.7 ms per image on an RTX 4090 and 69.4 ms on an A100. Weights trained by BRIA on private data (RMBG-2.0) are "for only non-commercial use" — [BiRefNet README](https://github.com/ZhengPeng7/BiRefNet)
- **SAM 2 / SAM 2.1.** Checkpoints and code are Apache-2.0 — [SAM 2 README](https://github.com/facebookresearch/sam2)
- **FashionCLIP.** Code is MIT. The model was updated (10/03/23) to start from the LAION CLIP ViT-B/32 checkpoint and is aimed at zero-shot fashion retrieval and classification. Weights are on Hugging Face — [FashionCLIP README](https://github.com/patrickjohncyh/fashion-clip)
- **FASHN VTON v1.5 garment inputs.** "Supports both model photos and flat-lay product shots as garment inputs" (tops / bottoms / one-pieces) — [FASHN VTON v1.5 README](https://github.com/fashn-AI/fashn-vton-1.5)
- **Training-data domain gap.** MagicTryOn is "trained on public datasets including VITON-HD, DressCode, and ViViD" and invites in-the-wild training "to better support real-world virtual try-on scenarios" — [MagicTryOn README](https://github.com/vivoCameraResearch/Magic-TryOn)
- **In-the-wild datasets.** TripVVT introduces a large triplet dataset specifically for in-the-wild video try-on — [TripVVT arXiv 2604.27958](https://arxiv.org/pdf/2604.27958)
- **TryOffDiff.** Reconstructs a canonical garment image from a worn photo ("Virtual-Try-Off"); a follow-up adds multi-garment try-off. License: "Not available for commercial use, unless the FULL source code is open-sourced" (SSPL) — [TryOffDiff README](https://github.com/rizavelioglu/tryoffdiff)
- **Human parsing.** MediaPipe multiclass segmentation's "clothes" class can isolate garments on a worn photo (Apache-2.0) — [Multiclass Segmentation model card](https://storage.googleapis.com/mediapipe-assets/Model%20Card%20Multiclass%20Segmentation.pdf)
- **fashn-human-parser.** Gives 18 finer classes but carries NVIDIA's non-commercial SegFormer license — [fashn-human-parser README](https://github.com/fashn-AI/fashn-human-parser); [SegFormer LICENSE](https://github.com/NVlabs/SegFormer/blob/master/LICENSE)
- **On-device tagging.** Raspberry Pi's AI HAT+ 2 (Hailo-10H) can run VLMs up to about 6B parameters locally, enabling on-device garment tagging — [Raspberry Pi AI HAT+ docs](https://github.com/raspberrypi/documentation/blob/master/documentation/asciidoc/accessories/ai-hat-plus/about.adoc)

### Inferences
- **Recommended capture pipeline:**
  1. A guided capture: garment flat on a plain contrasting surface, or on a hanger against a wall, shot square-on with even light.
  2. Background removal with BiRefNet (MIT) or SAM 2.
  3. Perspective correction and white balance.
  4. Dominant-colour extraction (k-means in a perceptual space such as CIELAB on the masked pixels).
  5. VLM/FashionCLIP tagging of category, colour names, pattern, material, formality and season, with user confirmation.
- **Expected flat-lay/hanger failure modes** (inferred from the dataset gap above):
  - wrinkles and folds baked into the texture;
  - perspective/keystone distortion;
  - folded sleeves or collars, and no back view;
  - hanger shoulders distorting the garment shape;
  - logo/print warping;
  - colour shifts from home lighting;
  - fit/size not modelled at all (try-on shows "how it looks", not "how it fits").
- **Mitigation.** A one-time "try-off" or cleanup step could normalize home photos. TryOffDiff itself is SSPL, so a commercial product would need its own model.

### Gaps
- Not verified: published quantitative evaluations of flat-lay/hanger vs product-image input quality for specific VTON models.
- Not verified: FashionCLIP weights license and its tagging accuracy, or VLM (GPT/Gemini/Qwen-VL) garment-tagging accuracy.
- Colour-harmony rule sources (Itten/Matsuda-style schemes) were not retrieved.

---

## 8. Outfit recommendation: rules, learned compatibility (Polyvore), LLM/VLM stylists

### Takeaway
Learned outfit-compatibility research is mature and openly licensed. The main examples are type-aware embeddings on the Polyvore Outfits dataset (BSD-3 code) and the Bi-LSTM outfit model (Apache-2.0 code). These models are trained on curated web outfits rather than one person's wardrobe. A practical home product would likely combine:
- rule-based filters (weather, dress code, colour harmony);
- embedding-based compatibility scoring;
- an LLM/VLM explanation layer.

No verified 2025–26 benchmarks of LLM stylists were retrieved.

### Cited Findings
- **Type-aware embeddings (Vasileva et al., ECCV 2018).** "Learning Type-Aware Embeddings for Fashion Compatibility". The Polyvore Outfits dataset includes splits and questions for the compatibility and fill-in-the-blank tasks (about 6 GB, hosted on Hugging Face). Code is BSD-3-Clause — [fashion-compatibility repo](https://github.com/mvasil/fashion-compatibility)
- **Bi-LSTM model (Han et al., ACM MM 2017).** "Learning Fashion Compatibility with Bidirectional LSTMs", trained on Polyvore.com outfit data. Code is Apache-2.0 — [polyvore repo](https://github.com/xthan/polyvore)
- **FashionCLIP embeddings.** Can provide zero-shot attribute and category signals for the wardrobe items (MIT code) — [FashionCLIP README](https://github.com/patrickjohncyh/fashion-clip)
- **Multi-item try-on of a recommended outfit.** FastFit can try on a full outfit (top, bottom, shoes, bag) in one pass, but it is non-commercial. Its DressCode-MR dataset has 28,179 multi-reference samples — [FastFit README](https://github.com/Zheng-Chong/FastFit)

### Inferences
- **Suggested recommender design:**
  1. Hard constraints from rules: occasion/dress code, weather, laundry status, not-worn-recently.
  2. Colour-harmony scoring on the extracted CIELAB colours (complementary/analogous/neutral pairing rules).
  3. Compatibility scoring via type-aware embeddings fine-tuned on public outfit data.
  4. An LLM/VLM to re-rank and explain choices in natural language, and to learn user feedback.
- **Data sufficiency.** One person's wardrobe (50–300 items) is too small to train a compatibility model. Use pretrained embeddings plus rules, and personalize with likes/dislikes.

### Gaps
- Not retrieved: current SOTA numbers on Polyvore compatibility AUC / FITB (e.g., OutfitTransformer and later); the search budget was exhausted.
- Not retrieved: studies evaluating LLM/VLM stylists against human stylists.
- Not retrieved: authoritative sources for colour-harmony rules or dress-code taxonomies.

---

## 9. What glass-to-glass latency feels natural for a video "digital mirror", and how are horizontal flip and mirror-like scaling handled?

### Takeaway
No source on mirror latency perception could be retrieved and verified this session, so the thresholds below are recalled and need checking. Recalled literature suggests motor performance degrades above about 75 ms and the sense of agency/ownership above about 125 ms. A target of **≤100 ms glass-to-glass (ideally ≤60–80 ms)** is a reasonable engineering goal.

Horizontal flip is standard: MediaPipe's own sample flips frames "for a selfie-view display". Mirror-like scale follows from optics: the reflection occupies half the user's height on the glass at any distance. The display should therefore render the user at 0.5× life size and adjust for distance.

### Cited Findings
- **Horizontal flip.** MediaPipe's pose sample code does `cv2.flip(image, 1)` with the comment "Flip the image horizontally for a selfie-view display" — [MediaPipe Pose docs](https://github.com/google-ai-edge/mediapipe/blob/master/docs/solutions/pose.md)
- **Example latencies for per-frame inference stages** (they sit inside the glass-to-glass budget):
  - BlazePose Full: 25 ms on a Pixel 3 GPU — [MediaPipe Pose docs](https://github.com/google-ai-edge/mediapipe/blob/master/docs/solutions/pose.md)
  - YOLO26n: 4.57 ms TensorRT FP16 on a Jetson Orin Nano Super — [Ultralytics Jetson guide](https://github.com/ultralytics/ultralytics/blob/main/docs/en/guides/nvidia-jetson.md)
  - RTMPose-s: 13.89 ms on a Snapdragon 865 — [RTMPose README](https://github.com/open-mmlab/mmpose/tree/main/projects/rtmpose)
- **Real-time generative pipelines are too slow for the live loop.** Even the fastest report about 0.5 s to first frame (StreamDiffusionV2 on 4×H100) — [StreamDiffusionV2 project page](https://streamdiffusionv2.github.io/)

### Inferences
- **Latency budget at 60 fps capture and display (estimated, not measured):**
  - camera exposure + readout ≈ 17–33 ms;
  - capture/ISP/transfer ≈ 5–20 ms;
  - pose + segmentation ≈ 5–25 ms;
  - warp/composite/render ≈ 5–15 ms;
  - display scan-out + panel response ≈ 17–35 ms;
  - total ≈ 50–130 ms.
- **Display choice.** TV panels with image processing can add tens of ms or more unless run in a "game"/low-latency mode. A monitor-class panel is preferable.
- **Mirror-like scale (plane-mirror optics).** The reflection appears at twice the user's distance from the glass, and on the glass it spans half the user's height regardless of distance. To emulate a mirror:
  - the renderer must keep the on-screen body at about 0.5× real height, counter-scaling as the user steps closer or farther (camera image size scales roughly as 1/distance);
  - align the eye line with the user's actual eye height.
- **Camera placement.** A camera at the top of the frame produces a looking-down perspective that no mirror shows. Better options are a camera behind a two-way mirror at about chest/eye height, or depth + view re-projection. A single fixed camera cannot reproduce a mirror's viewpoint-dependent parallax.
- **Live preview vs snapshot.** Keep the generative render out of the live loop; show it as a snapshot/"freeze-frame" result.

### Gaps
- **Not verified this session (recalled from prior knowledge):** Waltemate et al., VRST 2016, "The Impact of Latency on Perceptual Judgments and Motor Performance in Closed-loop Interaction in Virtual Reality" ([ACM DL](https://dl.acm.org/doi/10.1145/2993369.2993381)). It used a full-body virtual mirror and reportedly found:
  - motor performance and simultaneity perception affected above about 75 ms;
  - sense of agency/body ownership declining only above about 125 ms;
  - strong deterioration above about 210 ms.
  The report writer should verify these thresholds before relying on them.
- No industry figures were found for the glass-to-glass latency of commercial smart mirrors (FXMirror, MemoMi, etc.) or for two-way-mirror light-transmission losses for a camera behind glass.

---

## 10. Recommended realistic architecture: on-device vs cloud; live low-fidelity preview vs high-quality snapshot

### Takeaway
Use a **two-tier design**:
- **Live tier (edge, 30–60 fps).** Pose, segmentation and a lightweight 2D garment overlay run on a Jetson Orin Nano Super or RK3588 class device inside the mirror. Glass-to-glass target is ≤100 ms.
- **Photoreal tier (cloud, 5–20 s).** Triggered by a pose-hold or gesture, it returns a still try-on of the user in their own garment. It runs on a commercial API (about $0.06–0.075/image) or a self-hosted commercially licensed model (about $0.003–0.015/image at good utilization).
- **Video clips.** Offline cloud jobs for now. Real-time generative video try-on (LiveVVT, Aug 2026) is a 2027+ upgrade path, not a launch dependency.

### Cited Findings
- **Edge pose + segmentation runs at ≥30 fps:**
  - Jetson Orin Nano Super, YOLO26n TensorRT FP16: 4.57 ms — [Ultralytics Jetson guide](https://github.com/ultralytics/ultralytics/blob/main/docs/en/guides/nvidia-jetson.md)
  - RK3588 single NPU core: yolov8n-pose 58.3 fps; yolov8n-seg 63.2 fps — [RKNN Model Zoo](https://github.com/airockchip/rknn_model_zoo)
  - MediaPipe multiclass segmentation includes a "clothes" class and is built for real-time on-device use — [model card](https://storage.googleapis.com/mediapipe-assets/Model%20Card%20Multiclass%20Segmentation.pdf)
- **Real-time 2D try-on precedent:**
  - DM-VTON: 40 fps on a T4, but non-commercial — [DM-VTON](https://github.com/KiseKloset/DM-VTON)
  - Snap Garment Transfer: real-time upper-body try-on from a single 2D image — [Snap docs](https://developers.snap.com/lens-studio/features/try-on/garment-transfer)
- **Photoreal snapshot options:**
  - FASHN API: $0.075 on-demand, $0.06 at Tier II top-up — [FASHN help](https://help.fashn.ai/plans-and-pricing/api-pricing)
  - Vertex AI Virtual Try-On: about $0.06, third-party figure — [cloudprice.net](https://cloudprice.net/models/google-virtual-try-on-1)
  - Kling/Kolors: $0.07 via fal.ai — [fal.ai](https://fal.ai/models/fal-ai/kling/v1-5/kolors-virtual-try-on/llms.txt)
  - FASHN VTON v1.5 open weights: Apache-2.0, about 2 GB — [repo](https://github.com/fashn-AI/fashn-vton-1.5)
  - Leffa: MIT code, 6 s on A100 — [repo](https://github.com/franciszzj/Leffa)
- **Video try-on state:** MagicTryOn is offline and non-commercial; LiveVVT claims 22.39 fps, unverified hardware — [MagicTryOn](https://github.com/vivoCameraResearch/Magic-TryOn); [LiveVVT](https://www.alphaxiv.org/abs/2608.26714)
- **Generic real-time video diffusion needs 4×H100 for about 58–64 fps** — [StreamDiffusionV2](https://streamdiffusionv2.github.io/)

### Inferences
- **On-device (mirror) components:**
  - camera capture at 60 fps;
  - horizontal flip and mirror-scale/eye-line correction;
  - pose (BlazePose 33-pt 3D or RTMPose-s, both permissive licenses);
  - person + clothes segmentation (MediaPipe multiclass);
  - a live overlay renderer.

  The overlay renderer can be either:
  - a 2D texture-warp of the garment cut-out onto the torso/limb segments, using pose keypoints and occlusion from the segmentation mask (custom, or a commercially retrained warping network); or
  - for a small set of "hero" garments, pre-made 3D assets rendered on an MHR (Apache-2.0) body fit.

  Also on-device:
  - gesture/pose-hold detection to trigger snapshots;
  - optional local VLM tagging on an AI HAT+ 2-class NPU.
- **Cloud components:**
  - wardrobe ingestion (background removal with BiRefNet, tagging, colour extraction);
  - the photoreal snapshot service (vendor API at launch; migrate to a self-hosted, commercially licensed model on L4/A10G/A100 once volume exceeds about 6–9k images/month);
  - outfit recommender (rules + compatibility embeddings + LLM explanations);
  - optional async video clips.

  Prefer Mumbai/India regions (AWS ap-south-1 or RunPod IN) for latency to Indian users, at about a 20% price premium over us-east-1 on AWS.
- **User experience.** Label the live view clearly as a "preview" and the snapshot as the "realistic look". This manages expectations, because the live 2D overlay will not match diffusion quality.
- **Privacy.** Body images leave the home only for snapshots. Process the live loop entirely on-device, and choose vendors with no-training/no-retention terms.
- **License checklist before shipping.** Exclude:
  - CC BY-NC-SA models (IDM-VTON, OOTDiffusion, CatVTON, StableVITON, FitDiT, DM-VTON, CatV2TON, MagicTryOn);
  - FLUX.1-dev derivatives (OmniTry, Any2AnyTryon, CatVTON-FLUX);
  - SMPL-X;
  - NVIDIA SegFormer-based parsers;
  - BRIA RMBG-2.0;
  - SSPL TryOffDiff;
  - AGPL Ultralytics and GPL RVM, unless licensed.

### Gaps
- Not measured: end-to-end latency for the proposed edge pipeline.
- Not compared: visual quality of a custom 2D warp vs Snap Garment Transfer vs 3D simulation on real home-wardrobe photos. A prototype bake-off is needed.
- Not confirmed: vendor data-retention and commercial-use terms (FASHN, Google, Kling), and E2E Networks pricing.
