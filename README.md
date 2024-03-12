# DVC_Tutorial2

## Code
The sample code and data are provided from DVC:
https://dvc.org/doc/start/data-pipelines/data-pipelines

## DVC Pipline
This create a file "dvc.yaml" represent the pipline.
```
dvc init

dvc stage add -n prepare \
              -p prepare.seed,prepare.split \
              -d src/prepare.py -d data/data.xml \
              -o data/prepared \
              python src/prepare.py data/data.xml

dvc stage add -n featurize \
              -p featurize.max_features,featurize.ngrams \
              -d src/featurization.py -d data/prepared \
              -o data/features \
              python src/featurization.py data/prepared data/features

dvc stage add -n train \
              -p train.seed,train.n_est,train.min_split \
              -d src/train.py -d data/features \
              -o model.pkl \
              python src/train.py data/features model.pkl
```
-n: name
-d: dependency
-p: parameter
-o: output
The last line is the comment to run.

## Reproducing
```
dvc repro
```

## Visualizing Stages
```
dvc dag
```
```
+-----------+  
| featurize |  
+-----------+  
      *        
      *        
      *        
  +-------+    
  | train |    
  +-------+  
```