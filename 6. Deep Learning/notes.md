# To prevent overfitting, we need to know how to identify it.
Usually, we will be able to spot overfitting by dividing our available data into 3 subsets. (80:10:10 or 70:20:10 typically used)
1. Training
2. Validation - helps us prevent overfitting
3. Test - Measures the final predictive power of the model

# This is how it works:
All the training is done on the training set. 
In other words, we update the weights for the training set only.
Every once in awhile, we stop training.

We use the somewhat trained model and apply it to the validation data set.
This time, we run it without updating the weights, so we only propagate forward, not backward. 
In otherwords we only calculate its loss function.

On average, the loss function calculated for the validation set should be the same as the one for the training set.
This is because both training and validation sets were extracted from the same initial data set containing the perceived dependencies.
Normally, we would perform this operation many times in the process of creating a good machine learning algorithm.

The two loss functions we calculate are referred to as training loss and validation loss.
Since the data in the training set is trained using gradient dissent, each subsequent loss will be lower or equal to the previous one.

This is where validation loss comes into play.
At some point, the validation loss could start increasing. This means we are overfitting.
Although we are getting better at predicing the training set, we are moving further away from the overall logic on the data.
At this point, we should stop training the model.

# But what if our dataset is too small?
N-Fold Cross-Validation combines the train and validation sets in a clever way.

Say we have a dataset containing 11,000 observations. Save 1000 observations for test, we are left with 10,000 observations.
We want to train on 9000 data points and validate on 1000. We will split the remaining data into 10 subsets containing 1,000 observations each.
We fold it 10 times, so this is a 10-fold cross validation.
We treat one subset as a validation set while the other nine combined as a training set in each epoch. (We dont overlap training and validation in each epoch.)

This comes at a price as we have still trained on the validation set, which is not a good idea.
IT is less likely that the overfitting flag is raised and it is possible that we over fitted a bit.
The tradeoff is between not having a model or having a model that's a bit overfitted.

N-Fold Cross-Validation solves the scarce data issue but should by no means be used as the norm.

# Early Stopping Mechanism
- Simplest way: Train for a preset number of epochs.
Pros: 
1. Eventually solves the problem
Cons: 
1. No guarantee that the min has been reached
2. Might not have minimized at all (High enough learning rate might cause loss to diverge to infinity)
3. Naive

- Early Stopping - Stops when updates become too small (Common rule of thumb is to stop when the relative decrease in the loss function becomes less than 0.001)
Pros:
1. We are sure the loss is minimized
2. Saves computing power
Cons:
1. Might still cause overfitting

- Validation Set Strategy
Pros:
1. Solves the problem
2. Certain that loss is minimized
3. Prevents overfitting
Cons:
1. Can take the algorithm a long time to overfit as the weight may barely move

It is best practice to use a combination of both *Updates too small* and *Validation Set* strategies
Rule to follow: Stop when the validation loss starts increasing or when the training loss becomes very small

# Initialization
In our previous minimal example, we used uniformly random initializers for our weights and biases
We could choose a normal initializer with basically the same idea.
Both methods are somewhat problematic although they were the norm until 2010.
The problem is that non-linearities are essential for deep nets.
For example, we want a wide range of inputs for a sigmoid activator.
These inputs depend on weights that have to be initialized in a reasonable range so that we can have a nice variance along the linear combinations.

(Xavier) Glorot Initialization

Xavier initialization proposes the main idea that the method used for randomization isn't so important.
Rather, it is the number of outputs in the following layer that does.
With the passing of each layer, the Xavier initialization maintains the variance within some bounds so we can take full advantage of activation functions.

The uniform Xavier initialization states that we should draw each weight W from a random uniform distribution in the range from (-X, X), 
where X is equal to the square root of six divided by the number of inputs plus the number of outputs for the transformation.

For the normal Xavier initialization, we draw each weight W from a normal distribution with a mean of zero and a standard deviation equal to two divided by the number of inputs plus the number of outputs for the transformation.

The numerator values two and six vary across sources but the idea is the same. (?)

The higher the number of outputs, the higher the need to spread weights.
Since optimization is done through back propagation, we will also need spread weights given more inputs.

In TensorFlow, this is the default initializer, unlike what we did in the minimal example.

# Optimization
Clumsiest Optimizer: Gradient Descent
Slow in moving down the gradient through updating weights once per epoch.
*One Epoch is when an ENTIRE dataset is passed forward and backward through the neural network only ONCE.

Solution: Stochastic Gradient Descent (SGD)
Updates weights in real time inside a single epoch.
The SGD is closely related to the concept of batching, which is the process of splitting data into end batches (often called mini batches).
We update weights after every batch instead of every epoch.
That is, for 10,000 training points, and a batch size of 1000, we will have 10 batches per epoch.
For every full iteration over the training data set, the weights will be updated 10 times instead of once.
A minor cost to SGD is that it might approximate things a bit and slightly decrease accuracy, but the trade off is worth it.

Local Minimum Pitfall -> Momentum
Conventional to set Momentum Coefficient hyperparameter (alpha) = 0.9

Learning Rate Schedules / How to Choose the Optimal Learning Rate

Instead of using a simple rule to adjust the learning rate, consider these types of adaptive learning rates:
1. AdaGrad (adaptive gradient algorithm)
   - proposed in the 2011
   - dynamically varies the learning rate at each update and for each weight individually
2. RMSProp (root mean square propagation)
   - similar to AdaGrad with a different G function
3. *Adam (Adaptive Moment Estimation)*
   - state-of-the-art optimization algorithm
   - steps on RMSProp and introduces momentum into equation

# Preprocessing