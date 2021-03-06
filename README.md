# Recommender

This project is my first attempt to create a recommendation system using tensorflow. My first idea was to contribute to [TF-recomm](https://github.com/songgc/TF-recomm). But since my code took its own direction I decided to create this repository instead. Like that repository I am trying to implement the models presented in [Factorization Meets the Neighborhood](http://www.cs.rochester.edu/twiki/pub/Main/HarpSeminar/Factorization_Meets_the_Neighborhood-_a_Multifaceted_Collaborative_Filtering_Model.pdf) using the dataset [Movielens](http://grouplens.org/datasets/movielens/). The only models implemented so far are the SVD model and the NSVD model, both mentioned in section 2.3. I wrote a blog post on [medium](https://medium.com/@felsal/implementing-a-recommendation-system-on-tensorflow-e41b80793165) about implementing these two models.

### Requirements
* Tensorflow 
* Numpy
* Pandas 

## Usage

```
$ python3 svd.py --help
usage: svd.py [-h] [-p PATH] [-e EXAMPLE] [-b BATCH] [-s STEPS] [-d DIMENSION]
              [-r REG] [-l LEARNING] [-m MOMENTUM] [-i INFO] [-M MODEL]
              [-S NSVD_SIZE]

optional arguments:
  -h, --help            show this help message and exit
  -p PATH, --path PATH  ratings path (default=pwd/movielens/ml-1m/ratings.dat)
  -e EXAMPLE, --example EXAMPLE
                        movielens dataset examples (only 1, 10 or 20)
                        (default=1)
  -b BATCH, --batch BATCH
                        batch size (default=700)
  -s STEPS, --steps STEPS
                        number of training steps (default=7000)
  -d DIMENSION, --dimension DIMENSION
                        embedding vector size (default=12)
  -r REG, --reg REG     regularizer constant for the loss function
                        (default=0.0003)
  -l LEARNING, --learning LEARNING
                        learning rate (default=0.001)
  -m MOMENTUM, --momentum MOMENTUM
                        momentum factor (default=0.926)
  -i INFO, --info INFO  Training information. Only True or False
                        (default=True)
  -M MODEL, --model MODEL
                        models: either svd or nsvd (default=svd)
  -S NSVD_SIZE, --nsvd_size NSVD_SIZE
                        size of the vectors of the nsvd model: either max,
                        mean or min (default=mean)



```


## Example

```
$ bash download_data.sh
$ cd examples/
$ python3 svd.py -s 20000

>> step batch_error test_error elapsed_time
  0 3.930429 3.988358* 0.243376(s)
1000 0.943535 0.934758* 1.532505(s)
2000 0.921224 0.933712* 1.571072(s)
3000 0.943956 0.927437* 1.534095(s)
4000 0.913235 0.840039* 1.525031(s)
5000 0.897798 0.901872 1.281967(s)
6000 0.978220 0.896336 1.277157(s)
7000 0.899796 0.903618 1.292524(s)
8000 0.925525 0.944306 1.279324(s)
9000 0.894377 0.883023 1.285019(s)
10000 0.924365 0.941058 1.279905(s)
11000 0.921969 0.897630 1.267302(s)
12000 0.917880 0.899381 1.274572(s)
13000 0.922738 0.933798 1.285953(s)
14000 0.876588 0.946282 1.285653(s)
15000 0.904958 0.891187 1.278772(s)
16000 0.954195 0.907019 1.293461(s)
17000 0.900970 0.903008 1.294990(s)
18000 0.902404 0.879164 1.277366(s)
19000 0.875246 0.957183 1.292368(s)
 
>> The duration of the whole training with 20000 steps is 26.93 seconds,
which is equal to:  0:0:0:26 (DAYS:HOURS:MIN:SEC)

>> The mean square error of the whole valid dataset is  0.915779

>> Using our model for 10 specific users and 10 movies we predicted the following score:
[ 4.11244917  4.38496399  3.26372051  3.59210873  1.446275    3.33612514
  3.27328825  4.65662336  2.41137171  3.19429493]

>> And in reality the scores are:
[ 5.  5.  1.  1.  1.  5.  5.  5.  1.  2.]

```
