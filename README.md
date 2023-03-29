# Siamese_signature
# Handwritten Signature Detection and Verification
Authentication is an important factor to manage security. Signatures are 
widely used for personal identification and verification. Many documents 
like legal transaction and bank cheque requires signature verification. 
Signature-based verification of a multiple number of documents is a time- 
consuming and difficult task. Consequently, an explosive growth has been 
seen in biometric personal verification and authentication systems  as 
traditional identity verification methods such as passwords, tokens, pins 
suffer  from  some  fatal  flaws  and  are  incapable  to  satisfy  security 
necessities. In this assignment you will be tasked with identifying whether 
a handwritten signature is real or forged and detecting the signature in a 
document.

## Either for Face Verification(anchor,positive,negative) or signature verification(real,real,forged),we use the Siamese Network.
One-shot learning is a classification task where one, or a few, examples are used to 
classify many new unknown examples in the future.
Face recognition tasks provide examples of one-shot learning. Specifically, in the case of 
face identification, a model or system may only have one or a few examples of a given 
person’s face and must correctly identify the person from new photographs with 
changes to expression, hairstyle, lighting, accessories, and more.
For example, suppose there is an organization, and it wants a facial recognition system to 
allow access to the building for its employees and you are given the task of building such 
a system. The problem with this task is that the organization might not have more than 
ten images for each of the employee. Therefore, building and training a typical 
convolutional neural network will not work as it cannot learn the features required with 
the given amount of data. So, this is a one-shot learning task where you build a similarity 
function which compares two images and tells you if it is the same person or not.
Modern face recognition systems approach the problem of one-shot learning via face 
recognition by learning a rich low-dimensional feature representation, called a face 
embedding, that can be calculated for faces easily and compared for verification and 
identification tasks.

![image](https://user-images.githubusercontent.com/98246082/228568997-f834c48d-c79e-4984-83ab-58a4b2fb6d95.png)


![image](https://user-images.githubusercontent.com/98246082/228569146-f45cc938-8b94-4e7d-bf7c-2e273e0991e7.png)

## Siamese Network
A network that has been popularized given its use for one-shot learning is the Siamese network. 
A Siamese network is an architecture with n-parallel neural networks, each taking a different 
input, sharing the weights and whose outputs are combined to provide some prediction.
In the case of face verification using a siamese networks, we take an input image of a person 
and find out the encodings of that image, then, we take the same network without performing 
any updates on weights or biases and input an image of a different person and again predict it’s 
encodings. Now, we compare these two encodings to check whether there is a similarity 
between the two images. These two encodings act as a feature representation of the images. 
Images with the same person have similar features/encodings. Using this, we compare and tell 
if the two images are of the same person or not. Based on a loss function, the weights are 
updated in the network (both branches have the same weights as it is the same network only 
with different inputs that are computed in parallel)

![image](https://user-images.githubusercontent.com/98246082/228569536-597ef2e1-42d2-42ed-afe9-5e91e43f9b41.png)

## Triplet Loss
The triplet loss function takes three, 128-D features generated from the above network. Let 
these three be known as an anchor, a positive, and a negative where: 

• Anchor: An image of a real signature of a person  that will be used for comparison.
• Positive: An image of a real signature of the same person  as that of the anchor.
• Negative: An image of of a forged signature of the same person  than the anchor.

![image](https://user-images.githubusercontent.com/98246082/228570474-65ce8eaa-5328-4b7f-a0cb-a72267b46f1d.png)


Triplet loss works in these steps:
1.   Sample three images from the dataset, the anchor, positive, and negative face. The 
anchor is any face, and the positive is an image of the same face as the anchor, and the 
negative is an image of a different face.
2.   Compute the vectors of each of the images (Extract Embeddings)
3.   Calculate Euclidean distance between Anchor image(a) and Positive image(p), Anchor 
image(a) and Negative image(n).
4.   The distance d(a,p) should be as small as possible, while the d(a,n) should be as big as 
possible.
5.   Make sure that d(a,p) is smaller than d(a,n) by a margin alpha.

![image](https://user-images.githubusercontent.com/98246082/228570643-6830ca3b-d6da-4974-b3e9-4d2e108d956f.png)

6.   Compute the loss value as the difference between the distance between the anchor and 
negative image and the distance between the anchor and positive image.

![image](https://user-images.githubusercontent.com/98246082/228570844-5062f6ac-475c-432d-8991-e969ca5b9271.png)

## Now, what should we do in testing?
1.   We have two images (The anchor and the test image)
2.   Extract the encoding of each image.
3.   Calculate the distance between both encodings.
4.   If the distance is less than a threshold then verify that the test image is of the same 
person, otherwise they are different.

## THE LIMITS OF ONE -SHOT LEARNING:
Although very attractive, one-shot learning does have some limitations. Each Siamese neural 
network is just useful for the one task it has been trained on. A neural network tuned for one- 
shot learning for facial recognition can’t be used for some other task, such as telling whether 
two pictures contain the same dog or the same car.
The neural networks are also sensitive to other variations. For instance, the accuracy can 
degrade considerably if the person in one of the images is wearing a hat, scarf, or glasses, and 
the person in the other image is not.

## REAL LIFE SCENARIO THAT SHOW S THE BENEFIT OF USING ONE SHOT LEARNING 
COMPARED TO CLASSIFICATION MODELS:

One of the key problems in many computer vision problems is that you don’t have many 
labeled images to train your neural network. For instance, a classic facial recognition algorithm 
must be trained on many images of the same person to be able to recognize her.
Imagine what this would mean for a facial recognition system used at an international airport. 
You would need several images of every single person who would possibly pass through that 
airport, which could amount to billions of images. Aside from being virtually impossible to 
gather such a dataset, the notion of having a centralized store of people’s faces would be a 
privacy nightmare. And collecting a lot of new data for every new person entering the airport to 
train the model again with the new dataset including that new person, this operation will take a 
very long time leading that the person will probably miss the plane
This is where one-shot learning comes into play. Instead of treating the task as a classification 
problem, one-shot learning turns it into a difference-evaluation problem.
When a deep learning model is adjusted for one-shot learning, it takes two images (e.g., the 
passport image and the image of the person looking at the camera) and returns a value that 
shows the similarity between the two images. If the images contain the same object (or the 
same face), the neural network returns a value that is smaller than a specific threshold (say, 
zero) and if they’re not the same object, it will be higher than the threshold.

![image](https://user-images.githubusercontent.com/98246082/228571766-20709bee-8e8c-420d-8895-9105d7fb71a4.png)

