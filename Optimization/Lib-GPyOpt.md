# GPyOpt

> [홈페이지](https://sheffieldml.github.io/GPyOpt/), [깃허브](https://github.com/SheffieldML/GPyOpt), [매뉴얼(Jupyter)](https://nbviewer.jupyter.org/github/SheffieldML/GPyOpt/blob/devel/manual/index.ipynb), [ReadTheDocs](https://gpyopt.readthedocs.io/en/latest/)

```python 
# 패키지 설치 
sudo apt-get install python-pip
pip install gpyopt --user

# 소스 설치 
  git clone https://github.com/SheffieldML/GPyOpt.git
  cd GPyOpt
  python setup.py develop
```

>  GPy only supports python 2.7 and not python 3

## [실행 방법 ](https://sheffieldml.github.io/GPyOpt/firstexamples/index.html)

####  python 콘솔 
```python 
# --- Load GPyOpt
from GPyOpt.methods import BayesianOptimization
import numpy as np

# --- Define your problem
def f(x): return (6*x-2)**2*np.sin(12*x-4)
domain = [{'name': 'var_1', 'type': 'continuous', 'domain': (0,1)}]

# --- Solve your problem
myBopt = BayesianOptimization(f=f, domain=domain)
myBopt.run_optimization(max_iter=15)
myBopt.plot_acquisition()
```

#### 설정 파일 

```python 
# myfunc.py
def myfunc(x,y):
    return (4-2.1*x**2 + x**4/3)*x**2 + x*y + (-4 +4*y**2)*y**2
```

```json
# config.json
{
    "language"        : "PYTHON",
    "main-file"       : "myfunc.py",
    "experiment-name" : "simple-example",
    "likelihood"      : "gaussian",
    "resources": {
        "maximum-iterations" :  1,
        "max-run-time": "NA"
    },
    "variables" : {
        "y" : {
            "type" : "FLOAT",
            "size" : 1,
            "min"  : -3,
            "max"  : 3
        },
        "x" : {
            "type" : "FLOAT",
            "size" : 1,
            "min"  : -2,
            "max"  : 2
        }
    },
    "output":{
        "verbosity": true
    }
}
```

```python 
$ gpyopt.py ../myproblem/config.json
# `Evaluations.txt:`  containing the locations and values of the function evaluations.
# `Models.txt`: containing the parameters of all the models used.
```



## [Examples](https://nbviewer.jupyter.org/github/SheffieldML/GPyOpt/blob/devel/manual/GPyOpt_reference_manual.ipynb)

#### A. 1D example  /w  supported object
```python 
%pylab inline  
import GPy
import GPyOpt

# Create the true and perturbed Forrester function and the boundaries of the problem
f_true= GPyOpt.objective_examples.experiments1d.forrester()          # noisy version
bounds = [{'name': 'var_1', 'type': 'continuous', 'domain': (0,1)}]  # problem constraints 

#시각화 
#f_true.plot()
	"""pandas기반 시각화 
	#Plot the function 
	x = pd.Series(np.linspace(-5,4,1000))
	f_x = pd.Series.apply(x, obj_func)

	plt.plot(x, f_x, 'b-')
	plt.show()
	"""
# Creates GPyOpt object with the model and anquisition fucntion
seed(123)
myBopt = GPyOpt.methods.BayesianOptimization(f=f_true.f,            # function to optimize       
                                             domain=bounds,        # box-constraints of the problem
                                             acquisition_type='EI',
                                             exact_feval = True) # Selects the Expected improvement

# Run the optimization
max_iter = 15     # evaluation budget
max_time = 60     # time budget 
eps      = 10e-6  # Minimum allows distance between the las two observations

myBopt.run_optimization(max_iter, max_time, eps)   

#check the best found location x∗ by
myBopt.x_opt

#predicted value value of f at x∗ optimum by
myBopt.fx_opt

#그래프 결과(??) #In one dimensional examples
myBopt.plot_acquisition()

#그래프 결과(??) #In any dimensional examples
## The distance between the last two observations.
## The value of  ff  at the best location previous to each iteration.
myBopt.plot_convergence()

```

#### B. 2D example  /w  supported object 

```python 
%pylab inline  
import GPy
import GPyOpt

# create the object function
f_true = GPyOpt.objective_examples.experiments2d.sixhumpcamel()
f_sim = GPyOpt.objective_examples.experiments2d.sixhumpcamel(sd = 0.1)
bounds =[{'name': 'var_1', 'type': 'continuous', 'domain': f_true.bounds[0]},
         {'name': 'var_2', 'type': 'continuous', 'domain': f_true.bounds[1]}
         #{'name': 'var3', 'type': 'discrete', 'domain': (3,8,10),'dimensionality': 2}, # discrete Datatype
         #{'name': 'var4', 'type': 'categorical', 'domain': (0,1,2),'dimensionality': 1}, #categorical Datatype
		]

f_true.plot()

# Creates three identical objects that we will later use to compare the optimization strategies 

myBopt2D = GPyOpt.methods.BayesianOptimization(f_sim.f,
                                              domain=bounds,
                                              model_type = 'GP',
                                              acquisition_type='EI',  
                                              initial_design_numdata = 10,
                                              ##parallel Bayesian optimization
                                              #evaluator_type = 'local_penalization',
                                              #batch_size = 4,
                                              #num_cores = 4,
                                              normalize_Y = True,
                                              acquisition_weight = 2)  

# runs the optimization for the three methods
max_iter = 40  # maximum time 40 iterations
max_time = 60  # maximum time 60 seconds

myBopt2D.run_optimization(max_iter,max_time,verbosity=False)

myBopt2D.plot_acquisition()
myBopt2D.plot_convergence()


```

#### C. 2D example  /w  Own object 

> [Modular Bayesian Optimization](https://nbviewer.jupyter.org/github/SheffieldML/GPyOpt/blob/devel/manual/GPyOpt_modular_bayesian_optimization.ipynb)

#### D. Scikit-learn


```python 

%pylab inline  
import GPy
import GPyOpt
import numpy as np
from sklearn import svm
from numpy.random import seed
seed(12345)

# Let's load the dataset
## https://raw.githubusercontent.com/NYXFLOWER/Machine-Learning/master/warm/olympicMarathonTimes.csv
GPy.util.datasets.authorize_download = lambda x: True # prevents requesting authorization for download.
data = GPy.util.datasets.olympic_marathon_men()
X = data['X']
Y = data['Y']
X_train = X[:20]
Y_train = Y[:20,0]
X_test = X[20:]
Y_test = Y[20:,0]


nfold = 3

def fit_svr_val(x):
    x = np.atleast_2d(np.exp(x))
    fs = np.zeros((x.shape[0],1))
    for i in range(x.shape[0]):
        fs[i] = 0
        for n in range(nfold):
            idx = np.array(range(X_train.shape[0]))
            idx_valid = np.logical_and(idx>=X_train.shape[0]/nfold*n, idx<X_train.shape[0]/nfold*(n+1))
            idx_train = np.logical_not(idx_valid)
            svr = svm.SVR(C=x[i,0], epsilon=x[i,1],gamma=x[i,2])
            svr.fit(X_train[idx_train],Y_train[idx_train])
            fs[i] += np.sqrt(np.square(svr.predict(X_train[idx_valid])-Y_train[idx_valid]).mean())
        fs[i] *= 1./nfold
    return fs

## -- Note that similar wrapper functions can be used to tune other Scikit-learn methods


domain       =[{'name': 'C',      'type': 'continuous', 'domain': (0.,7.)},
               {'name': 'epsilon','type': 'continuous', 'domain': (-12.,-2.)},
               {'name': 'gamma',  'type': 'continuous', 'domain': (-12.,-2.)}]
               

opt = GPyOpt.methods.BayesianOptimization(f = fit_svr_val,            # function to optimize       
                                          domain = domain,         # box-constraints of the problem
                                          acquisition_type ='LCB',       # LCB acquisition
                                          acquisition_weight = 0.1)   # Exploration exploitation
                                          
# it may take a few seconds
opt.run_optimization(max_iter=50)
opt.plot_convergence()

x_best = np.exp(opt.X[np.argmin(opt.Y)])
print("The best parameters obtained: C="+str(x_best[0])+", epilson="+str(x_best[1])+", gamma="+str(x_best[2]))
svr = svm.SVR(C=x_best[0], epsilon=x_best[1],gamma=x_best[2])

## Baseline wo BO
# print("The default parameters obtained: C="+str(svr.C)+", epilson="+str(svr.epsilon)+", gamma="+str(svr.gamma))
# svr = svm.SVR()

svr.fit(X_train,Y_train)
Y_train_pred = svr.predict(X_train)
Y_test_pred = svr.predict(X_test)

plot(X_train,Y_train_pred,'b',label='pred-train')
plot(X_test,Y_test_pred,'g',label='pred-test')
plot(X_train,Y_train,'rx',label='ground truth')
plot(X_test,Y_test,'rx')
legend(loc='best')
print("RMSE = "+str(np.sqrt(np.square(Y_test_pred-Y_test).mean())))

```


> [GPyOpt: configuring Scikit-learn methods](https://nbviewer.jupyter.org/github/SheffieldML/GPyOpt/blob/devel/manual/GPyOpt_scikitlearn.ipynb)



#### E. Integrating the model hyperparameters


[GPyOpt: Integrating the model hyperparameters](https://nbviewer.jupyter.org/github/SheffieldML/GPyOpt/blob/devel/manual/GPyOpt_integrating_model_hyperparameters.ipynb)



---
- [Three things to help you get started on Bayesian Optimisation](https://www.blopig.com/blog/2019/09/three-things-to-help-you-get-started-on-bayesian-optimisation/)
	- [Nando de Freitas’ lecture on Bayesian optimization and multi-armed bandits](https://www.youtube.com/watch?v=vz3D36VXefI) : youtube강좌, 1:20분 

- [[추천] BAYESIAN OPTIMISATION WITH GPyOPT](https://www.blopig.com/blog/wp-content/uploads/2019/10/GPyOpt-Tutorial1.html)


