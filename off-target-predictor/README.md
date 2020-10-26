### General Idea

Our prediction model aims to scan the potential off-target sites on the genome and identify off-target sites with high confidence in experiments.

![](https://2020.igem.org/wiki/images/5/5e/T--SJTU-BioX-Shanghai--scan_genome.png)

In our model pipeline, we first construct our training set from the result of high-throughput sequencing and bioinformatics tools. Next, we use a machine learning model to carry out the classification task after extracting the features according to the sequence information.

![](https://2020.igem.org/wiki/images/3/33/T--SJTU-BioX-Shanghai--prediction_pipeline.png)

### Training Result

We consider the mismatch condition at each position for the sequence pair contains <Match,Transition,Transversion>, and the frequencies of them existing in the positive dataset are different.  We utilize 5-fold training to evaluate our model's robustness after feature extraction. Here are the common metrics to assess the performance of our machine learning model and the receiver operating characteristic (ROC) curve.

|  Fold  | Accuracy | Sensitivity | Specificity | Precision | F-measure |  MCC  |
| :----: | :------: | :---------: | :---------: | :-------: | :-------: | :---: |
| Fold 1 |  0.983   |    0.664    |    0.995    |   0.832   |   0.739   | 0.735 |
| Fold 2 |  0.982   |    0.651    |    0.995    |   0.817   |   0.725   | 0.720 |
| Fold 3 |  0.982   |    0.663    |    0.994    |   0.814   |   0.731   | 0.726 |
| Fold 4 |  0.982   |    0.654    |    0.994    |   0.800   |   0.720   | 0.714 |
| Fold 5 |  0.982   |    0.644    |    0.996    |   0.803   |   0.715   | 0.710 |

![](https://2020.igem.org/wiki/images/2/2c/T--SJTU-BioX-Shanghai--roc_curve.png)

### Predictor Software

+ Mode 1 (start from searching off-target candidates)

  Required to download [cas-OFFinder](https://sourceforge.net/projects/cas-offinder/files/Binaries/2.4/) and reference genome

  Sample Input

  ```shell
  python predict_mode_1.py -h
  usage: predict_mode_1.py [-h] -g GENOME_PATH -t TARGET_SEQ [-n {3,4,5,6}]
                           [-f FEATURE_FILE] [-m MODEL_FILE] [-o OUTPUT_FILE]
  
  Find off-target sequences for target with NGG PAM
  
  optional arguments:
    -h, --help            show this help message and exit
    -g GENOME_PATH, --genome_path GENOME_PATH
                          Input the abosulte path for the genome
    -t TARGET_SEQ, --target_seq TARGET_SEQ
                          Input the target sequence
    -n {3,4,5,6}, --max_mismatch_num {3,4,5,6}
                          Input the maximum number of mismatch
    -f FEATURE_FILE, --feature_file FEATURE_FILE
                          Input the feature file
    -m MODEL_FILE, --model_file MODEL_FILE
                          Input the model file
    -o OUTPUT_FILE, --output_file OUTPUT_FILE
                          Output csv file name
  ```

+ Mode 2 (directly input the sequence pairs)

  Required to prepare a csv file consist of <target,off-target seq> pairs

  ```shell
  usage: predict_mode_2.py [-h] -c CSV_FILE [-f FEATURE_FILE] [-m MODEL_FILE]
                           [-o OUTPUT_FILE]
  
  Find off-target sequences for target with NGG PAM
  
  optional arguments:
    -h, --help            show this help message and exit
    -c CSV_FILE, --csv_file CSV_FILE
                          Input target and potential off-target sequence pairs
                          in a .csv file
    -f FEATURE_FILE, --feature_file FEATURE_FILE
                          Input the feature file
    -m MODEL_FILE, --model_file MODEL_FILE
                          Input the model file
    -o OUTPUT_FILE, --output_file OUTPUT_FILE
                          Output csv file name
  ```

  
