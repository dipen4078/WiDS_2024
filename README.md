# WiDS_2024
## Paper A: CLiP
- CLiP(Contrastive Language-Image Pretraining) is a zero shot classifier which predicts text from images without any fine tuning or proper training.
- In this model we just ask the model how likely is our class labels to match the image and then select the class with highest probability.
- Quality of classifier (accuracy) depends not only on labels but also on prompt. This is also known as Prompt Engineering which highlights the significance of how structure of queries outcome changes.
### TRAINING:(Image classifier)
    - Given: Bunch of images(n) with it's correct phrase 
    - Encode the images and text
    - What we do is instead of asking the model to predict what is it's phrase we ask the model that out of which of the following phrases which one is most likely to be correct.
    - Our aim is to maximise the response of correct one and minimise the response of incorrect ones.
- Transformer Language Model is thrice worse off than a simple bag of words prediction while CLiP is four times more efficient than bag of words prediction.
### Zero Shot CLiP vs ResNet-50:
    - A zero shot CLiP outperforms ResNet-50 which was trained on 16 datasets.
    - ResNet50 was also trained with ImageNet while zeroshot CLiP outperforms ResNet-50 in ImageNet.
### Zero Shot CLiP:
    - Zero Shot CLiP does not mean no training it just means no training on input data/classes.
    - This means that it does not require additional learning from new tasks it just uses what it is previously trained.
    - Not fine tuned.
### Linear Probe CLiP:
    - Use a simple linear classifier to make a new model which trains on the datasets.
    - We don't modify CLiP we just change the classifier.
- Pretraining in CLiP is very huge.(It trains on large scale internet data)
- Zero shot Clip also outperforms some few shot CLiP
- CLiP also shows remarkable resilience against when exposed to variations in datasets while standard models fails miserably under variations while CLiP maintains its performance.
- Performance of CLiP was also compared with humans. It was found that most images which were difficult for CLiP were also difficult for humans.
- Performance of CLiP is poor when it comes to fine grained classifications like differentiating within a species. It also struggle on counting the number of objects.


## Paper B: CoOp
- CoOp(Context Optimization) aims to improve zero shot CLiP by giving better prompts as identifying right prompt for CLiP is non trivial.
- As Prompts play a significant role in CLiP Model CoOp improves the accuracy of zero shot CLiP by a significant margin.
- Models prompt's context words with learnable vectors which could be initialized with random vectors or pre trained word embeddings
  ### Two main implementations of CoOp based on above options
      a) Based on unified context - shares same context with all classes
      b) Based on class specific context - learns specific set of context tokens for each class and is found to be more suitable for fine grained categories.
- Outperforms hand crafted prompts and linear probe CLiP model within just a few shots of CoOp.
  ### Training :
    - Here we encode the text using text encoder and then obtain a classification weight vector.
    - Put Class token anywhere in the encoded vector and train according to the implementation.
    - Loss computation is done by Cross Entropy Loss function.
  ### Results :
    - CoOp + CLiP shows clear advantage over Linear Probe CLiP as latter requires four shot training to reach threshold of zero shot CLiP while this model on four shots is already 15% more accurate than Zero Shot CLiP.
  ### Limitations :
  - Overfits for small datasets if not regulated properly.

## Paper C: Vision Language Models
- Vision Language Models aka VLMs are higher order of CLiP which are AI models which can understand both image and text together. Eg:- CLiP, BLiP, ALIGN
- Normal CLiP models don't perform any good on imbalanced datasets and fine grained rare classes.
  #### The approaches to the issue of imbalanced classification :
        a) Loss function engineering - Adjust weight of losses of different classes to achive more balanced distribution.
        b) 2 stage decision boundary adjustment - decision boundary adjustment.
        c) Other methods : transfer learning, task specific architecture design, domain adaptation.
- CoOp and CoCoOp just does prompt tuning which is not specifically designed for imbalanced learning tasks as it just aims to create similarity between every image.
- Fine tuning model on just the added classifier layer of the CLiP model would not be sufficient.
  ### Steps:
  - We do not use the text decoder and use a lightweight decoder instead output of this decoder will be given to classifier and the classification scores can be adjusted for making more balanced dataset.
  #### There are three ways in which we can train the dataset classifier:
      a) Training by instance based sampling and cross entropy loss
      b) Training by class specific loss
      c) Training by two stage algorithms
  ### Results:
   - Strong zero shot predictions on ImageNet-LT
   - Decoder with softmax outperforms prompt tuning
  ### Limitations:
   - Vulnerable to small modifications in image/text to trick the model.   
