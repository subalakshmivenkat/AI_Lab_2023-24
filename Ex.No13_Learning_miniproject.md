# Ex.No: 13 Learning – Use Supervised Learning  
                                                                     
### REGISTER NUMBER : 212222040162
### AIM: 
To write a program to train the classifier for Diabetes Prediction.
### Algorithm:
1.Start the program.

2.Import required Python libraries, including NumPy, Pandas, Google Colab, Gradio, and various scikit-learn modules.

3.Mount Google Drive using Google Colab's 'drive.mount()' method to access the data file located in Google Drive.

4.Install the Gradio library using 'pip install gradio'.

5.Load the diabetes dataset from a CSV file ('diabetes.csv') using Pandas.

6.Separate the target variable ('Outcome') from the input features and Scale the input features using the StandardScaler from scikit-learn.

7.Create a multi-layer perceptron (MLP) classifier model using scikit-learn's 'MLPClassifier'.

8.Train the model using the training data (x_train and y_train).

9.Define a function named 'diabetes' that takes input parameters for various features and Use the trained machine learning model to predict the outcome based on the input features.

10.Create a Gradio interface using 'gr.Interface' and Specify the function to be used to make predictions based on user inputs.

11.Launch the Gradio web application, enabling sharing, to allow users to input their data and get predictions regarding diabetes risk.

12.Stop the program.

### Program:
```
#import packages
import numpy as np
import pandas as pd

from google.colab import drive
drive.mount('/content/gdrive')

pip install gradio

pip install typing-extensions --upgrade

import gradio as gr

cd /content/gdrive/MyDrive/demo/gradio_project-main

#get the data
data = pd.read_csv('diabetes.csv')
data.head()

print(data.columns)

x = data.drop(['Outcome'], axis=1)
y = data['Outcome']
print(x[:5])

from multi_imbalance.utils.plot import plot_cardinality_and_2d_data
plot_cardinality_and_2d_data(x, y, 'PIMA Diabetes Prediction Data set')

#split data
from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test= train_test_split(x,y)

#scale data
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
x_train_scaled = scaler.fit_transform(x_train)
x_test_scaled = scaler.fit_transform(x_test)

#instatiate model
from sklearn.neural_network import MLPClassifier
model = MLPClassifier(max_iter=1000, alpha=1)
model.fit(x_train, y_train)
print("Model Accuracy on training set:", model.score(x_train, y_train))
print("Model Accuracy on Test Set:", model.score(x_test, y_test))

print(data.columns)

#create a function for gradio
def diabetes(Pregnancies, Glucose, Blood_Pressure, SkinThickness, Insulin, BMI,Diabetes_Pedigree, Age):
    x = np.array([Pregnancies,Glucose,Blood_Pressure,SkinThickness,Insulin,BMI,Diabetes_Pedigree,Age])
    prediction = model.predict(x.reshape(1, -1))
    if(prediction==0):
      return "NO"
    else:
      return "YES"

#create a function for gradio
def diabetes(Pregnancies, Glucose, Blood_Pressure, SkinThickness, Insulin, BMI,Diabetes_Pedigree, Age):
    x = np.array([Pregnancies,Glucose,Blood_Pressure,SkinThickness,Insulin,BMI,Diabetes_Pedigree,Age])
    prediction = model.predict(x.reshape(1, -1))
    return prediction

outputs = gr.outputs.Textbox()
app = gr.Interface(fn=diabetes, inputs=['number','number','number','number','number','number','number','number'], outputs=outputs,description="Detection of Diabeties")
app.launch(share=True)
```

### Output:

![Screenshot 2024-11-11 160646](https://github.com/user-attachments/assets/b682f907-ae8d-462e-92de-0681ada725a6)



![Screenshot 2024-11-11 160658](https://github.com/user-attachments/assets/c69050ad-c5ef-46c8-9410-388b304ca9d6)



![Screenshot 2024-10-10 135744](https://github.com/user-attachments/assets/12e60eb2-9283-416b-b6d0-010a1e7b96be)



### Result:
Thus the system was trained successfully and the prediction was carried out.
