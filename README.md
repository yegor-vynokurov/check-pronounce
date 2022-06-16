# Accuracy of pronounciation

**Goal**: to create a neural network that recognizes the sounds of English speech and evaluates the quality of pronunciation.

**Purpose**: using examples of the diphthong [ai] to get the most possible significant differences.

**Method**: combination of classifier and autoencoder.

For the classifier, a training set of 120 words with diphthongs [ai] was used:

https://drive.google.com/drive/folders/11_MFr0WoAqVkHqhYQuWFCEb9lL5ZA8pu?usp=sharing

Classification accuracy was evaluated on a test set of 30 words:

https://drive.google.com/drive/folders/1VNxNB1f-TLgYfF1wEKiX5x-2pE861Sqq?usp=sharing

The selected sounds [ai] from the training sample were used to train the autoencoder.

yTrain, yTest were collected in a semi-automatic mode: an audio recording was listened to, places where the required sound was present were marked, marks were added to the list. The program, in accordance with the labels, created the correct answers and cut the sounds for the autoencoder.

The words are collected from the site https://ru.forvo.com, where native speakers voice the words. Words were selected only with a positive index for those who voiced.

# Точность произношения звуков английского языка. 

**Цель**: создать нейронную сеть, которая распознаёт звуки английского языка и оценивает качество их произношения. 

**Замысел**: использовать дифтонг [ai] и получить наиболее возможные значимые отличия. 

**Метод**: комбинация классификатора и автоэнкодера. 

Для классификатора использована тренировочная выборка из 120 слов с дифтонгами [ai]: https://drive.google.com/drive/folders/11_MFr0WoAqVkHqhYQuWFCEb9lL5ZA8pu?usp=sharing

Точность классификации оценивалась на тестовой выборке в 30 слов: https://drive.google.com/drive/folders/1VNxNB1f-TLgYfF1wEKiX5x-2pE861Sqq?usp=sharing

Для тренировки автоэнкодера использовались выделенные звуки [ai] из тренировочной выборки. 

yTrain, yTest  собирались в полуавтоматическом режиме: прослушивалась аудиозапись, отмечались места, где присутствует требуемый звук, метки вносились в список. Программа в соответствии с метками создавала правильные ответы и нарезала звуки для автоэнкодера. 

Слова собраны с сайта https://ru.forvo.com, где носители языка озвучивают слова. Отбирались слова только с положительным индексом для тех, кто озвучивал.
"""
