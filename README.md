# Final Project

This repository contains the code, experiment notebooks, and final inference notebook for my DL Vision Challenge final project.

The task is to predict the correct answer choice for multimodal science questions using the provided image, question text, answer choices, and optional context fields such as lecture and hint.

## Files

- `basemodel, lora4, no train, 200 s...`
  - Initial baseline and early testing notebook.
  - Used for data inspection, image-path debugging, prompt testing, zero-shot inference, and small-sample smoke testing.

- `LoRA r=4, ep=2 full training.ipynb`
  - Full training notebook for the LoRA rank 4 experiment.

- `LoRA r=4, ep=2 full training, resu...`
  - Result and submission notebook for the LoRA rank 4 experiment.

- `lora_r8_ep3, full training.ipynb`
  - Full training notebook for the LoRA rank 8, 3-epoch experiment.

- `lora_r8_ep3, full training, result s...`
  - Result and submission notebook for the LoRA rank 8 experiment.

- `dora_r8_ep3_final, full training.ipy...`
  - Final full training notebook using DoRA rank 8.

- `dora_r8_ep3_final, full training, re...`
  - Final offline inference and submission notebook for the DoRA rank 8 model.
  - This notebook loads the local base model and the trained DoRA adapter, then generates `submission.csv`.

## Methods

The main experiments included:

1. A baseline setting without full adapter training.
2. LoRA with rank 4.
3. LoRA with rank 8.
4. DoRA with rank 8.

For the adapter-based experiments, I applied adapters to both attention and MLP projection layers, including:

- `q_proj`
- `k_proj`
- `v_proj`
- `o_proj`
- `gate_proj`
- `up_proj`
- `down_proj`

The final model used DoRA with rank 8 because it achieved the best public leaderboard score among my experiments while staying under the 5 million trainable-parameter limit.

## Final Model

The final selected model was:

- Base model: `SmolVLM-500M-Instruct`
- Adapter method: DoRA
- Rank: 8
- Epochs: 3
- Learning rate: 2e-4
- LoRA alpha: 16
- Dropout: 0.05
- Trainable parameters: approximately 4.62M
- Public leaderboard score: 0.82293

## How to Reproduce the Final Submission

1. Open the final offline inference notebook.

2. Add the competition dataset as a Kaggle input.

3. I provided the local SmolVLM base model and the trained adapters for each experimental setting in the model weights folder:

   https://drive.google.com/drive/folders/11w_zBPtXCSdEur-t-gIt7l7lSiwconrz

4. Download or add the required base model and adapter files to the Kaggle notebook input.

5. In the notebook, replace the model paths with the paths corresponding to your Kaggle input location. In my Kaggle notebook, the paths were:

   ```python
   BASE_MODEL_DIR = "/kaggle/input/models/mutekik/base/other/default/1"
   DORA_ADAPTER_DIR = "/kaggle/input/models/mutekik/r8-ep3-dor/other/default/1"
## Training and Inference Structure

The training notebooks are used to train and save adapters. The final offline inference notebook does not train the model. It only loads the local base model and the selected DoRA adapter to generate `submission.csv`.

This separation was used to make sure the final notebook could run in the required offline evaluation setting.

## Training Diagnostics

Training loss logs were recorded during adapter fine-tuning. The final report includes the training configurations and leaderboard results. If available, the training loss curve or training log screenshot is included in the repository for reference.

## Notes

Some experiment settings were inspired by discussions and suggestions from classmates and the TA on EdStem. These included expanding adapter targets to both attention and MLP projection layers, trying DoRA, and keeping the trainable parameter count below the 5 million limit.

Final model training, validation checks, adapter loading, and submissions were run and verified by me.
