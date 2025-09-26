# stock-prediction
Time Series Forecasting: Stacked LSTM for Stock Price Prediction
This project demonstrates a deep learning approach to forecasting future stock prices based on historical features (Open, High, Low, Close, Volume).
Project Goal 
The objective is to build a Stacked LSTM model to learn long-term dependencies within historical stock data and use an autoregressive technique to predict the stock's closing price 30 days into the future.
Methodology and Model ArchitectureModel:
A Stacked Long Short-Term Memory (LSTM) neural network was selected for its superior capability in handling sequence-to-sequence data and capturing complex temporal patterns, which are crucial in financial markets.
Preprocessing: The historical data was scaled using MinMaxScaler and transformed into 3D sequences (rolling windows) required for the LSTM input format (Samples, Timesteps, Features).
Forecasting Technique: Autoregressive Forecasting was employed to generate the future price sequence.Autoregressive Prediction Loop (Key Logic)The core strength of this project is the rolling window prediction loop, which simulates a real-world forecasting scenario
Prediction: The model uses the current 100-day window of prices to predict the price for the 101st day (y^​t+1​).
Window Roll: The oldest price point in the window is dropped.
Feedback: The newly predicted price (y^​t+1​) is immediately appended to the end of the window.
Iteration: This new 100-day window is fed back into the model to predict the price for the 102nd day, continuing for the entire 30-day forecast.
This feedback mechanism demonstrates robust time series analysis skills.
How to Run the ProjectThe project is contained within a single Google Colab notebook for easy, reproducible execution.
Open the Notebook: Open the Stock Price prediction.ipynb file in Google Colab.
Run All Cells: Execute all cells sequentially. 
The notebook handles data acquisition (yfinance), preprocessing, model training, evaluation, and the final 30-day autoregressive forecast.
