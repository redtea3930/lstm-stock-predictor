## LSTM-stock-predictor


### Introduction
This excercise uses recursive nerual networks (RNN's) to use long short-term memory (LSTM) for value prediction on time series data. Specifically, taking several months of Bitcoing closing prices and "Crypto Fear and Greed" sentiment from [Alternative.me](https://alternative.me/crypto/fear-and-greed-index/#google_vignette) to attempt making an RNN predicting those prices, and evaluate the fear-and-greed sentiment vs closing prices in price prediction.

### Methods
Datasets of daily Bitcoin closing prices and fear-and-greed values over the same timeframe were provided, along with some starter code. A RNN was manually constructed for each dataset to predict closing values, several parameters of the RNN were tested using different values but identical final values were used for the RNN to evaluate both datasets. Two notebooks were made:
* [lstm_stock_predictor_closing](lstm_stock_predictor_closing.ipynb) RNN predicting Bitcoin closing price on historic Bitcoin closing price 
* [lstm_stock_predictor_fng](lstm_stock_predictor_fng.ipynb) RNN predicting Bitcoin closing price on "Fear and Greed" sentiment 

There were several parameters within the code were experimented with, with the following outcomes:
* window_size, the time frame in days of previous closing prices used to predict closing price. Lower values led to better predictions, the value was set to 1 for the final setup.
* number_units, the number of neurons in each level of the RNN. Surprisingly, higher values did not lead to better outcomes, I set this to 5 in the final setup
* dropout_fraction, the proportion of input units to be randomly set to zero during each update during training, thus preventing the RNN from training to closely on specific inputs and becoming overfit to the dataset. Higher dropout_fractions led to higher loss, I set this value to 0.1 in the final setup.
* epochs the number of times the entire training dataset is passed forward and backward through the neural network. Using higher numbers of epochs marginally decreased loss, but much less so than other parameter changes. I set the final value at 20.
* batch_size This parameter determines the number of samples that will be used in each iteration of training. Using any value larger than one increased loss

### Results
Each model was evaluated on loss and tracking to actual values. The window size for timeframe evaluation was also evaluated.
#### Loss:
Final loss values for the RNNs were:
lstm_stock_predictor_closing: 0.01371233444660902
lstm_stock_predictor_fng: 0.12138079851865768

Plots of the two model outputs show that lstm_stock_predictor_closing tracks actual Bitcoing prices well, and lstm_stock_predictor_fng tracks some rises and falls in price but does not track actual closing prices well at all. I believe the lower loss but worse tracking of lstm_stock_predictor_fng indicates overfitting.

Smaller window sizes, ie predicting values on smaller timescales for input values, led to lower loss and better value tracking. The smallest window size of 1 worked best.