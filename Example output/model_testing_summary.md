# Model Testing Summary

```text
                          model  accuracy  precision  roc_auc  average_precision  cv_wall_seconds  inference_ms_per_200_rows
regularized_logistic_regression  0.805435   0.830000 0.883317           0.889479         0.158624                     5.7164
                  random_forest  0.808696   0.818356 0.882958           0.880139         5.543485                    44.0594
```

All models excluded `num` and direct `source_site`; preprocessing was fit inside 5-fold stratified cross-validation.
