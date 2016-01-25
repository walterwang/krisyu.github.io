###class Holder

这里的holder其实仅仅是一个dictionary.

```
class Holder:
    factors={}  #Initialize an empty dictionary
    attributes = ()  #declaration of dictionaries parameters with an arbitrary length
        
    '''
    Constructor of class Holder holding two parameters, 
    self refers to the instance of the class
    '''
    
    def __init__(self,attr):  #
        self.attributes = attr
        for i in attr:
            self.factors[i]=[]
            
            
    def add_values(self,factor,values):
        self.factors[factor]=values
        
```



把holder这个class加上这一段代码运行一下，其实就是得到字典：

```
f = Holder(attributes)
```
初始化f，这个时候：

```
>>> f.factors
{'Water': [], 'Wind': [], 'Humidity': [], 'Temp': [], 'Sky': [], 'Forecast': []}
>>> f.attributes
('Sky', 'Temp', 'Humidity', 'Wind', 'Water', 'Forecast')
```


运行以下代码之后：


```
f.add_values('Sky',('sunny','rainy','cloudy')) #sky can be sunny rainy or cloudy
f.add_values('Temp',('cold','warm')) #Temp can be sunny cold or warm
f.add_values('Humidity',('normal','high')) #Humidity can be normal or high
f.add_values('Wind',('weak','strong')) #wind can be weak or strong
f.add_values('Water',('warm','cold')) #water can be warm or cold
f.add_values('Forecast',('same','change')) #Forecast can be same or change
```

此时f变为：

```
>>> f.factors
{'Water': ('warm', 'cold'), 'Wind': ('weak', 'strong'), 'Humidity': ('normal', 'high'), 'Temp': ('cold', 'warm'), 'Sky': ('sunny', 'rainy', 'cloudy'), 'Forecast': ('same', 'change')}

>>> f.attributes
('Sky', 'Temp', 'Humidity', 'Wind', 'Water', 'Forecast')
```


这里的Holder就是一个字典|||


一开始吓得我都不敢看这个代码||||



###class CandidateElimination


####init
首先一来还是先看到instructor（假装so）:

```
class CandidateElimination:

	 def __init__(self,data,fact):
	     self.num_factors = len(data[0][0])
	     self.factors = fact.factors
	     self.attr = fact.attributes
	     self.dataset = data

```

实际上调用的时候用的语句是：

```
#dataset is here:
dataset=[(('sunny','warm','normal','strong','warm','same'),'Y'),(('sunny','warm','high','strong','warm','same'),'Y'),(('rainy','cold','high','strong','warm','change'),'N'),(('sunny','warm','high','strong','cool','change'),'Y')]

a = CandidateElimination(dataset,f)
```

所以有意思的点在于：就是这个可以直接调用比如fact.factors, fact.attributes,还有的点在于其实len（data[0][0]）,但是其实直接可以用len(f.attributes) 或者 len(f.factors)，因为f这个dictionary本来就是给算法用的，所以肯定是对应的...

然后很容易懂的代码还有：

####general hypotheses & specific hypotheses

```
def initializeS(self):
    ''' Initialize the specific boundary '''
    S = tuple(['-' for factor in range(self.num_factors)]) #6 constraints in the vector
    return [S]

def initializeG(self):
    ''' Initialize the general boundary '''
    G = tuple(['?' for factor in range(self.num_factors)]) # 6 constraints in the vector
    return [G]

```

运行之后 S 和 G 分别如：

```
G
[('?', '?', '?', '?', '?', '?')]
S
[('-', '-', '-', '-', '-', '-')]
```

#### check training set postive & negative 

```
def is_positive(self,trial_set):
    ''' Check if a given training trial_set is positive '''
    if trial_set[1] == 'Y':
        return True
    elif trial_set[1] == 'N':
        return False
    else:
        raise TypeError("invalid target value")

def is_negative(self,trial_set):
    ''' Check if a given training trial_set is negative '''
    if trial_set[1] == 'N':
        return False
    elif trial_set[1] == 'Y':
        return True
    else:
        raise TypeError("invalid target value")
            
```

#### core algorthim 来了（算法来了，我要想会）

好吧，决定要去问老师了....


