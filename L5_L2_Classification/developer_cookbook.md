# Developer Cookbook — K_RLVRWORLD
**Stack:** Python 3.11, PyTorch 2.10+, stable-baselines3, PAX 27B (reward verifier), AIOSS_FORMAT
**Domain:** RL with verifiable rewards for world model agents in Anticloud

## Train RL agent with PAX verifier
```python
from k_rlvrworld import RLVRTrainer

trainer = RLVRTrainer(
    env="AnticloudRobotEnv-v0",
    pax_verifier="./pax-27b-q4.gguf",
    algorithm="PPO",
    aioss_chain="./rlvr.aioss"
)

def pax_reward(obs, action, next_obs, task_spec):
    return trainer.pax_score(obs, action, next_obs, task_spec)

trainer.train(reward_fn=pax_reward, n_steps=1_000_000)
```

## AIOSS Chain Append
```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()
```
