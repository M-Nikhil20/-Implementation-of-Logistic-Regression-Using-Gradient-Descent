# Implementation-of-Logistic-Regression-Using-Gradient-Descent

## AIM:
To write a program to implement the the Logistic Regression Using Gradient Descent.

## Equipments Required:
1. Hardware – PCs
2. Anaconda – Python 3.7 Installation / Jupyter notebook

## Algorithm
1. Import the required libraries.
2. Load the dataset.
3. Define X and Y array.
4. Define a function for costFunction,cost and gradient.
5. Define a function to plot the decision boundary.
6. 6.Define a function to predict the Regression value.

## Program:
```
/*
Program to implement the the Logistic Regression Using Gradient Descent.
Developed by: M Nikhil
RegisterNumber:  212222230095
*/
```
```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import optimize
data = np.loadtxt("ex2data1.txt", delimiter =',')
x = data[:,[0,1]]
y = data[:,2]

x[:5]
y[:5]

plt.figure()
plt.scatter(x[y == 1][:,0],x[y == 1][:,1],label="Admitted")
plt.scatter(x[y == 0][:,0],x[y == 0][:,1],label="Not Admitted")
plt.xlabel("Exam 1 Score")
plt.ylabel("Exam 2 Score")
plt.legend()
plt.show()

def sigmoid(z):
  return 1/(1+np.exp(-z))

plt.plot()
x_plot = np.linspace(-10,10,100)
plt.plot(x_plot, sigmoid(x_plot),color="pink")
plt.show()

def costFunction(theta,x,y):
  h = sigmoid(np.dot(x,theta))
  j = -(np.dot(y,np.log(h)) + np.dot(1 - y, np.log(1 - h)))/x.shape[0]
  grad = np.dot(x.T,h - y) / x.shape[0]
  return j,grad

x_train = np.hstack((np.ones((x.shape[0],1)),x))
theta = np.array([0, 0, 0])
j,grad = costFunction(theta, x_train, y)
print(j)
print(grad)

x_train = np.hstack((np.ones((x.shape[0], 1)),x))
theta = np.array([-24, 0.2, 0.2])
j, grad = costFunction(theta, x_train, y)
print(j)
print(grad)

def cost(theta, x, y):
  h = sigmoid(np.dot(x, theta))
  j = -(np.dot(y, np.log(h)) + np.dot(1 - y, np.log(1 -h)))/x.shape[0]
  return j

def gradient(theta, x, y):
  h = sigmoid(np.dot(x, theta))
  grad = np.dot(x.T, h - y)/x.shape[0]
  return grad

x_train = np.hstack((np.ones((x.shape[0], 1)),x))
theta = np.array([0, 0, 0])
res = optimize.minimize(fun = cost, x0 = theta, args = (x_train, y), method = 'Newton-CG', jac = gradient)
print(res.fun)
print(res.x)

def plotDecisionBoundary(theta, x, y):
  x_min, x_max = x[:, 0].min() - 1,x[:, 0].max() + 1
  y_min, y_max = x[:, 1].min() - 1,x[:, 1].max() + 1
  xx, yy = np.meshgrid(np.arange(x_min,x_max,0.1), np.arange(y_min, y_max, 0.1))
  x_plot = np.c_[xx.ravel(), yy.ravel()]
  x_plot = np.hstack((np.ones((x_plot.shape[0], 1)), x_plot))
  y_plot = np.dot(x_plot, theta).reshape(xx.shape)

  plt.figure()
  plt.scatter(x[y == 1][:, 0], x[y == 1][:, 1], label="Admitted")
  plt.scatter(x[y == 0][:, 0], x[y == 0][:, 1], label="Not Admitted")
  plt.contour(xx, yy, y_plot, levels=[0])
  plt.xlabel("Exam 1 Score")
  plt.ylabel("Exam 2 Score")
  plt.legend()
  plt.show()

plotDecisionBoundary(res.x, x, y)

prob = sigmoid(np.dot(np.array([1, 45, 85]),res.x))
print(prob)

def predict(theta, x):
  x_train = np.hstack((np.ones((x.shape[0], 1)), x))
  prob = sigmoid(np.dot(x_train, theta))
  return (prob >= 0.5).astype(int)

np.mean(predict(res.x, x) == y)
```

## Output:
## ARRAY VALUE OF X
![image](https://github.com/M-Nikhil20/-Implementation-of-Logistic-Regression-Using-Gradient-Descent/assets/118707852/f1416f60-430f-4e59-a3dd-6675a109b901)

## ARRAY VALUE OF Y
![image](https://github.com/M-Nikhil20/-Implementation-of-Logistic-Regression-Using-Gradient-Descent/assets/118707852/92735562-d863-49ca-b823-fdc3fed2e9c9)

## EXAM 1 - SCORE GRAPH
![image](https://github.com/M-Nikhil20/-Implementation-of-Logistic-Regression-Using-Gradient-Descent/assets/118707852/f011985f-64c2-4fcc-b2f9-1872f77e3a02)

## SIGMOID FUNCTION GRAPH
![image](https://github.com/M-Nikhil20/-Implementation-of-Logistic-Regression-Using-Gradient-Descent/assets/118707852/67d0500f-52f1-4fea-9cdd-dddcb0ef038b)

## X_TRAIN_GRAD VALUE
![image](https://github.com/M-Nikhil20/-Implementation-of-Logistic-Regression-Using-Gradient-Descent/assets/118707852/2878b028-4a21-4eb6-84d9-29ff0902ce78)

## Y_TRAIN_GRAD VALUE
![image](https://github.com/M-Nikhil20/-Implementation-of-Logistic-Regression-Using-Gradient-Descent/assets/118707852/f0c8c618-9c24-442d-bf63-a3caed77edc2)

## PRINT RES.X
![image](https://github.com/M-Nikhil20/-Implementation-of-Logistic-Regression-Using-Gradient-Descent/assets/118707852/19880729-ee5d-495d-be32-b4faaa431054)

## DECISION BOUNDARY GRAPH FOR EXAM SCORE
![image](https://github.com/M-Nikhil20/-Implementation-of-Logistic-Regression-Using-Gradient-Descent/assets/118707852/547a8099-a744-4ab9-9b79-a991f60df9f4)

## PROBABILITY VALUE
![image](https://github.com/M-Nikhil20/-Implementation-of-Logistic-Regression-Using-Gradient-Descent/assets/118707852/783963e4-b86f-4fda-a0e8-6d4988818857)

## PREDICTION VALUE OF MEAN
![image](https://github.com/M-Nikhil20/-Implementation-of-Logistic-Regression-Using-Gradient-Descent/assets/118707852/a8c0dd8b-48b8-45a9-811b-41c608e6a140)

## Result:
Thus the program to implement the the Logistic Regression Using Gradient Descent is written and verified using python programming.
