Session 2, part IV: Exercise - Building a simple neural network using Keras and Tensorflow
================

Example of Keras workflow
-------------------------

### 1. Prepare Data

``` r
# Prepare data
# Scale features
# Define
x_train
y_train
x_test
y_test
```

(Note, splitting the data into a `train` and a `test` set is called cross validation, more on this later)

### 2. Define Architecture

We can define the architecture of an ANN with `4` input neurons, `4` neurons in the first hidden layer, `3` neurons in the second hidden layer and `3` output neurons like so:

``` r
model = keras_model_sequential()
model %>% 
  layer_dense(units = 4, activation = 'relu', input_shape = 4) %>% 
  layer_dense(units = 3, activation = 'softmax')
model %>% summary
```

This gives a total of 35 parameters to be fitted: 4 for each input neuron connected to the hidden layer, plus an additional 4 for the associated first bias neuron and 3 for each of the hidden neurons connected to the output layer, plus an additional 3 for the associated second bias neuron. I.e. `(4 * 4) + 4 + (4 * 3) + 3 = 35`

### 3. Compile Model

``` r
model %>% compile(
  loss      = 'categorical_crossentropy',
  optimizer = optimizer_rmsprop(),
  metrics   = c('accuracy')
)
```

### 4. Train the Model

``` r
history = model %>% fit(
  x = x_train, y = y_train,
  epochs           = 200,
  batch_size       = 20,
  validation_split = 0
)
```

### 5. Evaluate Model Performance

``` r
perf = model %>% evaluate(x_test, y_test)
```

Summary
-------

1.  Prepare Data
2.  Define Architecture
3.  Compile Model
4.  Train the Model
5.  Evaluate Model Performance
6.  Adjust hyperparameters and redo steps 1-5

Exercise: Keras TensorFlow on Iris
----------------------------------

1.  Goto [Building a simple neural network using Keras and Tensorflow](https://github.com/leonjessen/keras_tensorflow_on_iris)
2.  Copy the code to the editor of your choice
3.  Make sure the script can run
4.  Try running the script a few times without changing anything, do you get consistent results?
5.  Play around with hyperparameters and architecture
