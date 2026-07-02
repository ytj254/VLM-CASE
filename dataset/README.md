# Scene-context dataset

10,560 CARLA front-camera frames (1280×720), each labeled with four scene-context fields:

| Field | Labels |
|---|---|
| `road_surface` | dry, wet, snow |
| `weather` | clear, heavy_rain, dense_fog |
| `time_of_day` | day, night |
| `illumination_assistance` | none, partial, strong |

Snow surfaces are produced by overlaying a snow/slush texture on the road (CARLA has no native snow), with tire friction reduced accordingly.

**Splits:** 8,448 train / 1,056 validation / 1,056 test, stratified over the joint distribution of the four fields.

**Download:** [ytj254/VLM-CASE_carla_dataset](https://huggingface.co/datasets/ytj254/VLM-CASE_carla_dataset) on Hugging Face. The dataset contains the frames plus JSONL label files (one record per frame: image path and the four fields).
