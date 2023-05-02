#


## VanillaRolloutStorage
[source](https://github.com/RLE-Foundation/Hsuanwu\blob\main\hsuanwu/xploit/storage/vanilla_rollout_storage.py\#L11)
```python 
VanillaRolloutStorage(
   observation_space: Union[gym.Space, DictConfig], action_space: Union[gym.Space,
   DictConfig], device: str = 'cpu', num_steps: int = 256, num_envs: int = 8,
   discount: float = 0.99, gae_lambda: float = 0.95
)
```


---
Vanilla rollout storage for on-policy algorithms.


**Args**

* **observation_space** (Space or DictConfig) : The observation space of environment. When invoked by Hydra,
    'observation_space' is a 'DictConfig' like {"shape": observation_space.shape, }.
* **action_space** (Space or DictConfig) : The action space of environment. When invoked by Hydra,
    'action_space' is a 'DictConfig' like
    {"shape": (n, ), "type": "Discrete", "range": [0, n - 1]} or
    {"shape": action_space.shape, "type": "Box", "range": [action_space.low[0], action_space.high[0]]}.
* **device** (str) : Device (cpu, cuda, ...) on which the code should be run.
* **num_steps** (int) : The sample length of per rollout.
* **num_envs** (int) : The number of parallel environments.
* **discount** (float) : discount factor.
* **gae_lambda** (float) : Weighting coefficient for generalized advantage estimation (GAE).


**Returns**

Vanilla rollout storage.


**Methods:**


### .add
[source](https://github.com/RLE-Foundation/Hsuanwu\blob\main\hsuanwu/xploit/storage/vanilla_rollout_storage.py\#L83)
```python
.add(
   obs: th.Tensor, actions: th.Tensor, rewards: th.Tensor, terminateds: th.Tensor,
   truncateds: th.Tensor, next_obs: th.Tensor, log_probs: th.Tensor,
   values: th.Tensor
)
```

---
Add sampled transitions into storage.


**Args**

* **obs** (Tensor) : Observations.
* **actions** (Tensor) : Actions.
* **rewards** (Tensor) : Rewards.
* **terminateds** (Tensor) : Terminateds.
* **truncateds** (Tensor) : Truncateds.
* **next_obs** (Tensor) : Next observations.
* **log_probs** (Tensor) : Log of the probability evaluated at `actions`.
* **values** (Tensor) : Estimated values.


**Returns**

None.

### .reset
[source](https://github.com/RLE-Foundation/Hsuanwu\blob\main\hsuanwu/xploit/storage/vanilla_rollout_storage.py\#L120)
```python
.reset()
```

---
Reset the terminal state of each env.

### .compute_returns_and_advantages
[source](https://github.com/RLE-Foundation/Hsuanwu\blob\main\hsuanwu/xploit/storage/vanilla_rollout_storage.py\#L125)
```python
.compute_returns_and_advantages(
   last_values: th.Tensor
)
```

---
Perform generalized advantage estimation (GAE).


**Args**

* **last_values** (Tensor) : Estimated values of the last step.
* **gamma** (float) : Discount factor.
* **gae_lamdba** (float) : Coefficient of GAE.


**Returns**

None.

### .sample
[source](https://github.com/RLE-Foundation/Hsuanwu\blob\main\hsuanwu/xploit/storage/vanilla_rollout_storage.py\#L151)
```python
.sample(
   num_mini_batch: int = 8
)
```

---
Sample data from storage.


**Args**

* **num_mini_batch** (int) : Number of mini-batches


**Returns**

Batch data.