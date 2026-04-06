# Lab-3.1-CNN-Fundamentals-Convolution-Pooling-Padding-Strides
This README covers the transition from standard neural networks to **Convolutional Neural Networks (CNNs)**. It explains how specialized layers process spatial information and provides a hands-on demonstration of image filtering and feature extraction.

---


In this lab, we step away from flattening images into long vectors. Instead, we treat images as 2D grids, allowing the model to preserve spatial relationships (like how pixels above and below each other form an edge).

## 🖼️ The Building Blocks of Vision

### 1. The Convolution Operation
The core of a CNN is the **Filter (or Kernel)**. A small matrix slides across the image, performing a dot product at each position.
* **Manual Demo:** The code implements a manual **Sobel-style filter** to detect vertical edges. By setting the weights to `[[1, 0, -1], [1, 0, -1], [1, 0, -1]]`, we highlight areas where pixel intensity changes horizontally.
* **Padding:** Adding a border of zeros around the image to ensure the output has the same dimensions as the input.
* **Stride:** The "step size" the filter takes. A stride of 2 skips every other pixel, effectively downsampling the image.



### 2. Pooling (Downsampling)
Pooling layers reduce the spatial size of the representation. 
* **MaxPooling:** Takes the maximum value in a window (e.g., $2 \times 2$). This makes the model "translation invariant"—it cares that a feature (like an eye) exists, even if its exact pixel position shifts slightly.
* **Result:** It reduces the number of parameters and computation in the network.



---

## 🏗️ Model Architecture: `SimpleCNN`

We build a classic vision hierarchy:
1.  **Conv Layer 1:** 32 filters to catch basic edges and textures.
2.  **ReLU & MaxPool:** Non-linearity and spatial reduction.
3.  **Conv Layer 2:** 64 filters to combine edges into more complex shapes.
4.  **Fully Connected (Linear) Layers:** The "classifier" head that takes the high-level features and maps them to the 10 FashionMNIST categories.

---

## 🔍 Visualizing the "Hidden" World

One of the most powerful parts of this lab is **Feature Map Visualization**. After training, we feed a single image into the first few layers and plot what the filters "see."

* **Early Layers:** You will notice some feature maps look like edge detectors, while others look like inverted versions of the original image.
* **Abstraction:** As you go deeper into a CNN, these maps become less recognizable to humans and more meaningful to the mathematical classifier.

---

## 📊 Summary of Implementation
* **Device Agnostic:** The code automatically detects and uses a **GPU (CUDA)** if available, significantly speeding up the training process.
* **Training:** Uses the **Adam optimizer** for 3 epochs, typically achieving over **90% accuracy**—a significant jump from simple linear models.
* **Evaluation:** Includes a robust accuracy function and a Matplotlib grid to display the model's internal activations.

---

## 🛠️ How to Use
1.  Run the manual convolution section to see how a specific kernel transforms a shoe or a shirt into an edge-map.
2.  Train the `SimpleCNN`.
3.  Observe the **Feature Maps** plot. Each square in the grid represents what one specific "neuron" in the first layer is looking for.

> **Key Takeaway:** CNNs don't just "learn weights"—they learn **visual filters**. This is why they are the foundation for almost all modern computer vision tasks, from facial recognition to autonomous driving.
