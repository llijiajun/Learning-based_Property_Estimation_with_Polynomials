# Redirect

[Click here to go to the learned_ndv_estimator](https://github.com/wurenzhi/learned_ndv_estimator)

Your should install and compile learned_ndv_estimator first.

### Learned NDV estimator
Learned model to estimate number of distinct values (NDV) of a population using a small sample. The model approximates the maximum likelihood estimation of NDV, which is difficult to obtain analytically.
See our VLDB 2022 paper [Learning to be a Statistician: Learned Estimator for Number of Distinct Values](https://vldb.org/pvldb/vol15/p272-wu.pdf) for more details.

### How to use
1. Install the package
   
    `pip install estndv`

2. Import and create an instance

```python
   from estndv import ndvEstimator
   estimator = ndvEstimator()
```

4. Assume your sample is S=[1,1,1,3,5,5,12] and the population size is N=100000. You can estimate population ndv by:

    `ndv = estimator.sample_predict(S=[1,1,1,3,5,5,12], N=100000)`
   
5. If you have the sample profile e.g. f=[2,1,1], you can estimate population NDV by:
   
    `ndv = estimator.profile_predict(f=[2,1,1], N=100000)`

6. If you have multiple samples/profiles from multiple populations, you can estimate population NDV for all of them in a batch by method `estimator.sample_predict_batch()` or `estimator.profile_predict_batch()`.



### How to train the ndv estimator
You can directly use our package on PyPI for your datasets, as the pre-trained model is agnostic to any workloads. However, if you want to train the model from scratch anyway, do the following:
1. Go to the model_training folder
    `cd model_training`

2. Install requirements
   
    `pip install requirements.txt`
   
3. Generate training data. (This uses a lot of memory.)
   
    `python training_data_generation.py`
   
4. Train model
   
    `python model_training.py`
5. Save trained pytorch model parameters to numpy, this generates a file model_paras.npy

    `python torch2npy.py`

6. Test with your model parameters by specifying a path to your model_paras.npy

   `estimator = ndvEstimator(para_path=your path to model_paras.npy)`

### Citation
If you use our work or found it useful, please cite our paper:
```
@article{wu2022learning,
   author = {Wu, Renzhi and Ding, Bolin and Chu, Xu and Wei, Zhewei and Dai, Xiening and Guan, Tao and Zhou, Jingren},
   title = {Learning to Be a Statistician: Learned Estimator for Number of Distinct Values},
   year = {2021},
   issue_date = {October 2021},
   publisher = {VLDB Endowment},
   volume = {15},
   number = {2},
   issn = {2150-8097},
   url = {https://doi.org/10.14778/3489496.3489508},
   doi = {10.14778/3489496.3489508},
   journal = {Proc. VLDB Endow.},
   month = {oct},
   pages = {272–284},
   numpages = {13}
}
```