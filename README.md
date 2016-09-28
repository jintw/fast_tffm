# Tensorflow-based Distributed Factorization Machine
An efficient distributation factoriazation machine implementation based on tensorflow (cpu only).

1. Support both multi-thread local machine training and distributed training.
2. Can easily benefit from numerous implementations of operators in tensorflow, e.g., different optimizors, loss functions.
3. Customized c++ operators, significantly faster than pure python implementations. Comparable performance (actually faster according to my benchmark) with pure c++ implementation.

## Quick Start
### Compile
```
mkdir build
cd build
cmake ../
make
make test
cd ..
```
### Local Training
```
python fast_tffm.py train sample.cfg
```
### Distributed Training
Open 4 command line windows. Run the following commands on each window to start 2 parameter servers and 2 workers.
```
python fast_tffm.py dist_train sample.cfg ps 0
python fast_tffm.py dist_train sample.cfg ps 1
python fast_tffm.py dist_train sample.cfg worker 0
python fast_tffm.py dist_train sample.cfg worker 1
```
### Local Prediction
```
python fast_tffm.py predict sample.cfg
```
### Distributed Prediction
Open 4 command line windows. Run the following commands on each window to start 2 parameter servers and 2 workers.
```
python fast_tffm.py dist_predict sample.cfg ps 0
python fast_tffm.py dist_predict sample.cfg ps 1
python fast_tffm.py dist_predict sample.cfg worker 0
python fast_tffm.py dist_predict sample.cfg worker 1
```
## Benchmark

1. Local Mode. Training Efficiency compared with difacto using the same configuration

  + *Configuration*: 36672494 training examples, 10 threads, factor_num = 8, batch_size = 10000, epoch_num = 1, vocabulary_size = 40000000
  + **Difacto**: 337 seconds. 108820 examples / second.
  + **FastTffm**: 157 seconds. 233582 examples / second.
  
2. Distriubuted Mode.
  + Coming soon...
  
## Input Data Format

[label] [fid]:[fval]

label: currently only support binary. 0 or 1

fid: feature id. Starting from 0.
