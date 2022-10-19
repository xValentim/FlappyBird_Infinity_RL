# Flappy Bird With Neural Network Policy

This is a simple implementation of Flappy Bird using gym Environment and a Neural Network Policy. The Neural Network Policy is trained using the Genetic Algorithm and Proximal Policy Optimization (PPO) algorithm. The Genetic Algorithm is used to select the best Neural Network Policy from a population of Neural Network Policies. The Proximal Policy Optimization (PPO) algorithm is used to train the Neural Network Policy with Policy Gradient methods. 

We will to train with both methods and will compare the results. Our objective is to train the Neural Network Policy to play Flappy Bird for as long as possible, in other words, to get the highest score and never die! 

<p align="center">
<img src="flappy_infinity.png" width=250>
</p>

## Requirements

First, you need to install the requirements. You can do this by running the following command:

    pip install -r requirements.txt


## Flappy Bird Environment

We will to use Environment provided by `https://github.com/Talendar/flappy-bird-gym`. This Environment is a simple implementation of Flappy Bird using gym Environment. The Environment is very simple and it is easy to understand. For this implemantation we will use the `FlappyBird-v0` Environment and will to change dificult of the game to `easy`. The model can be trained with the `hard` dificult, but it will take a lot of time to train. So, we will change `_get_random_pipe()` (you can find in `game_logic.py` file) in flappy-bird-gym implementation to reduce random range of pipes. This will to turn much more easy to train the model. Change the function and fill with the following code:
```
    def _get_random_pipe(self) -> Dict[str, int]:
        """ Returns a randomly generated pipe. """
        # y of gap between upper and lower pipe
        gap_y = random.randrange(0,
                                 int(self.base_y * 0.6 - self._pipe_gap_size)//10)
        gap_y += int(self.base_y * 0.2)

        pipe_x = self._screen_width + 100
        return [
            {"x": pipe_x, "y": gap_y - PIPE_HEIGHT},          # upper pipe
            {"x": pipe_x, "y": gap_y + self._pipe_gap_size},  # lower pipe
        ]
```

Finally, just reinstall locally this environment with the following command:

    pip install -e . --force-reinstall

## Usage

If everything is ok, you can run the notebook `model_trained.ipynb` and see the results.

## Neural Network Policy

In here, we will to use a simple Neural Network Policy trained. You can just to load the model and play with it. This model was trained using Genetic Algorithm and Proximal Policy Optimization. In this repo, we just use model trained. In soon, we will to train the model step by step and we will consider problems like a local minimum. Modern methods like Proximal Policy Optimization (PPO) can stuck in local minimum because Policy Gradient Methods are very sensitive to local minimum. In other words, we can train policy using both algorithms. First, we use Genetic Algorithm to scape of local minimum and then we use Proximal Policy Optimization to train the policy for the rest of simulation.

## Aknowledgements

Thanks to `@Talendar` for the Flappy Bird Environment. 

Link to the repo: `https://github.com/Talendar/flappy-bird-gym`