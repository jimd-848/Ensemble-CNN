# Ensemble-CNN

Goal - Repurpose several baseline models that solve the CIFAR-10 dataset and ensemble them together using various methods. <br />
All models use categorical crossentropy loss and final activaion layer is softmax. <br />
"Best model" is the epoch which had the lowest validation loss. <br />
*Transfer and ensemble models may not load properly due to use of lambda layer in model.

# custom_1
Architecture taken from https://towardsdatascience.com/cifar-10-image-classification-in-tensorflow-5b501f7dc77c <br />
Best model results: Epoch 8/100 <br />
98/98 [==============================] - 2s 20ms/step - loss: 0.2981 - categorical_accuracy: 0.8995 - auc: 0.9937 - val_loss: 0.7924 - val_categorical_accuracy: 0.7741 - val_auc: 0.9635

# custom_2
Architecture taken from https://www.tensorflow.org/tutorials/images/cnn <br />
Best model results: Epoch 22/100 <br />
98/98 [==============================] - 1s 8ms/step - loss: 0.6852 - categorical_accuracy: 0.7654 - auc: 0.9736 - val_loss: 1.0044 - val_categorical_accuracy: 0.6615 - val_auc: 0.9426

# custom_vgglike
Architecture taken from https://machinelearningmastery.com/how-to-develop-a-cnn-from-scratch-for-cifar-10-photo-classification/ <br />
Best model results: Epoch 195/200 <br />
98/98 [==============================] - 1s 15ms/step - loss: 0.6192 - categorical_accuracy: 0.7816 - auc: 0.9775 - val_loss: 0.6191 - val_categorical_accuracy: 0.7853 - val_auc: 0.9770

# transfer_densenet
Transfer learning from DenseNet121.  Top of network is left off and custom dense layers are implimented, imagenet weights are loaded.  All CNN layers are frozen for training. <br />
Architecture taken from https://medium.com/swlh/hands-on-the-cifar-10-dataset-with-transfer-learning-2e768fd6c318 <br />
Best model results: Epoch 7/50 <br />
98/98 [==============================] - 25s 256ms/step - loss: 0.4091 - categorical_accuracy: 0.8642 - auc: 0.9886 - val_loss: 0.4763 - val_categorical_accuracy: 0.8412 - val_auc: 0.9849

# ensemble_avg
Ensemble model containing all baseline models.  Output of each model is averaged together to get final class probabilities.  No additional training required. <br />
Model results: val_loss: 0.4978346824645996 - val_categorical_accuracy: 0.845300018787384 - val_auc: 0.988166093826294 <br />

# reduced_ensemble_avg
Same as above except only custom_1 and custom_2 are included in the ensemble. <br />
Model results: val_loss: 0.716093897819519 - val_categorical_accuracy: 0.7791000008583069 - val_auc: 0.9688507914543152 <br />

# ensemble_logreg
Ensemble model containing all baseline models, all weights are untrainable in the baseline models.  Output of each model is concatenated and then connected to softmax layer which is the equivalent of running a logistic regression on all the ouputs. <br />
Best model results: Epoch 29/50 <br />
98/98 [==============================] - 21s 212ms/step - loss: 0.1896 - categorical_accuracy: 0.9493 - auc: 0.9979 - val_loss: 0.4653 - val_categorical_accuracy: 0.8515 - val_auc: 0.9853

# ensemble_dl
Ensemble model containing all baseline models, all weights are untrainable in the baseline models.  Output of each model is concatenated and then connected to another neural net for final classification. <br />
Best model results: Epoch 4/50 <br />
98/98 [==============================] - 21s 214ms/step - loss: 0.1919 - categorical_accuracy: 0.9476 - auc: 0.9953 - val_loss: 0.4720 - val_categorical_accuracy: 0.8535 - val_auc: 0.9843

# Conclustions
As expected, the ensemble models only show a very slight improvement over the best baseline it contains (custom_1 for reduced, transfer_densenet for every other model).  It is good to note that inclusion of a poor model (custom_2) does not drag down the results of the ensemble models.  The baseline models can be further tuned to improve results.
