# Deep Learning With Python
 
# 🧠 Deep Learning with Python – Practical Notebooks

This repository contains my hands-on implementation of code examples from the book **"Deep Learning with Python" by François Chollet**.

The goal of this project is to **understand, replicate, and document** the deep learning concepts explained in the book using Python, TensorFlow, and Keras.  
Each notebook corresponds to a specific chapter and includes both code and detailed explanations based on my personal learning process.

---

## ⚠️ Disclaimer

The code presented in this repository is **based on the original content from the book _Deep Learning with Python_** (by François Chollet).  
I do **not claim ownership** of the original code — my goal is to study, annotate, and demonstrate what I've learned by reproducing and expanding on it.

---

## 📘 Chapter Summaries

### 📗 Chapter 3 – *Introduction to Keras and TensorFlow*

This chapter introduces the core building blocks of TensorFlow and contrasts them with NumPy:

- Creating and inspecting tensors (`shape`, `dtype`, `rank`)
- Differences between TensorFlow and NumPy tensors (immutability vs. mutability)
- Using `tf.Variable` to create modifiable tensors
- Performing mathematical operations on tensors
- Computing gradients with `tf.GradientTape`
- Building a basic binary classifier from scratch using:
  - Synthetic, linearly separable 2D data
  - A simple prediction model: `y = Wx + b`
  - Manual implementation of:
    - Forward pass
    - Mean squared error loss
    - Gradient descent optimization loop
  - Visualizing the dataset and decision boundary with `matplotlib`

This chapter lays the groundwork for understanding how deep learning models operate under the hood.

---

### 📘 Chapter 4 – *Getting Started with Neural Networks: Classification and Regression*

#### 🔹 Part 1: Binary Classification – Sentiment Analysis on IMDB Reviews

In this notebook, we tackle a **binary classification problem** using a neural network.

- **Dataset:** [IMDB Movie Reviews](https://keras.io/api/datasets/imdb/) — 50,000 reviews labeled as *positive* or *negative*.
- Reviews are preprocessed into sequences of integers (each representing a word index).
- Labels are binary values (0 = negative, 1 = positive).

We go through the full pipeline:

- 🔄 **Decoding reviews**: Rebuilding text from word indices using the IMDB word index.
- 🔢 **Vectorization (Multi-hot Encoding)**: Converting variable-length reviews into uniform-size boolean vectors of length 10,000 (vocabulary size).
- 🧠 **Model architecture**: 
  - Two hidden `Dense` layers with 16 units and ReLU activation
  - Final output layer with a single unit and sigmoid activation
- ⚙️ **Compilation details**:
  - Optimizer: `rmsprop`
  - Loss: `binary_crossentropy`
  - Metrics: `accuracy`

We also explore **validation**, **overfitting**, and **model tuning**:

- Training vs. validation loss plotted across 20 epochs
- Experimented with:
  - Different number of units (8, 16, 64)
  - Activation functions (ReLU, `tanh`)
  - Loss functions
  - ⚠️ Still resulted in overfitting...

💡 **Solution tested:** Dropout regularization (50%)  
Result: The model started to stabilize and generalize better!

📈 Visual analysis helps understand when the model starts to overfit and how architectural changes impact learning.

#### 🔹 Part 2: Multi-class Classification – Reuters Newswire Topics

In this notebook, we explore a **multi-class single-label classification** task using the Reuters dataset.

- **Dataset:** [Reuters newswire topics](https://keras.io/api/datasets/reuters/)
- Contains **11,228 newswires** classified into **46 distinct topics**.
- Each sample belongs to **only one class** (single-label).

🧾 **Data loading & preprocessing**:
- Inputs are pre-tokenized sequences of integers.
- Decode with `reuters.get_word_index()` for raw text reconstruction.
- Vectorize input using multi-hot encoding
  
🧪 **Architecture Variants**: 
 - 🔸 Two hidden `Dense` layers with 64 units and ReLU activation.
  - Final output layer with 46 units and softmax activation
  - Optimizer: `rmsprop`, Loss: `categorical_crossentropy`, metrics: `accuracy`
    - Average accuracy ~80%.
 - 🔸 Bottleneck (only 4 units in the two hidden Dense Layer)
   - Drops accuracy to ~71% due to limited capacity.
  - 🔸 Larger Network (128 units in the two hidden Dense Layer)
    - Slight boost: ~82–83% accuracy.
    
🔍 **Grid Search for Hyperparameter Tuning**
- Automatically selects the best combination of hyperparameters.
- **Best results with: adam, 128 units, relu, dropout 0.5.**
- **Achieves ~83% accuracy with better generalization.**
---

More chapters will be added as I progress through the book 📚
