# RECONNAISSANCE ET EXTRACTION DE DOCUMENTS 


Depuis plusieurs mois, les services de délivrance des cartes nationales d’identité et des passeports
camerounais connaissent de fortes perturbations. Les autorités évoquent des dysfonctionnements
techniques et un changement d’opérateur, mais peinent à calmer l’agacement des citoyens.
L’événement était particulièrement attendu. Le 8 janvier, après une semaine de protestations de citoyens
en colère dans les médias comme sur les réseaux sociaux, les responsables de la police camerounaise sont
finalement sortis de leur réserve pour désamorcer une crise montante : celle née de la raréfaction des
titres d’identité dans les commissariats. Initiée par des anonymes sur la Toile, cette campagne avait
conduit à une mobilisation autour du slogan « Je veux ma CNI [carte nationale d’identité] ».


Retards et pénuries
Dans une conférence de presse aux allures de communication de crise, Dominique Baya, le secrétaire
général de la Délégation générale à la sûreté nationale (DGSN), s’est employé à expliciter les raisons
des retards et pénuries observés dans la délivrance des cartes nationales d’identité et des passeports.
Droit dans ses bottes, l’ancien commissaire divisionnaire a ainsi exposé une série de raisons, en insistant
sur l’incivisme des usagers. Il a notamment dénoncé les détenteurs de multiples identités, qui
refuseraient « de faire valider leur identité authentique, car ils ont développé d’autres avantages avec
celles-là ». Selon la police, plus de 3 millions de personnes seraient dans ce cas.
PLUS DE 245 000 CARTES SONT EN ATTENTE DE RETRAIT
Dominique Baya est également revenu sur ce qui constituait la ligne de défense des autorités depuis le
déclenchement de cette polémique : « le non-retrait desdits documents ».
Interpellée sur son compte Facebook officiel par de nombreux usagers, la police camerounaise avait en
effet multiplié les publications montrant des stocks de CNI attendant preneurs dans les commissariats. «
Plus de 245 000 cartes déjà produites sont en attente de retrait par leur demandeur », a affirmé
Dominique Baya, citant le seul centre de production de Garoua (région du Nord).
À LIRE
Crise anglophone au Cameroun : le jour où le bruit et la fureur se sont abattus sur KumbaMais dans ce pays confronté à de multiples crises sécuritaires et où les contrôles se sont multipliés, ces
explications ont du mal à passer. « Il est difficile de s’imaginer que des gens refusent volontairement de
retirer leurs documents d’identité alors que certaines personnes se retrouvent en détention pour non-
présentation de leur titre, s’étonne Amadou, un habitant de Yaoundé confronté au problème. Cela fait
vingt-huit mois que j’ai fait refaire la mienne. Mais, à chaque fois que je vais au commissariat, on me dit
qu’elle n’est pas encore disponible. »
Racket organisé par les gendarmes
Une situation qui favorise le racket organisé par les gendarmes aux barrages de sécurité et provoque
l’apparition de réseaux parallèles de production de titres d’identité au noir, avec des coûts parfois quatre
voire cinq fois plus élevés que d’ordinaire.
Les autorités ont procédé à la mi-2016 à une refonte totale du système d’identification et de fabrication
des nouveaux titres dans le but de renforcer la sécurité sur le territoire, en luttant en particulier contre
l’usurpation d’identité et la fraude documentaire.
Seulement, l’opération – qui avait bien démarré avec la mise en circulation de cartes biométriques
comportant des photos couleur au laser – a vite affiché quelques défaillances.

Etant élève ingénieur on vous demande d’implémenter un algorithme capable enfin d’aider la police
camerounaise dans le déploiement d’un tel système :
▪
▪
D’extraire les informations sur l’image CNI qui sera envoyé sur la plateforme : Numéro de la
CNI, date et lieu de naissance, date délivrance, date d’expiration et autorité signataire.
Après extraction il faut un algorithme capable de vérifier la conformité avec les donnes des
utilisateurs recueillis.

**1)From scratch with NIST36 dataset**   

Training Models

Since our input images are 32 × 32 images, unrolled into one 1024 dimensional vector, that gets multiplied by W(1), each row of W(1) can be seen as a weight image. Reshaping each row into a 32×32 image can give us an idea of what types of images each unit in the hidden layer has a high response to.

The training data in nist36 train.mat contains samples for each of the 26 upper-case letters of the alphabet and the 10 digits. This is the set you should use for training your network. The crossvalidation set in nist36 valid.mat contains samples from each class, and should be used in the training loop to see how the network is performing on data that it is not training
on. This will help to spot over fitting. Finally, the test data in nist36 test.mat contains testing data, and should be used for the final evaluation on your best model to see how well  it will generalize to new unseen data.

We train a network from scratch using a single hidden layer with 64 hidden units, and train for at least 30 epochs. We modify the script to plot generate two plots:
one showing the accuracy on both the training and validation set over the epochs, and the other showing the cross-entropy loss averaged over the data. The x-axis should represent the epoch number, while the y-axis represents the accuracy or loss. We see an accuracy on the validation set of 75%.

Visualizing the confusion matrix for your best model.     

![5](/results/5.png)

We can observe that the top misclassified classes are:     
O confused with 0, D  
8 confused with B  
I confused with 1     



Now that we have a network that can recognize handwritten letters with reasonable accuracy, we can now use it to parse text in an image. Given an image with some text on it, our goal is to have a function that returns the actual text in the image. 
However, since your neural network expects a a binary image with a single character, we will need to process the input image to extract each character. 

Steps:

1. Process the image (blur, threshold, opening morphology, etc. (perhaps in that order))
to classify all pixels as being part of a character or background.  
2. Find connected groups of character pixels (see skimage.measure.label). Place a bounding box around each connected component.   
3. Group the letters based on which line of the text they are a part of, and sort each group so that the letters are in the order they appear on the page.   
4. Take each bounding box one at a time and resize it to 32 × 32, classify it with LeNet5 network, and show the characters in order (inserting spaces when it makes sense).    

![1](/results/1.png)
![2](/results/2.png)
![3](/results/3.png)
![4](/results/4.png)


**1)From EMNIST dataset with PyTorch using a convolutional net (LeNet5) **   

![5](/results/6.png)

We can see that this is much better detection as compared to previous implementation.
Just some minor confusions are there for 0 and O, S and 5, k and I   
Addition of constitutional layers helps in extracting features. This architecture learns much more data.

The graphs for training are shown below:
![6](/results/7.png)

