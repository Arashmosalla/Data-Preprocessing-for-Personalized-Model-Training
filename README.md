# Data Preprocessing for Personalized Model Training

## Overview
This project focuses on splitting the dataset into training, development (dev), and test subsets to facilitate personalized model training, fine-tuning, and evaluation for individual unique identifiers (`Plate_NUM`). A three-set data split strategy is used to ensure a robust and unbiased evaluation while maintaining sufficient training data for generalization and individual-specific adaptations.

## 1. Motivation for a Three-Set Split
A conventional train-test split for each `Plate_NUM` can introduce potential issues:
- **Lack of fine-tuning**: Without a development set, the model cannot adapt global patterns to the unique characteristics of each `Plate_NUM`.
- **Hyperparameter selection bias**: Without a separate dev set, hyperparameters are often tuned on the test set, inflating performance metrics.
- **Overfitting risk**: A large training set without an intermediate dev set increases the likelihood of overfitting.
- **Biased evaluation**: Evaluating directly on the test set without prior fine-tuning limits model reliability.

To address these concerns, the dataset is split into three parts:
- **Training Set**: Used to train the global model with data from all `Plate_NUMs`.
- **Development Set (Dev Set)**: Used to fine-tune the model for specific `Plate_NUMs`.
- **Test Set**: Used to evaluate model performance on previously unseen records.

## 2. Challenges in Data Splitting
The primary challenges in defining an effective data split strategy include:
1. **Defining optimal split times** to balance training and evaluation data while ensuring adequate representation for each `Plate_NUM`.
2. **Ensuring all `Plate_NUMs` are included across subsets**, so that each `Plate_NUM` appears in training, dev, and test sets.
3. **Avoiding scenarios where a `Plate_NUM` appears only in dev or test sets** without any representation in training, which would make learning impossible.

## 3. Methodology
To create a robust data split, the following steps were followed:

### Step 1: Iterative Split Optimization
Various configurations of `train_end`, `dev_duration`, and `test_duration` were systematically tested to find an optimal split strategy. For each configuration, the following metrics were computed:
- The number of records for each `Plate_NUM` in training, dev, and test subsets to ensure adequate representation.
- The total number of unique `Plate_NUMs` distributed across all subsets.
- The overlap of `Plate_NUMs` between subsets to ensure that every `Plate_NUM` has at least one record in each subset.

### Step 2: Ranking Configurations
Configurations were ranked based on:
- **Maximizing `Plate_NUM` coverage** in dev and test sets.
- **Maintaining sufficient overlap with training data** to enable meaningful fine-tuning and evaluation.

The best configurations were those that:
- Provided enough training data for learning global patterns.
- Allowed fine-tuning using the dev set.
- Ensured that each `Plate_NUM` appeared in all subsets for consistent evaluation.


## 4. Validation of the Split Strategy
The selected data split ensures that:
- The training set captures general trends for all `Plate_NUMs`.
- The dev set allows for fine-tuning personalized adjustments.
- The test set evaluates the model’s ability to predict on new records.

## 5. Conclusion
By adopting a three-set split strategy, this methodology ensures fair and effective model training, fine-tuning, and evaluation. The inclusion of a dev set allows adaptation to `Plate_NUM`-specific behaviors while retaining generalizable patterns learned from the global dataset. The test set remains unbiased, providing a reliable assessment of model performance on unseen records.

