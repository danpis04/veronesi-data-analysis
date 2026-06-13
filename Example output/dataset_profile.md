# Heart Disease Dataset Profile

- Source directory: `C:\Users\danie\Downloads\heart+disease`
- Combined processed modeling table: 920 rows x 16 columns
- Processed source files: processed.cleveland.data, processed.hungarian.data, processed.switzerland.data, processed.va.data
- Target candidates: `num` and derived `disease_binary = num > 0`
- Full duplicate rows: 2; duplicate rows ignoring site: 2
- Total missing cells in modeling table: 1759

## Processed File Profiles

                                                              site rows columns                               target_counts_num  binary_target_counts missing_cells
processed.cleveland.data               Cleveland Clinic Foundation  303      17  {'0': 164, '1': 55, '2': 36, '3': 35, '4': 13}  {'0': 164, '1': 139}             6
processed.hungarian.data         Hungarian Institute of Cardiology  294      17                            {'0': 188, '1': 106}  {'0': 188, '1': 106}           782
processed.switzerland.data  University Hospital Zurich Switzerland  123      17     {'0': 8, '1': 48, '2': 32, '3': 30, '4': 5}    {'0': 8, '1': 115}           273
processed.va.data                   V.A. Medical Center Long Beach  200      17   {'0': 51, '1': 56, '2': 41, '3': 42, '4': 10}   {'0': 51, '1': 149}           698

## Preview

 age  sex  cp  trestbps  chol  fbs  restecg  thalach  exang  oldpeak  slope  ca  thal  num  disease_binary                 source_site
63.0  1.0 1.0     145.0 233.0  1.0      2.0    150.0    0.0      2.3    3.0 0.0   6.0    0               0 Cleveland Clinic Foundation
67.0  1.0 4.0     160.0 286.0  0.0      2.0    108.0    1.0      1.5    2.0 3.0   3.0    2               1 Cleveland Clinic Foundation
67.0  1.0 4.0     120.0 229.0  0.0      2.0    129.0    1.0      2.6    2.0 2.0   7.0    1               1 Cleveland Clinic Foundation
37.0  1.0 3.0     130.0 250.0  0.0      0.0    187.0    0.0      3.5    3.0 0.0   3.0    0               0 Cleveland Clinic Foundation
41.0  0.0 2.0     130.0 204.0  0.0      2.0    172.0    0.0      1.4    1.0 0.0   3.0    0               0 Cleveland Clinic Foundation
56.0  1.0 2.0     120.0 236.0  0.0      0.0    178.0    0.0      0.8    1.0 0.0   3.0    0               0 Cleveland Clinic Foundation
62.0  0.0 4.0     140.0 268.0  0.0      2.0    160.0    0.0      3.6    3.0 2.0   3.0    3               1 Cleveland Clinic Foundation
57.0  0.0 4.0     120.0 354.0  0.0      0.0    163.0    1.0      0.6    1.0 0.0   3.0    0               0 Cleveland Clinic Foundation
63.0  1.0 4.0     130.0 254.0  0.0      2.0    147.0    0.0      1.4    2.0 1.0   7.0    2               1 Cleveland Clinic Foundation
53.0  1.0 4.0     140.0 203.0  1.0      2.0    155.0    1.0      3.1    3.0 0.0   7.0    1               1 Cleveland Clinic Foundation
57.0  1.0 4.0     140.0 192.0  0.0      0.0    148.0    0.0      0.4    2.0 0.0   6.0    0               0 Cleveland Clinic Foundation
56.0  0.0 2.0     140.0 294.0  0.0      2.0    153.0    0.0      1.3    2.0 0.0   3.0    0               0 Cleveland Clinic Foundation

## Schema Summary

        column                           role   dtype  non_null  missing  missing_percent  unique_values                                                                                                                         example_values
           age              numeric_predictor float64       920        0             0.00             50                                                                                         63.0, 67.0, 37.0, 41.0, 56.0, 62.0, 57.0, 53.0
           sex   binary_categorical_predictor float64       920        0             0.00              2                                                                                                                               1.0, 0.0
            cp  ordinal_categorical_predictor float64       920        0             0.00              4                                                                                                                     1.0, 4.0, 3.0, 2.0
      trestbps              numeric_predictor float64       861       59             6.41             61                                                                                 145.0, 160.0, 120.0, 130.0, 140.0, 172.0, 150.0, 110.0
          chol              numeric_predictor float64       890       30             3.26            217                                                                                 233.0, 286.0, 229.0, 250.0, 204.0, 236.0, 268.0, 354.0
           fbs   binary_categorical_predictor float64       830       90             9.78              2                                                                                                                               1.0, 0.0
       restecg          categorical_predictor float64       918        2             0.22              3                                                                                                                          2.0, 0.0, 1.0
       thalach              numeric_predictor float64       865       55             5.98            119                                                                                 150.0, 108.0, 129.0, 187.0, 172.0, 178.0, 160.0, 163.0
         exang   binary_categorical_predictor float64       865       55             5.98              2                                                                                                                               0.0, 1.0
       oldpeak              numeric_predictor float64       858       62             6.74             53                                                                                                 2.3, 1.5, 2.6, 3.5, 1.4, 0.8, 3.6, 0.6
         slope  ordinal_categorical_predictor float64       611      309            33.59              3                                                                                                                          3.0, 2.0, 1.0
            ca  ordinal_categorical_predictor float64       309      611            66.41              4                                                                                                                     0.0, 3.0, 2.0, 1.0
          thal          categorical_predictor float64       434      486            52.83              3                                                                                                                          6.0, 3.0, 7.0
           num                 ordinal_target   int64       920        0             0.00              5                                                                                                                          0, 2, 1, 3, 4
