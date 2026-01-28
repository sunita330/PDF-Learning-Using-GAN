# Learning Probability Density Functions using GAN

## Dataset
The dataset used in this assignment is the India Air Quality Dataset obtained from Kaggle.  
NO₂ concentration is used as the feature variable.

Dataset link:  
https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data

---

## Objective
To learn the probability density function of a transformed random variable using only data samples.  
No analytical form of the distribution is assumed. A Generative Adversarial Network (GAN) is used to implicitly learn the distribution.

---

## Step 1: Data Transformation
The original feature (x) (NO₂ concentration) is transformed into (z) using a roll-number-dependent non-linear function:

z = x + a_r*sin(b_r x)

Where:
- Roll number ( r = 102303814 )
- ( a_r = 0.05 (r mod 7) = 0.20)
- ( b_r = 0.3 (r mod 5 + 1) = 1.5)

After transformation, the data is normalized for stable GAN training.

---

## Step 2: GAN Architecture

### Generator
The generator maps Gaussian noise (epsilon sim N(0,1)) to the data space using fully connected layers with ReLU activation.

Architecture:
- Dense(1 → 32)
- ReLU
- Dense(32 → 32)
- ReLU
- Dense(32 → 1)

### Discriminator
The discriminator is a binary classifier that distinguishes real samples from generated samples.

Architecture:
- Dense(1 → 32)
- ReLU
- Dense(32 → 32)
- ReLU
- Dense(32 → 1)
- Sigmoid

---

## Step 3: Training Procedure
- The discriminator is trained to classify real and fake samples correctly.
- The generator is trained to fool the discriminator.
- Binary Cross-Entropy loss is used.
- Adam optimizer with learning rate 0.001 is applied.
- Training is performed for 1500 epochs.

---

## Step 4: PDF Approximation
After training, samples are generated from the generator network. 
The probability density function is approximated using histogram density estimation, as permitted in the assignment.

---

## Results
The histogram of GAN-generated samples closely follows the histogram of the real transformed data.  
This indicates that the GAN has successfully learned the underlying data distribution.

---

## Observations

- **Mode Coverage:**  
  The generator captures the main modes of the transformed distribution.

- **Training Stability:**  
  Loss values stabilize after initial epochs, indicating stable training.

- **Quality of Generated Distribution:**  
  Generated samples closely match the real data distribution.

---

## Conclusion
The GAN successfully learns the probability density function of the transformed variable using data only, without assuming any parametric form.
