# DVC_Tutorial2

## Code
The sample code are provided from DVC:
https://dvc.org/doc/start/data-pipelines/data-pipelines

## DVC Pipline
This create a file "dvc.yaml" represent the pipline.
```
dvc init
dvc stage add -n featurize \
              -p featurize.max_features,featurize.ngrams \
              -d src/featurization.py -d data/prepared \
              -o data/features \
              python src/featurization.py data/prepared data/features
```
-n: name
-d: dependency
-p: parameter
-o: output

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