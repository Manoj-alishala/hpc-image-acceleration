# 🖼️ Parallel Image Processing with OpenCV

A Python notebook demonstrating **serial vs. parallel grayscale conversion** and classical image filtering using OpenCV and NumPy. Benchmarks the speedup achieved by vectorized operations over pixel-level loops.

---

## 📌 Features

- **Serial grayscale conversion** — pixel-by-pixel loop using the luminance formula (`0.299R + 0.587G + 0.114B`)
- **Parallel grayscale conversion** — vectorized NumPy dot product (same formula, drastically faster)
- **Mean blur filter** — 5×5 averaging kernel via `cv2.filter2D`
- **Sobel edge detection** — gradient magnitude computed from X and Y Sobel responses
- **Speedup benchmark** — wall-clock timing comparison between serial and parallel approaches
- **Matplotlib visualization** — side-by-side display of Original, Grayscale, Blurred, and Edge images

---

## 🧰 Requirements

```bash
pip install opencv-python numpy matplotlib scikit-image requests
```

| Library        | Purpose                            |
|----------------|------------------------------------|
| `opencv-python`| Image filtering and Sobel operator |
| `numpy`        | Vectorized pixel operations        |
| `matplotlib`   | Visualization                      |
| `scikit-image` | Fallback sample image (`camera()`) |
| `requests`     | Downloading remote images          |

---

## 🚀 Usage

Run the notebook cell-by-cell in **Jupyter** or any compatible environment (VS Code, Google Colab, etc.).

```bash
jupyter notebook image_processing.ipynb
```

The script will:
1. Attempt to download a sample image from `picsum.photos`
2. Fall back to `skimage.data.camera()` if the download fails
3. Process and display all pipeline stages
4. Print the parallel speedup ratio

---

## 📊 Pipeline Overview

```
Raw Image (RGB)
      │
      ├──▶ Serial Loop Grayscale   (timed)
      │
      └──▶ Parallel NumPy Grayscale (timed)
                  │
                  ├──▶ Mean Blur (5×5 kernel)
                  │
                  └──▶ Sobel Edge Detection
                              │
                              └──▶ Gradient Magnitude = √(Gx² + Gy²)
```

---

## ⚡ Performance

The serial loop iterates over every pixel in Python — O(H × W) with interpreter overhead. The parallel approach uses a single NumPy matrix multiply, which delegates to optimized BLAS routines under the hood.

Expected speedup on a typical image (1200×800):

| Method   | Approx. Time |
|----------|-------------|
| Serial   | ~5–15 s     |
| Parallel | < 10 ms     |
| Speedup  | **~500–1500×** |

Actual numbers are printed at the end of execution.

---

## 🖼️ Sample Output

| Original | Grayscale | Blurred | Edges |
|----------|-----------|---------|-------|
| Color RGB image | Luminance-weighted | 5×5 mean | Sobel gradient |

---

## 📁 File Structure

```
├── image_processing.ipynb   # Main notebook
└── README.md
```

---

## 📄 License

MIT — free to use and modify.
