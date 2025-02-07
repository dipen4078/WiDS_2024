# WiDS_2024
## Paper A: CLiP
- CLiP(Contrastive Language-Image Pretraining) is a zero shot classifier which predicts text from images without any fine tuning or proper training.
- In this model we just ask the model how likely is our class labels to match the image and then select the class with highest probability.
- Quality of classifier (accuracy) depends not only on labels but also on prompt. This is also known as Prompt Engineering which highlights the significance of how structure of queries outcome changes.
- ### TRAINING:(Image classifier)
    - Given: Bunch of images(n) with it's correct phrase 
    - Encode the images and text
    - What we do is instead of asking the model to predict what is it's phrase we ask the model that out of which of the following phrases which one is most likely to be correct.
    - Our aim is to maximise the response of correct one and minimise the response of incorrect ones.
- Transformer Language Model is thrice worse off than a simple bag of words prediction while CLiP is four times more efficient than bag of words prediction.
- ### Zero Shot CLiP vs ResNet-50:
    - A zero shot CLiP outperforms ResNet-50 which was trained on 16 datasets.
    - ResNet50 was also trained with ImageNet while zeroshot CLiP outperforms ResNet-50 in ImageNet.
- ### Zero Shot CLiP:
    - Zero Shot CLiP does not mean no training it just means no training on input data/classes.
    - This means that it does not require additional learning from new tasks it just uses what it is previously trained.
    - Not fine tuned.
- ### Linear Probe CLiP:
    - Use a simple linear classifier to make a new model which trains on the datasets.
    - We don't modify CLiP we just change the classifier.
- Pretraining in CLiP is very huge.(It trains on large scale internet data)
- Zero shot Clip also outperforms some few shot CLiP
- CLiP also shows remarkable resilience against when exposed to variations in datasets while standard models fails miserably under variations while CLiP maintains its performance.
- Performance of CLiP was also compared with humans. It was found that most images which were difficult for CLiP were also difficult for humans.
- Performance of CLiP is poor when it comes to fine grained classifications like differentiating within a species. It also struggle on counting the number of objects.

  
