# Twitter Sentiment Analysis Using BiLSTM

## Project Overview

This project is an end-to-end Natural Language Processing (NLP) application that performs sentiment analysis on Twitter text. The system classifies tweets into one of three sentiment categories:

* Negative
* Neutral
* Positive

A Bidirectional Long Short-Term Memory (BiLSTM) deep learning model is trained on the Twitter_Data dataset and deployed through a Streamlit web application for real-time sentiment prediction.

---

## Dataset

**Dataset:** `Twitter_Data.csv`

The dataset contains Twitter posts along with their sentiment labels.

### Dataset Columns

| Column    | Description                                   |
| --------- | --------------------------------------------- |
| text      | Tweet content                                 |
| sentiment | Sentiment label (negative, neutral, positive) |

### Data Preprocessing

The following preprocessing steps were applied:

* Removed URLs
* Removed Twitter mentions (@username)
* Removed special characters and numbers
* Converted text to lowercase
* Removed extra spaces
* Removed missing values
* Filtered very short tweets

---

## Project Structure

```text
Twitter-Sentiment-Analysis/
│
├── Twitter_Data.csv
├── twitter_sentiment_main.py
├── twitter_sentiment_app.py
├── sentiment_model.h5
├── tokenizer.joblib
├── requirements.txt
└── README.md
```

---

## Model Training Pipeline

### 1. Data Loading and Cleaning

The dataset is loaded using Pandas and cleaned using custom text preprocessing functions.

### 2. Label Encoding

Sentiment labels are converted into numerical values:

| Sentiment | Label |
| --------- | ----- |
| Negative  | 0     |
| Neutral   | 1     |
| Positive  | 2     |

### 3. Train-Test Split

The dataset is divided into:

* 80% Training Data
* 20% Testing Data

Stratified sampling is used to preserve class distribution.

### 4. Text Tokenization

Tweets are converted into numerical sequences using Keras Tokenizer.

**Configuration:**

* Vocabulary Size: 20,000 words
* Maximum Sequence Length: 40 tokens

### 5. Sequence Padding

All sequences are padded to a fixed length of 40 tokens to ensure consistent input dimensions.

---

## Model Architecture

The sentiment classifier is built using TensorFlow/Keras.

```text
Embedding Layer (100 Dimensions)
            ↓
SpatialDropout1D (0.1)
            ↓
Bidirectional LSTM (128 Units)
            ↓
Dense Layer (64 Units, ReLU)
            ↓
Dropout (0.3)
            ↓
Output Layer (Softmax, 3 Classes)
```

### Training Configuration

| Parameter           | Value                           |
| ------------------- | ------------------------------- |
| Embedding Dimension | 100                             |
| LSTM Units          | 128                             |
| Batch Size          | 32                              |
| Epochs              | 15                              |
| Optimizer           | Adam                            |
| Loss Function       | Sparse Categorical Crossentropy |

### Additional Techniques

* Early Stopping
* Class Weight Balancing
* Validation Monitoring

---

## Model Evaluation

The model is evaluated on the test dataset using:

* Accuracy
* Precision
* Recall
* F1-Score
* Classification Report
* Confusion Matrix

These metrics help assess model performance across all sentiment classes.

---

## Saved Artifacts

After training, the following files are generated:

### sentiment_model.h5

Stores the trained BiLSTM model.

### tokenizer.joblib

Stores the fitted tokenizer used during training.

These files are loaded by the Streamlit application for inference.

---

## Streamlit Web Application

The project includes a Streamlit application (`twitter_sentiment_app.py`) for real-time sentiment prediction.

### Application Workflow

1. Load trained model (`sentiment_model.h5`)
2. Load tokenizer (`tokenizer.joblib`)
3. Accept user text input
4. Apply the same preprocessing used during training
5. Convert text into padded sequences
6. Generate sentiment prediction
7. Display:

   * Predicted Sentiment
   * Class Probabilities

### Example

**Input**

```text
I love this new phone. The camera quality is amazing!
```

**Output**

```text
Sentiment: Positive
```

**Probabilities**

```text
Negative: 0.03
Neutral: 0.07
Positive: 0.90
```

---

## Installation

### Clone Repository

```bash
git clone https://github.com/your-username/twitter-sentiment-analysis.git

cd twitter-sentiment-analysis
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Train the Model

```bash
python twitter_sentiment_main.py
```

This creates:

```text
sentiment_model.h5
tokenizer.joblib
```

---

## Run the Streamlit Application

```bash
streamlit run twitter_sentiment_app.py
```

Open the generated local URL in your browser and enter any tweet or text to analyze sentiment.

---

## Key Features

* Multi-class sentiment classification
* NLP-based text preprocessing
* Deep Learning using BiLSTM
* Class imbalance handling with class weights
* Early stopping to reduce overfitting
* Real-time prediction through Streamlit
* Model persistence using H5 and Joblib

---

## Skills Demonstrated

* Python
* Natural Language Processing (NLP)
* Deep Learning
* TensorFlow / Keras
* Bidirectional LSTM (BiLSTM)
* Text Preprocessing
* Data Cleaning
* Model Evaluation
* Streamlit Deployment
* Sentiment Analysis

---

## Future Enhancements

* Use pre-trained embeddings (GloVe, Word2Vec)
* Implement Transformer-based models such as BERT
* Hyperparameter optimization
* Real-time Twitter API integration
* Docker deployment
* Cloud deployment using AWS or Azure

---

## Author

**Shobhita Sisodia**

B.Tech Biotechnology | Aspiring Data Scientist | Machine Learning & AI Enthusiast
