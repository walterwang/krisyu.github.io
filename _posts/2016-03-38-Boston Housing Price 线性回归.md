
# Boston Housing Price 线性回归

## 一维线性回归

这个知名的数据集是内建在sklearn package的:

boston这个type类似object

然后feature多,feature在boston.data，type是numpy的array



```
python
from sklearn.datasets import load_boston
boston = load_boston()

print(type(boston))
print(boston.data.shape)
print(type(boston.data))
print(boston.feature_names)
```

    <class 'sklearn.datasets.base.Bunch'>
    (506, 13)
    <class 'numpy.ndarray'>
    ['CRIM' 'ZN' 'INDUS' 'CHAS' 'NOX' 'RM' 'AGE' 'DIS' 'RAD' 'TAX' 'PTRATIO'
     'B' 'LSTAT']


这里我们只考虑属性RM,平均房间数。

%pylab inline 是用来配置画图，不生成单独窗口画图


```
python
%pylab inline
from matplotlib import pyplot as plt
plt.scatter(boston.data[:,5],boston.target)
plt.show()
```

    Populating the interactive namespace from numpy and matplotlib



![png](images/output_5_1.png)


这一句x = np.transpose(np.atleast_2d(x))改变了x的形状，但是它们都是numpy.ndarray

首先,x是一个一维的array，np.atleast_2d(x)把它变成了一个类似list的array，然后再转置，实际上感觉类似array转matrix的操作（？）

看到有做法也是这样的x = np.array([[v] for v in x])，验证x0 == x1

之所以要这样转换是因为LinearRegression的要求


```
python
from sklearn.linear_model import LinearRegression
lr = LinearRegression()

x = boston.data[:,5]
y = boston.target

print(x.shape)
print(len(np.atleast_2d(x)))
x = np.transpose(np.atleast_2d(x))
print(x.shape)
lr.fit(x,y)
y_predicted = lr.predict(x)
```

    (506,)
    1
    (506, 1)


画个图看看，可以看到这个sklearn的LinearRegression自带偏移量w.


```
python
plt.scatter(x,y,color = 'r',marker = 'o')
plt.plot(x, y_predicted)
```




    [<matplotlib.lines.Line2D at 0x114452b70>]




![png](images/output_9_1.png)



```python
from sklearn.metrics import mean_squared_error

mse = mean_squared_error(y,lr.predict(x))
print("Mean squared (error of training data) : {:.3}".format(mse))
```

    Mean squared (error of training data) : 43.6


rmse是root mean squre error(RMSE)
其意义是对于符合正态分布的状况，我们可以预估一般结果应该在predict±2*rmse


```python
rmse = np.sqrt(mse)
print("RMSE (of training data):{:.3}".format(rmse))
```

    RMSE (of training data):6.6


这个score我概念不大


```python
from sklearn.metrics import r2_score
r2 = r2_score(y,lr.predict(x))
print("R2 (on training data): {:.2}".format(r2))
```

    R2 (on training data): 0.48


## 多维线性回归

现在开始用所有的变量开始回归


```python
x = boston.data
y = boston.target
lr.fit(x,y)
```




    LinearRegression(copy_X=True, fit_intercept=True, n_jobs=1, normalize=False)



注意代码

画了散点

同时画了线plt.plot()

这里感觉是因为参数成功设置才能成功画线

比如用这一组参数plt.plot([0,5],[[1],[11]])

y = 2*x + 1成功

(http://matplotlib.org/users/pyplot_tutorial.html)


```python
p = lr.predict(x)
plt.scatter(p,y)
plt.xlabel('Predicted price')
plt.ylabel('Actual price')
#plt.plot()
plt.plot([y.min(),y.max()],[[y.min()],[y.max()]])
```




    [<matplotlib.lines.Line2D at 0x1147c3208>]




![png](images/output_19_1.png)


## Cross-validation

cross validation可以对classifier估计更精确。或者能帮助生成更好的classifier.


```python
from sklearn.cross_validation import KFold
kf = KFold(len(x),n_folds = 5)
p = np.zeros_like(y)
for train,test in kf:
    lr.fit(x[train],y[train])
    p[test] = lr.predict(x[test])
rmse_cv = np.sqrt(mean_squared_error(p,y))
print('RMSE on 5-fold CV:{:.2}'.format(rmse_cv))
```

    RMSE on 5-fold CV:6.1


## Regularization / Penalization

regularization 反正就是弄一个惩罚机制来防止overfitting.

bias-variance tradeoff,最终的结果是training set上准确率降低，但是test set（unseen data）准确率上升。

L1 是最小化sum(|w|)， L2 最小化sum(w^2)

L1的发明者 Lasso, L2 的发明者 Ridge Regression, L1 + L2一起用的，叫ElasticNet


```python
from sklearn.linear_model import ElasticNet, Lasso
en = ElasticNet(alpha = 0.5)
```

这里有待进一步研究


```python
las = Lasso(normalize = 1)
alphas = np.logspace(-5,2,1000)
alphas, coefs, _ = las.path(x ,y , alphas = alphas)

fig, ax = plt.subplots()
ax.plot(alphas,coefs.T)
# Set log scale
ax.set_xscale('log')
# Make alpha decrease from left to right
ax.set_xlim(alphas.max().alphas.min())
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-61-215c3fb28f2c> in <module>()
          8 ax.set_xscale('log')
          9 # Make alpha decrease from left to right
    ---> 10 ax.set_xlim(alphas.max().alphas.min())
    

    AttributeError: 'numpy.float64' object has no attribute 'alphas'



![png](images/output_27_1.png)

