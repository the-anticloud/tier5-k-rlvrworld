# Deploy Guide — K_RLVRWORLD
**Tier:** TIER_5_WORLD_NEURO_EMBODIED | **Stack:** Python 3.11, PyTorch 2.10+, stable-baselines3, PAX 27B (reward verifier), AIOSS_FORMAT
**Air-gap capable after initial setup.**

## Prerequisites
Python 3.11+, PyTorch 2.10+, stable-baselines3 2.3+, PAX 27B weights. A100 for training.

## Environment
A100 for fast RL training. T4 for evaluation. 32GB RAM.

## AIOSS Integration
```bash
aioss init --module K_RLVRWORLD --output ./k_rlvrworld.aioss
aioss append --chain ./k_rlvrworld.aioss --payload ./output.bin --module K_RLVRWORLD
aioss verify --chain ./k_rlvrworld.aioss
```

## Air-Gap Setup
```bash
pip download -r requirements.txt -d ./wheels/
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX 27B Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(
    model_path="./pax-27b-q4.gguf",
    module="K_RLVRWORLD",
    aioss_chain="./K_RLVRWORLD.aioss",
    classification="L5_NARROW_L2_GENERAL"
)
result = harness.process(input_data)
```

## Verification
```bash
aioss verify --chain ./K_RLVRWORLD.aioss --verbose
python -m K_RLVRWORLD.tests.smoke
```
