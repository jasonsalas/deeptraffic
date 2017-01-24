# deeptraffic
This is my initial submmission for [MIT's self-driving car course](http://selfdrivingcars.mit.edu/) project on deep reinforcement learning, [Deep Traffic](http://selfdrivingcars.mit.edu/deeptrafficjs/). 

This JavaScript code trains a pre-built neural network by tweaking various parameters in order to have an automotive agent drive optimally and maintain a rate of speed just over the speed limit of 70MPH. My submission didn't crack the [course's leaderboard](http://selfdrivingcars.mit.edu/leaderboard/), but I did get the net to run stable at an average velocity of 70.66 MPH. (The [10th-highest score](http://selfdrivingcars.mit.edu/leaderboard/) hit 74.04 MPH, so clearly I can make this work better.) 

### My code
Here are [the adjustments](https://github.com/jasonsalas/deeptraffic/blob/master/net.js) I made to the default JavaScript code, to lines 5-8:
~~~~
lanesSide = 4;
patchesAhead = 10;
patchesBehind = 8;
trainIterations = 100000;
~~~~

...and to line 24...
~~~~
num_neurons: 40,
~~~~

### Noteworthy behavior patterns
What's most interesting about this project is how the car behaves. When modifying the JS variables at the top of the script (you really only need to mess with the _lanesSide_, _patchesAhead_, _patchesBehind_, and _trainIterations_ value, and then based on those adjustments, look at the number of inputs the net expects and then modify the number of neurons for the [reLU](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)) layer(s) as the activation functio.

In [my own tinkering](https://github.com/jasonsalas/deeptraffic/blob/master/net.js) with tweaking the neural net params, two distinct behaviors became apparent by the car among the traffic:

* With minimal adjustments to the default values, the car tends to "hug the rail" - meandering over to the extreme leftmost or rightmost lanes and staying there. Intuitively, since this is a reinforcement network, the AI agent is being rewarded for avoiding traffic jams and being able to accelerate, but once it makes its way to the outer lanes will hide out there. Overfitting, perhaps?
* With more extreme adjustments - modifications to the parameter values that aren't in balance - the car will avoid traffic proactively, but when driving in a straight line andwill tend to oscillate, and bob-&-weave between open lanes. I think this is akin to the learning rate being set too high/low. 

The behaviors noted above are interesting, being similar to findings from students in Udacity['s Self-Driving Car nanodegree program](https://www.udacity.com/drive), who [reported that](https://medium.com/@acflippo/cloning-driving-behavior-by-augmenting-steering-angles-5faf7ea8a125#.mxypzm1fp) simulated steering challenge data proved implied that machine learning-trained steering handling curves better than human drivers...but was very sketchy when driving for extended straight lines.

Generally, though, the car learns to handle traffic obstacles fairly well.

### Further work
Because this is a client-side implementation of a neural network, I wasn't able to use more advanced machine learning frameworks (Weka, H20, TensorFlow, etc.) to do grid search to optimize the hyperparameters. But manually turning the knobs is part of the educational process, so it's not a biggie.
