<p>
<img src="https://img.shields.io/badge/licence-MIT-green">
<img src="https://img.shields.io/badge/dependencies-up%20to%20date-brightgreen">
<a href="https://github.com/psf/black"><img alt="Code style: black" src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>
</p>

# MuZero General: WINDOWS PORT

## This is a windows port of [Duvaud et al's MuZero implementation](https://github.com/werner-duvaud/muzero-general)

Implementation Changes:

I have used torch multiprocessing instead of ray, and made a few sacrifices of correctness for speed in implementing the asynchronous communications between processes.a

In general, where ray requests a response from another process, I have made the processes just queue answers instead.
This means the responses are slightly stale.
This means I don't reprodue exactly the same results, but the performance on par.

API Changes:
- shared storage is deprecated in favour of setting up queues in the config.
As such it's easiest to just inherit from the base config class when creating new games

**I do not plan on updating this with their new features. [please use their official repo](https://github.com/werner-duvaud/muzero-general)**

A commented and [documented](https://github.com/werner-duvaud/muzero-general/wiki/MuZero-Documentation) implementation of MuZero based on the Google DeepMind [paper](https://arxiv.org/abs/1911.08265) and the associated [pseudocode](https://arxiv.org/src/1911.08265v1/anc/pseudocode.py).
It is designed to be easily adaptable for every games or reinforcement learning environments (like [gym](https://github.com/openai/gym)). You only need to edit the [game file](https://github.com/werner-duvaud/muzero-general/tree/master/games) with the parameters and the game class. Please refer to the [documentation](https://github.com/werner-duvaud/muzero-general/wiki/MuZero-Documentation) and the [example](https://github.com/werner-duvaud/muzero-general/blob/master/games/cartpole.py).

MuZero is a model based reinforcement learning algorithm, successor of AlphaZero. It learns to master games without knowing the rules. It only knows actions and then learn to play and master the game. It is at least more efficient than similar algorithms like [AlphaZero](https://arxiv.org/abs/1712.01815), [SimPLe](https://arxiv.org/abs/1903.00374) and [World Models](https://arxiv.org/abs/1803.10122). See [How it works](https://github.com/werner-duvaud/muzero-general/wiki/How-MuZero-works)

## Features

* [x] Fully connected network in [PyTorch](https://github.com/pytorch/pytorch)
* [x] Multi-Threaded with [Ray](https://github.com/ray-project/ray)
* [x] CPU/GPU support
* [x] TensorBoard real-time monitoring
* [x] Single and multiplayer mode
* [x] Commented and [documented](https://github.com/werner-duvaud/muzero-general/wiki/MuZero-Documentation)
* [x] Easily adaptable for new games
* [x] [Examples](https://github.com/werner-duvaud/muzero-general/blob/master/games/cartpole.py) of board and Gym games (See [list below](https://github.com/werner-duvaud/muzero-general#games-already-implemented-with-pretrained-network-available))
* [x] [Pretrained weights](https://github.com/werner-duvaud/muzero-general/tree/master/pretrained) available
* [ ] Play against MuZero mode with policy and value tracking 
* [ ] Residual Network
* [ ] Atari games

## Games already implemented with pretrained network available

* Cartpole
* Lunar Lander
* Connect4

## Demo

All performances are tracked and displayed in real time in tensorboard :

![lunarlander training preview](https://github.com/werner-duvaud/muzero-general/blob/master/docs/cartpole_training_summary.png)

Testing Lunar Lander :

![lunarlander training preview](https://github.com/werner-duvaud/muzero-general/blob/master/docs/lunarlander_training_preview.png)

## Getting started
### Installation

```bash
cd muzero-general
pip install -r requirements.txt
```

### Training

Edit the end of muzero.py:
```python
muzero = Muzero("cartpole")
muzero.train()
```
Then run:
```bash
python muzero.py
```
To visualize the training results, run in a new terminal:
```bash
tensorboard --logdir ./
```

### Testing

Edit the end of muzero.py:
```python
muzero = Muzero("cartpole")
muzero.load_model()
muzero.test()
```
Then run:
```bash
python muzero.py
```

## Authors

* Werner Duvaud
* Aurèle Hainaut
* Paul Lenoir
