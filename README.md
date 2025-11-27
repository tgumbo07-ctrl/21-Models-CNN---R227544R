# 21-Models-CNN---R227544R
HDSC

Multimodal Property Price Prediction Project Summary

This project developed and benchmarked a Late Fusion Multimodal Architecture to predict property prices, utilizing both tabular features (e.g., bedrooms, location) and visual data (property images). The primary goal was to find the optimal Convolutional Neural Network (CNN) backbone for the image component that, when combined with a Multi-Layer Perceptron (MLP) for tabular data, minimizes prediction error.

Core Methodology 
Architecture:We employed a Late Fusion strategy. The tabular features and image features were processed by separate networks, each leading to its own prediction head. The final price prediction was the average of the two individual predictions.
Missing Data: A unique masking mechanism was implemented. If a property image was missing, a binary mask of '0' was used to zero out the image features, effectively disabling the visual pathway for that sample and allowing the model to rely solely on the tabular data.
Data Preprocessing: The target price variable was stabilized using a Log-Transform and Standard Scaling. The models were trained using the Huber Loss function, chosen for its robustness against significant price outliers.
Benchmarking: Twenty different CNN backbones (including popular models like ResNet, VGG, and custom stubs) were tested sequentially to compare performance.

Key Results

The model performance was evaluated using the Root Mean Squared Error (RMSE) and Mean Absolute Error (MAE), calculated on the prices in their original currency.
Best Model: The WideResNet backbone achieved the lowest prediction error.
Best RMSE: $4,429,167Best 
MAE: $650,033

Interpretation

All models yielded an R-squared ($R^2$) value close to or below zero. This indicates that while the models did learn, their predictive accuracy was not substantially better than simply guessing the average price. The consistently high magnitude of the RMSE and MAE, even with log-scaling and Huber Loss, confirms the extreme high variance and the presence of significant outliers within the raw property price data, making accurate absolute prediction a major challenge for this specific dataset.

Future Direction

Future work should focus on Fine-Tuning the top-performing backbones (unfreezing pre-trained weights) and exploring Early or Mid Fusion architectures to encourage deeper interaction between the image and tabular features.
