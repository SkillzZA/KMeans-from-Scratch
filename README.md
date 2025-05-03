# K-Means from Scratch for Ishihara Test Analysis

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/SkillzZA/KMeans-from-Scratch/blob/main/CVL3.ipynb) 
<!-- Optional: Replace YOUR_USERNAME/YOUR_REPOSITORY/blob/main/ishihara_kmeans.ipynb with the actual URL to your notebook on GitHub -->

This repository contains a Google Colab notebook (`.ipynb`) that implements the K-Means clustering algorithm purely from scratch using Python and NumPy. It then applies this implementation to Ishihara color blindness test images to demonstrate color quantization and attempt heuristic extraction of the hidden numbers based on color clusters.

## Features

*   **K-Means from Scratch:** A `KMeans` class implementing the core logic:
    *   Initialization (random centroid selection)
    *   Assignment Step (assigning points to nearest centroid)
    *   Update Step (recalculating centroids)
    *   Convergence Check (based on centroid movement tolerance)
    *   Prediction method
*   **Image Processing:** Loads images, handles basic preprocessing (normalization, reshaping), and manages RGB color channels.
*   **Color Quantization:** Reduces the number of colors in an image to `k` dominant colors found by the K-Means centroids.
*   **Visualization:** Uses Matplotlib to display the original image, the color-quantized image, and a potential mask highlighting the cluster identified as the hidden number.
*   **Heuristic Number Extraction:** Provides a simple interactive method to identify which color cluster likely corresponds to the number within the Ishihara plate and generates a binary mask for that cluster.
*   **Colab Integration:** Uses `google.colab.files` for easy image uploading directly within the notebook environment.

## Example Result

![Example K-Means Result on Ishihara Plate](result.png) 
## How it Works

1.  **Image Loading:** An Ishihara test image is uploaded and loaded.
2.  **Preprocessing:** The image is converted to a 2D array where each row is a pixel and columns represent RGB color values. Values are typically normalized to the [0, 1] range.
3.  **K-Means Clustering:** The `KMeans` algorithm is run on the pixel data. It iteratively groups pixels with similar colors together by:
    *   Assigning each pixel to the nearest cluster centroid (based on color distance).
    *   Updating each centroid to be the average color of all pixels assigned to it.
4.  **Quantization:** A new image is created where each pixel's original color is replaced by the color of the centroid it was assigned to. This visually segments the image based on the `k` dominant colors.
5.  **Number Identification (Heuristic):** Since the dots forming the hidden number usually have a distinct color range compared to the background dots, they should ideally fall into one (or a small number) of the `k` clusters. By observing the quantized image and the centroid colors, the user identifies the cluster index most likely representing the number.
6.  **Masking:** A binary mask is generated, showing only the pixels belonging to the selected cluster. If the correct cluster was chosen, the hidden number should appear in the mask.

## Usage

1.  **Open in Colab:** Click the "Open In Colab" badge above or upload the `ishihara_kmeans.ipynb` file to your Google Colab environment.
2.  **Upload Image:** Run the first code cell. Click the "Choose Files" button and upload your Ishihara test image. Wait for the upload to complete.
3.  **Run All Cells:** Select `Runtime` -> `Run all` from the Colab menu, or run the cells sequentially using `Shift+Enter` or the play button.
4.  **Choose `k`:** Examine the cell under "Step 4: Run K-Means Clustering". You can modify the `k_value` variable (e.g., `k_value = 5`). A value between 3 and 6 is often a good starting point for Ishihara plates. Re-run this cell if you change `k`.
5.  **Observe Quantized Image:** Look at the "Quantized Image" output. Note how the colors have been grouped. Also, examine the printed "Cluster Centroid Colors" and their corresponding indices (0, 1, 2, ...).
6.  **Identify Number Cluster:** Determine which cluster index seems to represent the color(s) of the hidden number in the quantized image.
7.  **Enter Index:** Run the final cell ("Step 5: Extract the Number"). When prompted, enter the cluster index you identified.
8.  **View Mask:** A third plot, "Potential Number Mask," will appear. If you chose the correct index and `k` was appropriate, the hidden number should be visible (usually in white against a black background). If not, you may need to try a different `k` value or select a different cluster index.

## Customization

*   **Number of Clusters (`k_value`):** This is the most critical parameter to adjust. Experiment with different values in the Step 4 cell.
*   **Cluster Index for Masking:** In Step 5, you must input the index corresponding to the number based on the Step 4 output.
*   **K-Means Parameters:** You can modify `max_iters` (maximum iterations) and `tol` (convergence tolerance) when creating the `KMeans` object in Step 4 if needed.

## Limitations

*   The number extraction method is purely heuristic and relies on visual inspection and user input. It's not an automated recognition system.
*   The success heavily depends on the quality of the Ishihara image and the choice of `k`. Some plates might be harder to segment than others.
*   K-Means results can vary slightly between runs due to the random initialization of centroids, although convergence often leads to similar results.
*   The handling of empty clusters during the algorithm is basic (re-initialization).
