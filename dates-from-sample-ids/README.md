# Imputing sampling dates from sample IDs

The file [`samples.tsv`](samples.tsv) lists sample IDs and sampling dates if known. The notebook [`dates-from-sample-ids.nb`](dates-from-sample-ids.nb) reads this file and regresses sample ID against known date of sampling.

ordering of samples, i.e. G3757-5 is 1, G3769-5 is 2, etc... against known dates of sampling.

## Samples ordered by G-index

In this case, the predictor is the order of samples when sorted by their G-index, so for example, G3757-5 is 1, G3769-5 is 2, G3789-3 is 3, etc...

### Linear model

Assuming a linear relationship between G-index and date of sampling yields:

![](ordered-linear-regression.png)

The lighter band shows the 95% prediction interval and the darker band showing the 50% prediction interval. Adjusted *R*<sup>2</sup> for this relationship is 0.830. 

This relationship is used to impute sample dates:

![](ordered-linear-prediction.png)

These predictions are output to the file [`ordered-linear-imputation.tsv`](ordered-linear-imputation.tsv), which includes 50% and 95% prediction intervals for each sample with unknown date.

### Exponential model

Assuming a exponential relationship between G-index and date of sampling yields:

![](ordered-exponential-regression.png)

The lighter band shows the 95% prediction interval and the darker band showing the 50% prediction interval. Adjusted *R*<sup>2</sup> for this relationship is 0.827. 

This relationship is used to impute sample dates:

![](ordered-exponential-prediction.png)

These predictions are output to the file [`ordered-exponential-imputation.tsv`](ordered-exponential-imputation.tsv), which includes 50% and 95% prediction intervals for each sample with unknown date.

## Samples directly encoded by G-index

In this case, the predictor is taken directly from the G-index, so for example, G3757-5 is 3757, G3769-5 is 3769, G3789-3 is 3789, etc...

### Linear model

Assuming a linear relationship between G-index and date of sampling yields:

![](direct-linear-regression.png)

The lighter band shows the 95% prediction interval and the darker band showing the 50% prediction interval. Adjusted *R*<sup>2</sup> for this relationship is 0.879. 

This relationship is used to impute sample dates:

![](direct-linear-prediction.png)

These predictions are output to the file [`direct-linear-imputation.tsv`](direct-linear-imputation.tsv), which includes 50% and 95% prediction intervals for each sample with unknown date.

### Exponential model

Assuming a exponential relationship between G-index and date of sampling yields:

![](direct-exponential-regression.png)

The lighter band shows the 95% prediction interval and the darker band showing the 50% prediction interval. Adjusted *R*<sup>2</sup> for this relationship is 0.777. 

This relationship is used to impute sample dates:

![](direct-exponential-prediction.png)

These predictions are output to the file [`direct-exponential-imputation.tsv`](direct-exponential-imputation.tsv), which includes 50% and 95% prediction intervals for each sample with unknown date.

## Discussion

The direct / linear model gives the best adjusted *R*<sup>2</sup> to the training data at 0.879. However, this model appears to under-estimate the most samples (placing them in Sep rather than Nov).
