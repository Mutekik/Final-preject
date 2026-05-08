# Final-preject
final project notbook
# Final Project

This repository contains the code and experiment files for my final project.


## Files

- `basemodel, lora4, no train, 200 s...`
  - Initial baseline and early testing notebook.

- `LoRA r=4, ep=2 full training.ipynb`
  - Full training notebook for the LoRA rank 4 experiment.

- `LoRA r=4, ep=2 full training, resu...`
  - Results of the LoRA rank 4 experiment.

- `lora_r8_ep3, full training.ipynb`
  - Full training notebook for the LoRA rank 8 experiment.

- `lora_r8_ep3, full training, result s...`
  - Results of the LoRA rank 8 experiment.

- `dora_r8_ep3_final, full training.ipy...`
  - Final full training notebook using DoRA rank 8.

- `dora_r8_ep3_final, full training, re...`
  - Results of the final DoRA rank 8 model.

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

- Adapter method: DoRA
- Rank: 8
- Epochs: 3
- Learning rate: 2e-4
- Trainable parameters: approximately 4.62M
- Public leaderboard score: 0.82293

## Notes

Some experiment settings were inspired by discussions and suggestions from classmates and the TA on EdStem. Final model training, validation checks, and submissions were run and verified by me.
