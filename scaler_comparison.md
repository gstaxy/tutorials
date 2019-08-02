Inspired by: Jeff Hale							
See this Medium article for discussion:	https://towardsdatascience.com/scale-standardize-or-normalize-with-scikit-learn-6ccc7d176a02
See this Kaggle kernel for the code: https://www.kaggle.com/discdiver/scale-standardize-or-normalize-with-sklearn						


| Preprocessing Type | Scikit-learn Function | Range                        | Mean   | Distribution Characteristics |
| ------------------ | --------------------- | ---------------------------- | ------ | ---------------------------- |
| Scale              | MinMaxScaler          | 0 to 1 default, can override | varies | Bounded                      |
| Standardize        | RobustScaler          | varies                       | varies | Unbounded                    |
| Standardize        | StandardScaler        | varies                       | 0      | Unbounded                    |
| Normalize          | Normalizer            | varies                       | 0      | Unit norm, Unit variance     |
| ?                  | MaxAbsScaler          | ?                            | ?      | ?                            |

### MinMaxScaler
#### When to use
Use first unless have theoretical reason to need stronger medicine.
#### Definition
Add or substract a constant. Then multiply or divide by another constant. MinMaxScaler subtracts the mimimum value in the column and then divides by the difference between the original maximum and original minimum.
#### Notes
Preserves the shape of the original distribution. Doesn't reduce the importance of outliers. Least disruptive to the information in the original data. Default range for MinMaxScaler is 0 to 1.

### RobustScaler
#### When to use
Use if have outliers and don't want them to have much influence.
#### Definition
RobustScaler standardizes a feature by removing the median and dividing each feature by the interquartile range.
#### Notes
Outliers have less influence than with MinMaxScaler. Range is larger than MinMaxScaler or StandardScaler.

### StandardScaler
#### When to use
When need to transform a feature so it is close to normally distributed.
#### Definition
StandardScaler standardizes a feature by removing the mean and dividing each value by the standard deviation.
#### Notes
Results in a distribution with a standard deviation equal to 1 (and variance equal to 1). If you have outliers in your feature (column), normalizing your data will scale most of the data to a small interval.

### Normalizer
#### When to use
Rarely.
#### Definition
An observation (row) is normalized by applying l2 (Euclidian) normalization. If each element were squared and summed, the total would equal 1. Could also specify l1 (Manhatten) normalization.
#### Notes
Normalizes each sample observation (row), not the feature (column)!
