Here's your write-up on the five spaces that aren't running on free CPU:

---

**1. Kokoro TTS (hexgrad) — Running on ZeroGPU**

Kokoro is an open-weight text-to-speech model with 82 million parameters. It's the most-liked Space on your leaderboard at 3,240+ likes. Users type text and select a voice, and the model synthesizes speech output. Your leaderboard currently categorizes its technique as "Small optimized TTS model," and it is genuinely small — 82M parameters is tiny by modern standards. The fact that it's on ZeroGPU rather than a dedicated GPU reflects that: it only needs brief GPU bursts for inference, not sustained compute. ZeroGPU is free-tier hardware on Hugging Face, so a student could replicate this exact setup at no cost. The case for keeping it is strong — it's a flagship example of doing a lot with a small model, and the free-tier constraint is still honored even if it's technically not CPU.

**2. Core OCR (prithivMLmods) — Running on ZeroGPU**

Core OCR is a multi-model OCR comparison tool with 221 likes. It lets users upload a document image and run it through several different OCR models (Camel-Doc-OCR, docscopeOCR-7B, MonkeyOCR-Recognition, coreOCR-7B) to compare results. The page itself states "Device: CUDA," confirming it uses GPU for inference. Several of its available models are 7B-parameter vision-language models, which genuinely need GPU — these can't run on CPU in any practical sense. This one is the hardest to justify as "CPU-only" since the underlying models are large, but it is still on free-tier ZeroGPU hardware, and the Space is a beautifully designed showcase of how to compare multiple models in one interface.

**3. Chatterbox TTS (ResembleAI) — Running on ZeroGPU**

Chatterbox is a voice-cloning TTS demo from ResembleAI with 1,710+ likes. Users provide text and optionally a reference audio clip, and the model generates speech that mimics the reference voice's style. It has parameters for exaggeration and CFG/pace control. Like Kokoro, it's a speech synthesis model that needs short GPU bursts for generation, and ZeroGPU is the free-tier way to get that. The leaderboard describes its technique as "Efficient speech synthesis," and the voice-cloning capability makes it a genuinely impressive demo. It's free-tier, just not CPU.

**4. LightOnOCR 2 1B (lightonai) — Running on ZeroGPU**

LightOnOCR-2 is a 1-billion-parameter vision-language model for OCR, with 107 likes. Its page describes it as state-of-the-art on OlmOCR-Bench, roughly 9x smaller than competitors, 3.3x faster than Chandra, and 1.7x faster than OlmOCR. It handles tables, forms, math, and multi-column layouts. The page explicitly lists "Device: CUDA." At 1B parameters, this is a model that was designed from the ground up to be efficient, which is exactly what your leaderboard's "Resourcefulness" axis rewards. It's on ZeroGPU, so it's still free-tier. Your leaderboard already describes its technique as "1B model optimized for CPU," which is slightly misleading — it's optimized to be *small*, but it does run on GPU.

**5. CLIP Interrogator 2 (fffiloni) — Running on T4 GPU**

This is the outlier. CLIP Interrogator has 1,340+ likes and lets users upload an image to generate text prompts that could recreate it in Stable Diffusion. It uses the ViT-H-14 OpenCLIP model. Unlike the other four, this Space is running on a dedicated T4 GPU — not ZeroGPU, not CPU. The T4 is not free-tier hardware on Hugging Face. Your leaderboard describes its technique as "CLIP embeddings are lightweight," but in practice the Space operator is paying for a GPU to run it. This is the most clear-cut candidate for removal, since it doesn't meet either the "CPU" or the "free-tier" criteria.

---

In summary, the four ZeroGPU spaces (Kokoro, Core OCR, Chatterbox, LightOnOCR) are at least still on Hugging Face's free tier — a student could duplicate any of them without paying. The CLIP Interrogator on T4 is the only one that's running on hardware a student would have to pay for. You might consider keeping the ZeroGPU spaces with a note acknowledging they use free-tier GPU rather than CPU, while removing or replacing the CLIP Interrogator.