# Ex.No: 13 Learning – Use Supervised Learning  
### DATE:                                                                      
### REGISTER NUMBER : 212221040184
### AIM: 
To write a program to train the classifier for Diabetes Prediction.
###  Algorithm:
Start the program.
Import required Python libraries, including NumPy, Pandas, Google Colab, Gradio, and various scikit-learn modules.
Mount Google Drive using Google Colab's 'drive.mount()' method to access the data file located in Google Drive.
Install the Gradio library using 'pip install gradio'.
Load the diabetes dataset from a CSV file ('diabetes.csv') using Pandas.
Separate the target variable ('Outcome') from the input features and Scale the input features using the StandardScaler from scikit-learn.
Create a multi-layer perceptron (MLP) classifier model using scikit-learn's 'MLPClassifier'.
Train the model using the training data (x_train and y_train).
Define a function named 'diabetes' that takes input parameters for various features and Use the trained machine learning model to predict the outcome based on the input features.
Create a Gradio interface using 'gr.Interface' and Specify the function to be used to make predictions based on user inputs.
Launch the Gradio web application, enabling sharing, to allow users to input their data and get predictions regarding diabetes risk.
Stop the program.
### Program:
from google.colab import drive
drive.mount('/content/gdrive')
#import packages
import numpy as np
import pandas as pd
pip install gradio
pip install typing-extensions --upgrade
!python --version
 pip install --upgrade typing
import gradio as gr
import pandas as pd
cd /content/gdrive/MyDrive/demo/gradio_project-main
#get the data
data = pd.read_csv('diabetes.csv')
data.head()
print(data.columns)
x = data.drop(['Outcome'], axis=1)
y = data['Outcome']
print(x[:5])
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
outputs = gr.Textbox()
app = gr.Interface(fn=diabetes, inputs=['number','number','number','number','number','number','number','number'], outputs=outputs,description="Detection of Diabeties")
app.launch(share=True)

### Output:
![image](https://github.com/user-attachments/assets/f418b140-f6cd-4718-8811-da876021fb98)
![image](https://github.com/user-attachments/assets/a9b7659d-57f0-412e-a1d7-3d32912745df)
![image](https://github.com/user-attachments/assets/d42ef3a5-edef-4543-86ea-2833ba8ed398)
![image](https://github.com/user-attachments/assets/00b07bd4-d54e-4526-b305-94f4f8c9b4a4)
![image](https://github.com/user-attachments/assets/b4568349-5a9d-4280-96b5-0e933d36ffca)

### Result:
Thus the system was trained successfully and the prediction was carried out.
