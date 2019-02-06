# Super_Hero_Clustering
## Introduction
This project is to distribute comic super heroes into different clusters based on their abilities using machine learning. It can be divided into two parts.  
* Part 1: Using cosine similarity to find out the most similar hero for the input one based on the abilities.  
* Part 2: Clustering heroes into different groups by KMeans method.  

## Data  
**Data Source:**  
https://www.kaggle.com/claudiodavi/superhero-set#super_hero_powers.csv  
This data was scraped from <a href='https://www.superherodb.com/'>SuperHeroDb</a> and was collected in June/2017 from superherodb which  had not been updated since, so it may not be up to date.  

Data example:  
<img src='Data_example.png' alt='screenshot for data example' title='data example' width=600px height=400px>  

Data summary:  
668 x 168  (668 heroes and 168 types of abilities)  

**Although the columns are already in one-hot style, the values are 'True/False' in String, which need to be converted into 1 or 0 for the convenience of future analysis.**  

## Methodology  
**I.  Data preprocessing**  





1.  Load CSV file with PIL in batch by glob.  
2.  Convert all the images to 'RGB' mode and resize them to 128 x 128 pixels (Using larger image would cause very complex computation, and the significance change is not worth of the computation cost).  
3.  Standardize the pixel value and convert the image data to numpy vectors, which are the X sets for the model inputs (including training, dev and testing). Create the related Y sets (vector of 0 for normal sets, 1 for pneumonia sets) based on the X set's shape.  
4.  Make the complete data sets by concatenating both normal and penumonia data sets for both X and Y.  
5.  Shuffle the data sets in random.  

**II. Building the model in Keras**  
The general model architecture is like model VGG-16 which keeps increasing filter units in the exponential of 2 and decreasing the image size by half with max pooling during every hidden layer. After 4 hidden layers of computation, the image data is converted from (128, 128, 3) to (5, 5, 256). The flatten vector is eventually computed by a sigmoid function to get the classification results (Fig.1).  

**_Fig.1_** <img src='model.png' title='cnn model' alt='a cnn work flow'>  
**Hyperparameters (part of)**  
  * optimizer: Adam, learning rate: 0.001, beta_1: 0.9, beta_2: 0.999  
  * epochs: 20  
  * mini batch size: 16  

## Results  
By far, upon the current hyperparameters the best results are:  
  * Accurancy of training set: 1.0;  
  * Accurancy of dev set: 1.0;  
  * Accurancy of testing set: 0.83.  

The final result can be different by more iterations of training, hyperparameters tuning or other model architectures.    

## Discussion  
  1. The image size can be important for the model performance. Since the difference is quite subtle for images between normal and pneumonia, larger image can be more beneficial for more details. However, the computation cost is also exponentially increased when dealing with large image. Therefore, I took the size of 128 x 128 here as the balance between performance and efficiency.
  2. The sample number of dev set is quite small which is only 16. More dev samples may be good for the model performance. Because the samples were distributed by the author before shipped, no change was conducted here.  
  3. Other models as LeNet and AlexNet were also tried, but the performace was not significantly changed.  
  4. The final best accuracy of the testing set is 0.83, which is not very good and can't be reliable for actual usage. Thus, more following optimization is required definitely.  

## Conclusion  
Using deep learning technique to assist practical clinic method is very promising and significantly useful. This model to analyze X ray images for pneumonia diagnose is a good try. However, more work needs to be done before it is really practable. 
