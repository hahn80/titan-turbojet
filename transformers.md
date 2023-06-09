# How to call functions with transformers service?

Transformers will contain serveral algorithms to run ML tasks.

## Clustering

Here is the sample of json file to run the service:
```json
{
    "input": "iris.arrow",
    "output": "output.arrow",
    "operations": [
        {
            "operator": "select",
            "options": {"columns": ["x1", "x2", "x4"]}
        },
        {
            "operator": "clustering",
            "options": {"cluster_name": "hac", "columns": ["x1", "x2"], "n_clusters": 3}
        }
    ]
}
```
We can create the json object in Java, convert it to HashMap and pass it directly to Python using Py4J.
Let me explain the information in the above json params.
`"input": "iris.arrow"` is the input of arrow format. We also work with arrow!
`"output": "output.arrow"` is the output file of the result. Note that the transformers always gives the output in the arrow format, so the output file should be in the arrow format.

`"operations": []` will contain a list of operations. We can perform multiple operations as you want!
Each entry of operations is a dictionary, for example
```json
{
            "operator": "clustering",
            "options": {"cluster_name": "hac", "columns": ["x1", "x2"], "n_clusters": 3}
        }
```
It tells us that we call function `clustering` passing params `"options": {"cluster_name": "hac", "columns": ["x1", "x2"], "n_clusters": 3}` to this function.

The only thing we need to change is the `"cluster_name"`. There are the following clustering names you can call:

- hac: Hierarchical Agglomerate Clustering. For example `"cluster_name": "hac"`.
- kmean: K-means Clustering. For example `"cluster_name": "kmean"`.
- spectral: Spectral Clustering
- gmm: Gaussian Mixture Clustering
- bgm: Bayesian Mixture Clustering
- meanshift: MeanShift Clustering
- affinity: Affinity Propagation Clustering
- bdscan: DBSCAN Clustering
- optics: Optics Clustering

## Imputer
This function will fill the missing values for data preprocessing.
Here is the sample of json file to run the service:
```json
{
    "input": "outlier.arrow",
    "output": "output.arrow",
    "operations": [
        {
            "operator": "select",
            "options": {"columns": ["x1", "x2", "x3"]}
        }
        {
            "operator": "imputer",
            "options": {"columns": ["x3"], "method": "simple", "strategy": "mean"}
        },
        {
            "operator": "imputer",
            "options": {"columns": ["x2"], "method": "interpolate"}
        },
        {
            "operator": "imputer",
            "options": {"columns": ["x1"], "method": "knn", "n_neighbors": 5}
        },
        {
            "operator": "imputer",
            "options": {"columns": ["x2"], "method": "bayesian", "max_iter": 10}
        }
    ]
}

```
The only thing we want to change is the `"method"`. There are the following methods
- simple: A simpple imputation with different strategies: ‘forward’, ‘backward’, ‘min’, ‘max’, ‘mean’, ‘zero’, ‘one
- interpolate: Fill nulls with linear interpolation over missing values.
- knn: Impute the missing values using k-Nearest Neighbors
- bayesian: Multivariate imputer using BayesianRidge estimator.

## Outlier
Detect the outliers from a given Polars dataframe.
Here is a sample json params:
```json
{
    "input": "outlier.arrow",
    "output": "output.arrow",
    "operations": [
        {
            "operator": "select",
            "options": {"columns": ["x1", "x2", "x3"]}
        },
        {
            "operator": "outlier",
            "options": {"outlier_name": "iqr", "columns": ["x1", "x2"]}
        }
    ]
}
```
There are many ways to use outlier. We only need to change the `"outlier_name"`. Here is the list of options
- iso_forest: Isolation Forest Algorithm
- local_factor: Unsupervised Outlier Detection using the Local Outlier Factor
- one_svm: Unsupervised Outlier Detection using SVM
- ledoit_wolf: Oulier using LedoitWolf estimator
- kernel_density: Outlier using Kernel Density Estimation
- iqr: Outlier using IQR
- z_scores: Outlier using Z-Scores.

**Ghi chú:**
- Biến columns có thể 1 đến nhiều phần tử.
- Ví dụ, select ["keys", "x1"] rồi thực hiện outlier với biến "x1". Kết quả trả về sẽ bao gồm cả dữ liệu ngoại biên của "x1" và các keys tương ứng.
- Kiểu dữ liệu cho columns là numerical (int, float).


## Feature Selections

The function `kfeatures` will take input Polars dataframe and give output as a copy of the dataframe with importance features.
Here is the sample of json file to run the service:
```json
{
    "input": "domin.arrow",
    "output": "output.arrow",
    "operations": [
    {
        "operator": "kfeatures",
        "options":
        {
            "columns": [
                "CRIM", "ZN", "INDUS", "CHAS", "NOX", "RM", "AGE", "DIS", "RAD", "TAX", "PTRATIO", "B", "LSTAT"
            ],
            "target": "PRICE",
            "method": "sequence"
        }
    }]
}
```
There are serveral methods to call for this functions:
- percentile: Select features according to a percentile of the highest scores
- random_forest: Select features using random forest regressor.
- svm: Select features using support vector machines.
- rfe: Select feature using recursive feature elimination.
- sequence: Sequential Feature Selection
- best: This is the default method using SelectKBest with f_regression

Notics: After running kfeature, we can perform diminance analysis.
