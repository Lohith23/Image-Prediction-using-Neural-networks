# Image-Prediction-using-Neural-networks

import tensorflow as tf
from tensorflow import keras
import numpy as np
import matplotlib.pyplot as plt

data = keras.datasets.fashion_mnist

(train_images, train_labels), (test_images, test_labels) = data.load_data()

Class_names = ['t-shirt/top', 'trousers', 'Pullover', 'Dress', 'Coat', 'sandal', 'shirt', 'sneaker', 'Bag', 'Ankle boot']
train_images = train_images/255.0
test_images = test_images/255.0

Model = keras.Sequential([
       keras.layers.Flatten(input_shape=(28,28)),
       keras.layers.Dense(128, activation="relu"),
       keras.layers.Dense(10, activation="softmax")
       ])

Model.compile(optimizer="adam", loss="sparse_categorical_crossentropy", metrics=["accuracy"])

Model.fit(train_images, train_labels, epochs=5)

prediction = Model.predict(test_images)

for i in range(5):
    plt.grid(False)
    plt.imshow(test_images[i], cmap=plt.cm.binary)
    plt.xlabel("Actual: " + Class_names[test_labels[i]])
    plt.title("Prediction" + Class_names[np.argmax(prediction[i])])
    plt.show()
