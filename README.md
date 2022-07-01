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

# Results and Conclusions

Results and conclusions
The best result from single audio parameters was shown by mfcc. Separate chroma_stft, chromagram, etc. showed no results. Concatenate "small" features like chroma_stft gives a result comparable to the spectrum of stft.

For further research, we settled on mfcc

The diphthong [ai] gave an error during recognition: the classifier recognized both the sound [ai] and some sounds [a], [i].

# Classifier evaluation data:
true recognized sounds: 192

sounds recognized as true but not true: 159

recognized as false, but they are true: 64

recognized as false - and they are false: 1632

Word Recognition Rate: 89.11%

Word Error Rate: 10.89%

Accuracy: 0.55

Fullness: 0.75

Harmonic mean: 0.63

Conclusion: there is no point in classifying diphthongs, it is better to take individual sounds.

Used yTest, yTrain of 0 and 1 where there was no target sound and there was a target sound.

The classifier showed rise and fall in probability with a peak corresponding to 1 in yTrain, yTest.

In further work, use yTrain, yTest, which indicates lower sound probabilities. For example, where the sound [b] has not yet ended, and the sound [a] has just begun, put not 1 or 0, but a percentage: 0.7, 0.8, 0.9, 1.0, 1.0, 1.0, 0.9, 0.8. This can improve the accuracy of predictions.

# Autoencoder recognition data:
The predicted sounds [ai] when processed by the autoencoder did not make it possible to use bias to filter out "clean" and "not clean" sounds. The error boundaries overlapped completely, the mean values almost coincided.

Therefore, we used a trained classifier and ran the predicted sounds through it. We got the probability that each of the sounds belongs to [ai].

The resulting probability was sometimes greater than 1, sometimes much less. It may be worth adding some kind of normalization or an additional softmax layer.

It can be assumed that this probability correlates with the purity of the sound.

#I checked each of the recognized sounds by ear. Patterns:
the autoencoder more often supports the female voice. The test sample was chosen at random; perhaps it has more female voices.

in general, the autoencoder reflects the "purity" of pronunciation. Those that recognized the classifier but did not recognize the autoencoder were often more deaf.

The sounds that are fed to the autoencoder are clipped in the classification. Perhaps you should change n_fft and set a larger plus or minus of 500-1000 units.

#Experiment on preprocessing min-max scaler and standard scaler. Patterns:
MinMaxScaler gives more precision. Sound boundaries are wider. Fewer sounds are recognized in one track. Accuracy is improved by filtering out false positives. You can trust the average more. The Autoencoder has more support for the classifier - more values ​​other than 0 compared to the StandardScaler.

An experiment on preprocessing a training set on a prepared autoencoder.
In theory, "extra" sounds should be extinguished. In practice, sounds were recognized a little "dirtier" - neighboring ones were captured. But, unlike others, he gave the best prediction for 2 target sounds in a word.

Models were trained mainly on one-two-three-syllable words. Long sentences increase the margin of error.

##Conclusions on Improving Accuracy
For reference samples of sounds, you can set additional statistical indicators, such as the average length of the sound, standard deviation. New sounds can be compared with these indicators, and if the neural network recognized a sound with a length of 100, and the average length of a sound is 10 and the standard deviation is 3, then the recognized sound can be rejected with a high probability.

In most cases, the sounds [a], [i] gave a pitch comparable to the diphthong [ai]. Conclusion: to improve accuracy, train on individual vowels.

For the final selection of sounds, use the average accuracy between the classifier and the autoencoder.
