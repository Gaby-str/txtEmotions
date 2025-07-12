
## Resultados CountVectorizer 

#### Del cross validate
f1 prom:  0.7281401033099608
Accuracy prom:  0.7502185212639733

#### Del modelo entrenado

                   precision    recall  f1-score   support

         sadness       0.77      0.91      0.84      1277
           anger       0.87      0.71      0.78       617
            love       0.78      0.36      0.50       318
        surprise       0.68      0.19      0.30       168
            fear       0.81      0.65      0.72       531
           happy       0.76      0.91      0.83      1381

        accuracy                           0.78      4292
       macro avg       0.78      0.62      0.66      4292
    weighted avg       0.78      0.78      0.76      4292



## Resultados TfidfVectorizer

#### Del cross validate
f1 prom:  0.5664388039206901
Accuracy prom:  0.6415799920855612

#### Del modelo entrenado

                   precision    recall  f1-score   support

         sadness       0.68      0.92      0.78      1277
           anger       0.96      0.29      0.45       617
            love       1.00      0.07      0.13       318
        surprise       1.00      0.01      0.01       168
            fear       0.90      0.24      0.38       531
           happy       0.61      0.97      0.75      1381

        accuracy                           0.66      4292
       macro avg       0.86      0.42      0.42      4292
    weighted avg       0.76      0.66      0.60      4292


## Resultados TfidfVectorizer + SMOTE sobremuestreo

#### Del cross validate
f1 prom:  0.902898308321791
Accuracy prom:  0.9039187913125591

#### Del modelo entrenado

                   precision    recall  f1-score   support

         sadness       0.88      0.87      0.87      1277
           anger       0.84      0.80      0.82       617
            love       0.59      0.78      0.67       318
        surprise       0.54      0.73      0.62       168
            fear       0.81      0.78      0.80       531
           happy       0.87      0.82      0.84      1381

        accuracy                           0.82      4292
       macro avg       0.76      0.80      0.77      4292
    weighted avg       0.83      0.82      0.82      4292