disease_binary binary_target_derived_from_num   Int64       920        0             0.00              2                                                                                                                                   0, 1
   source_site              cohort_identifier     str       920        0             0.00              4 Cleveland Clinic Foundation, Hungarian Institute of Cardiology, University Hospital Zurich Switzerland, V.A. Medical Center Long Beach

## Target Counts

 num  count  percent
   0    411    44.67
   1    265    28.80
   2    109    11.85
   3    107    11.63
   4     28     3.04

## Binary Target Counts

 disease_binary  count  percent
              0    411    44.67
              1    509    55.33

## Site Composition

                           source_site  rows  disease_present  target_missing  disease_present_percent
           Cleveland Clinic Foundation   303              139               0                    45.87
     Hungarian Institute of Cardiology   294              106               0                    36.05
University Hospital Zurich Switzerland   123              115               0                     93.5
        V.A. Medical Center Long Beach   200              149               0                     74.5

## Missingness Summary

        column  missing_count  missing_percent
            ca            611            66.41
          thal            486            52.83
         slope            309            33.59
           fbs             90             9.78
       oldpeak             62             6.74
      trestbps             59             6.41
         exang             55             5.98
       thalach             55             5.98
          chol             30             3.26
       restecg              2             0.22
           age              0             0.00
            cp              0             0.00
disease_binary              0             0.00
           num              0             0.00
           sex              0             0.00
   source_site              0             0.00

## Numeric Summary

 feature  count       mean        std  min     1%    5%   25%   50%   75%   95%    99%   max
     age  920.0  53.510870   9.424685 28.0 32.000  37.0  47.0  54.0  60.0  68.0  74.00  77.0
trestbps  861.0 132.132404  19.066070  0.0 95.000 105.0 120.0 130.0 140.0 160.0 180.00 200.0
    chol  890.0 199.130337 110.780810  0.0  0.000   0.0 175.0 223.0 268.0 334.1 412.55 603.0
 thalach  865.0 137.545665  25.926276 60.0 75.560  95.0 120.0 140.0 157.0 178.0 186.36 202.0
 oldpeak  858.0   0.878788   1.091226 -2.6 -0.586   0.0   0.0   0.5   1.5   3.0   4.00   6.2

## Clinical Range Validation

 feature                                 rule  flagged_rows  flagged_percent                                                                 source_site_breakdown
     age             age outside 18-100 years             0             0.00                                                                                    {}
     sex                    sex outside {0,1}             0             0.00                                                                                    {}
      cp                 cp outside {1,2,3,4}             0             0.00                                                                                    {}
trestbps resting systolic BP <=0 or >300 mmHg             1             0.11                                                 {"V.A. Medical Center Long Beach": 1}
    chol  serum cholesterol <=0 or >800 mg/dl           172            18.70 {"University Hospital Zurich Switzerland": 123, "V.A. Medical Center Long Beach": 49}
     fbs                    fbs outside {0,1}             0             0.00                                                                                    {}
 restecg              restecg outside {0,1,2}             0             0.00                                                                                    {}
 thalach   maximum heart rate <=0 or >250 bpm             0             0.00                                                                                    {}
   exang                  exang outside {0,1}             0             0.00                                                                                    {}
 oldpeak       ST depression outside -5 to 10             0             0.00                                                                                    {}
   slope                slope outside {1,2,3}             0             0.00                                                                                    {}
      ca                 ca outside {0,1,2,3}             0             0.00                                                                                    {}
    thal                 thal outside {3,6,7}             0             0.00                                                                                    {}
     num       target num outside {0,1,2,3,4}             0             0.00                                                                                    {}

## PIPO

- **Population Patients**: Adult patients evaluated for heart disease at Cleveland, Hungarian, Swiss, and Long Beach VA clinical sites.
- **Inputs Predictors**: Demographics, chest pain class, resting blood pressure, cholesterol, fasting blood sugar, resting ECG, maximum heart rate, exercise angina, ST depression/slope, fluoroscopy vessels, thalassemia stress-test category.
- **Procedures Processes**: Clinical examination, laboratory cholesterol and fasting blood sugar, resting ECG, exercise testing, fluoroscopy/thalassemia-related assessment fields.
- **Outcomes Endpoints**: num, an angiographic heart disease status from 0 to 4; binary disease presence derived as num > 0.

## Runtime Package Versions

- numpy: 2.3.5
- pandas: 3.0.1
- matplotlib: 3.11.0
- sklearn: 1.9.0
- scipy: 1.17.1
- seaborn: 0.13.2