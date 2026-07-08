# VLM-CASE: Vision-Language-Model-Enabled Context-Adaptive Safety Envelopes

Supplementary materials for the paper:

> **VLM-CASE: vision-language model enabled context-adaptive safety envelopes for anticipatory safe autonomous driving**
> Tianjia Yang, Ke Li, Ruwen Qin, Xianbiao Hu
>
> [![arXiv](https://img.shields.io/badge/arXiv-2607.05180-b31b1b.svg)](https://arxiv.org/abs/2607.05180)

Preprint: [arXiv:2607.05180](https://arxiv.org/abs/2607.05180)

VLM-CASE gives an autonomous vehicle anticipatory, human-like caution under adverse driving conditions: a fine-tuned vision-language model (VLM) reasons about the driving scene from the front camera and parametrizes a context-adaptive safety envelope (CASE), a formally grounded admissible action set that couples braking and steering through a shared friction budget and widens the following margin as visibility degrades. A model predictive controller then drives freely within the envelope.

## Repository contents

| Folder | Contents |
|---|---|
| `dataset/` | The scene-context dataset: 10,560 labeled CARLA front-camera frames (download instructions inside) |
| `scenarios/` | Definitions of all 66 evaluation scenarios: experiment configs, per-town scenario conditions, and lead-vehicle profiles |
| `results/tables/` | Aggregated results (CSV) behind every table in the paper |
| `results/figures/` | The result figures of the paper (PDF and PNG) |
| `gifs/` | Representative closed-loop recordings of the proposed controller |

## Dataset

The dataset comprises 10,560 front-camera frames (1280×720) collected in CARLA across three road surfaces (dry, wet, snow), three weather types (clear, heavy rain, dense fog), day/night, and three illumination-assistance levels, each labeled with the four scene-context fields. Splits: 8,448 train / 1,056 validation / 1,056 test, stratified over the joint label distribution.

**Download:** [ytj254/VLM-CASE_carla_dataset](https://huggingface.co/datasets/ytj254/VLM-CASE_carla_dataset) on Hugging Face. See `dataset/README.md` for the label schema.

## Evaluation scenarios

Three experiment groups, 66 scenarios, 198 runs (3 runs each):

- **No-lead driving** (18): lateral safety under friction alone — dry (N1, μ=0.8), wet (N2, μ=0.4), snow (N3, μ=0.2).
- **Constant-lead following** (30): following distance under visibility alone — clear day (L1), foggy day (L2), clear night with strong (L3), partial (L4), and no (L5) illumination assistance.
- **Lead braking** (18): integrated stress test — the lead brakes hard to a stop under C1 (dry, clear day), C2 (wet, heavy rain, night, partial illumination), and C3 (snow, clear night, strong illumination).

Each scenario is defined by a map (Town03 urban, 40–60 km/h; Town04 highway, 70–90 km/h), a condition, and a speed. See `scenarios/`.

## Headline results

On the integrated lead-braking test, VLM-CASE-MPC completes **54/54 runs (100%)**, against 81.5% for a non-adaptive envelope, 75.9% for a state-of-the-art VLM-integrated controller, and 51.9% for a base MPC. Full per-condition results are in `results/tables/`. In the tables, min clearance is the smallest lateral margin between the vehicle edge and the lane edge over a run (negative means the lane boundary was crossed); values are mean ± std over runs.

## Demonstrations

Closed-loop recordings of the proposed controller in the lead-braking group at the top speed of each map (Town03 at 60 km/h, Town04 at 90 km/h) under the three compound conditions. The complete set of full-resolution recordings is available on request.

| C1 dry, clear day | C2 wet, heavy rain, night | C3 snow, clear night |
|---|---|---|
| ![Town03 C1](gifs/Town03_C1_nominal.gif) | ![Town03 C2](gifs/Town03_C2_moderate_adverse.gif) | ![Town03 C3](gifs/Town03_C3_severe_adverse.gif) |
| ![Town04 C1](gifs/Town04_C1_nominal.gif) | ![Town04 C2](gifs/Town04_C2_moderate_adverse.gif) | ![Town04 C3](gifs/Town04_C3_severe_adverse.gif) |

*Top row: Town03 (urban, 60 km/h). Bottom row: Town04 (highway, 90 km/h).*

## Code release

The implementation code (safety envelope, VLM inference, LoRA fine-tuning, and the closed-loop CARLA pipeline) will be released here in a future update.

## Citation

```bibtex
@misc{yang2026vlmcase,
  title         = {VLM-CASE: vision-language model enabled context-adaptive safety envelopes for anticipatory safe autonom