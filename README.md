# VirtualTaobao

This project provides VirtualTaobao simulator trained from the real-data of [Taobao](http://taobao.com), one of the largest online retail platform. In Taobao, when a customer entered some query, the recommondation system returns a list of items according to the query and the customer profile. The system is expected to return a good list such that customers will have high chances of clicking the items. 

Using VirtualTaobao simulator, one can access a "live" environment just like the real Taobao environment, which can be useful for recommondation system research. Virtual customer will be generated once at a time, the virtual customer starts a query, and the recommendation system needs to return a list of items. The virtual customer will decide if it would like to click the items in the list, similar to a real customer.

How VirtualTaobao was trained is described in 
> Jing-Cheng Shi, Yang Yu, Qing Da, Shi-Yong Chen, and An-Xiang Zeng. [Virtual-Taobao: Virtualizing real-world online retail environment for reinforcement learning](https://arxiv.org/abs/1805.10000). In: Proceedings of the 33rd AAAI Conference on Artificial Intelligence (AAAI’19), Honolulu, HI, 2019. 

Anyone can this simulator freely, but should give credit to the above reference.

### Installation

```bash
pip install -e .
```

### What will happen when a user raises a query?
1. Several items related to the query were callbacked to form an itemset.
2. The agent assigns a weight to each attribute of the item.
3. Platform calculate item values according to the weight vector and select 10 items with the highest value.
4. Those items are pushed to the user, and user may click on some items(reward++), browse next page (so the agent need to decide new weight vector) or leave the platform.

### Usage for Supervised Learning


### Usage for Reinforcement Learning

```python
import gym
import virtualTB

env = gym.make('VirtualTB-v0')
print(env.action_space)
print(env.observation_space)
print(env.observation_space.low)
print(env.observation_space.high)
state = env.reset()
while True:
    env.render()
    action = env.action_space.sample()
    state, reward, done, info = env.step(action)
    
    if done: break
env.render()
```