

# Player Classification using Image Processing Techniques

## Overview

This project aims to classify players in images using various image processing techniques and deep learning models. By detecting players and analyzing their features, we can group similar players based on visual characteristics. The project employs different methodologies, including traditional computer vision techniques and advanced deep learning approaches, to achieve robust classification results.

## Table of Contents


- [Methodology](#methodology)
  - [Player Detection](#player-detection)
  - [Feature Extraction](#feature-extraction)
  - [Classification Approaches](#classification-approaches)
    - [Approach 1: Cosine Similarity with Feature Vectors](#approach-1-cosine-similarity-with-feature-vectors)
    - [Approach 2: CLIP (Vision Transformers)](#approach-2-clip-vision-transformers)
    - [Approach 3: Colour Layout Descriptor](#approach-3-colour-layout-descriptor)
    - [Approach 4: Weighted Combination of CLIP and Colour Layout Descriptor](#approach-4-weighted-combination-of-clip-and-colour-layout-descriptor)
- [Results](#results)
- [Usage](#usage)




## Methodology

### Player Detection

1. **YOLOv3 Model**: The project begins by loading the YOLOv3 model, which is a powerful object detection algorithm. This model is used to detect players within the input images by drawing bounding boxes around individuals identified as "persons".
   
2. **Image Cropping**: Once players are detected, their corresponding regions are cropped from the original images, resulting in individual images for each player. This enables focused analysis on each player without interference from the background.

### Feature Extraction

Feature extraction is performed using two different methods to capture the visual characteristics of the player images:

1. **Inception Model**: 
   - The Inception V3 model is utilized for extracting feature vectors from cropped player images. This model, pre-trained on a large dataset, effectively captures high-level features.
   - The feature vectors are generated by processing each player image through the model, which outputs a representation of the image in a lower-dimensional space.
   - These feature vectors are then used for similarity comparison using cosine similarity metrics.

2. **CLIP (Vision Transformers)**: 
   - CLIP is used to compute textual embeddings of the player images. The model integrates vision and language, allowing it to encode images into feature vectors that capture their semantic meaning.
   - For each player image, a corresponding embedding is generated, enabling comparisons to classify players based on visual similarities.

### Classification Approaches

#### Approach 1: Cosine Similarity with Feature Vectors

- **Feature Vector Generation**: Using the Inception model, feature vectors for all player images are generated. 
- **Comparison with Reference Image**: A reference image's feature vector (e.g., the average of a selected group) is calculated, and cosine similarity is computed with each player’s feature vector.
- **Classification**: The player image with the highest similarity score is identified as the most similar to the reference image. This approach allows for straightforward player classification based on feature similarity.

#### Approach 2: CLIP (Vision Transformers)

- **Image Encoding**: The player images are processed through the CLIP model to generate embeddings that capture the visual features of each player.
- **Similarity Calculation**: Similarity scores are computed between the embeddings of each player and those of a reference player. The comparison allows us to classify images based on their closeness to the reference embeddings.
- **Output**: Each image is classified as either corresponding to player 1 or player 2, depending on which reference image it is most similar to.

#### Approach 3: Colour Layout Descriptor

- **Custom Weighting**: To enhance the significance of color information, a custom weight matrix is created, emphasizing the center of the image. To further refine the color layout descriptors, the weights of the grid boxes in the center have been increased. Due to this more attention is achived in the center thus enhancing the color layout descriptor for Tshirt colour detection.
- **Color Layout Descriptor Generation**: The images are divided into grids, and color descriptors are generated for each grid cell. The mean color of each cell is computed, and weights are applied to the descriptors.
- **Comparison**: Similarity between player color descriptors and reference descriptors is assessed using Euclidean distances.
- **Classification**: Players are classified based on which reference image they are more similar to, considering the color layout.

#### Approach 4: Weighted Combination of CLIP and Colour Layout Descriptor

- **Combination of Methods**: This approach integrates results from both CLIP and color layout descriptor methods. It allows for a more comprehensive classification by leveraging the strengths of each method.
- **Weighted Scoring**: Similarity scores from both approaches are computed, and a weighted score is calculated for each player image. The weights can be adjusted to reflect the relative importance of visual features versus color characteristics.
- **Final Classification**: Based on the weighted scores, images are classified into their respective player groups, ensuring a robust classification process.

## Results

The results of the classification are stored in separate output directory.Based on the classification approaches used player_1 and player_2 have 4 diffrent type of folders for the 4 differnt approaches. Each classified image is accompanied by similarity scores indicating how closely it matches the reference player images.

## Analysis

The Approach 4 of weighted combination of CLIP and Colour Layout Descriptor has shown the best results in terms of classification accuracy. By combining the strengths of both methods, the classification process becomes more robust and accurate. The weighted scoring mechanism allows for fine-tuning the classification based on the relative importance of visual features and color characteristics. This approach can be further optimized by adjusting the weights and exploring additional feature extraction techniques to enhance the classification performance. We can achieve about 80% accuracy in the classification of players using this approach. 

### Best accuracy achieved is about 80%.

## Usage

To run the project:

1. Ensure you have the necessary libraries installed.
2. Prepare your images and place them in the appropriate directories.
3. Run the script to execute the detection, feature extraction, and classification processes.
4. Check the output directories for the classified images.

## Extra
Also performed segmentation and another background extraction using mask to remove the background and focus on the player.


