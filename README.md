# **📈 Stock Price Prediction using Multivariate LSTM (Google Colab Ready)**

This project implements an advanced recurrent neural network (Long Short-Term Memory, or LSTM) model for predicting the future closing price of a stock (AAPL in this case). The model is trained on a multivariate time series dataset, using Open, High, Low, Close, and Volume (OHLCV) as features.

This notebook is optimized for execution within **Google Colab**, requiring the data file to be uploaded or mounted via Google Drive.

## **🎯 Task Overview**

The goal was to build a robust model to predict future stock prices based on historical data. We chose a **Multivariate LSTM** architecture due to its superior capability in modeling temporal dependencies and complex relationships between multiple sequential features (OHLCV).

## **🚀 Key Features**

* **Multivariate Input:** Uses 5 features (open, high, low, close, volume) to predict the next day's closing price.  
* **Sequential Data Splitting:** Implements a strict time-based split (Train, Validation, Test) to prevent data leakage, a critical step for financial time series modeling.  
* **Correct Scaling:** MinMaxScaler is fit *only* on the training data, avoiding contamination from future information.  
* **Anti-Overfitting Measures:**  
  * **Dropout Layers:** Added to the LSTM network to randomly ignore neurons during training, enforcing regularization.  
  * **Early Stopping:** Utilizes the Keras EarlyStopping callback to automatically stop training when validation loss ceases to improve, restoring the best model weights.  
* **Future Forecasting:** Includes functions to predict the stock price for **10 days** and **30 days** beyond the historical data.

## **⚙️ Project Structure (Generated Files)**

The script generates **four** crucial output files. The table below lists the primary project files and the generated outputs:

| File | Description |
| :---- | :---- |
| AAPL.US\_D1.csv | The historical stock data file. |
| stock\_predictor.ipynb | The Jupyter Notebook containing all Python code logic. |
| README.md | This file. |
| **stock\_split\_visualization.png** | **Plot 1:** Visualizes the chronological split of the data (Train/Validation/Test). |
| **stock\_prediction\_full\_history.png** | **Plot 2:** Displays the actual prices versus the model's predictions over the full history. |
| **stock\_prediction\_10\_day\_forecast\_isolated.png** | **Plot 3:** The clean, isolated **10-day** future price forecast graph. |
| **stock\_prediction\_30\_day\_forecast\_isolated.png** | **Plot 4:** The clean, isolated **30-day** future price forecast graph. |

## **🛠️ Requirements**

To run this script, you need Python and the following libraries:

pip install numpy pandas scikit-learn tensorflow matplotlib

## **🧠 Model Architecture**

The core prediction engine is a two-layer LSTM with Dropout for regularization.

| Layer | Type | Output Shape | Notes |
| :---- | :---- | :---- | :---- |
| 1 | LSTM (100 units) | (None, 60, 100\) | input\_shape=(60, 5). Uses 60 time steps, 5 features. |
| 2 | Dropout (0.2) | (None, 60, 100\) | Regularization: 20% of connections dropped. |
| 3 | LSTM (100 units) | (None, 100\) | Converts sequence output to single vector. |
| 4 | Dropout (0.2) | (None, 100\) | Regularization: 20% of connections dropped. |
| 5 | Dense | (None, 1\) | Output layer predicting the next day's closing price. |

**Key Training Parameters:**

* **Time Step (Lookback):** 60 days  
* **Loss Function:** Mean Squared Error (MSE)  
* **Optimizer:** Adam  
* **Callback:** EarlyStopping (patience=15, restore\_best\_weights=True)

## **📊 Results and Evaluation**

The model's performance is measured using the **Root Mean Squared Error (RMSE)**. A lower RMSE indicates better predictive accuracy.

The training process is optimized by **Early Stopping**, which halts the process at the epoch where the validation loss is minimized, preventing the model from overshooting into the overfitting region.

### **Example Console Output:**

\--- Training Data Shape \---  
X\_train shape (samples, time\_steps, features): (4254, 60, 5\)

\--- Model Training Finished \---  
Model trained for a total of 84 epochs (optimal stop point determined by EarlyStopping).

Train RMSE: $0.4613   
Test RMSE: $56.7313 

10-Day Future Price Prediction: $90.4386  
30-Day Future Price Prediction: $88.8435

### **Generated Plots:**

The script generates **three** vital plots:

1. **stock\_prediction\_full\_history.png**: Displays the original stock price and the model's predictions on the training and testing segments.  
2. **stock\_prediction\_10\_day\_forecast\_isolated.png**: Displays the isolated 10-day future price forecast.  
3. **stock\_prediction\_30\_day\_forecast\_isolated.png**: Displays the isolated 30-day future price forecast.

## **🏃 How to Run the Project**

1. **Clone the Repository:**  
   git clone \[YOUR\_REPOSITORY\_URL\]  
   cd stock-price-prediction

2. **Ensure Data is Present:** Make sure AAPL.US\_D1.csv is in the root directory.  
3. **Run the Python Script:**  
   python stock\_predictor.py

The script will print the training progress, final RMSE scores, and the 10-day/30-day forecasts, and save the four required plots to the local directory.
