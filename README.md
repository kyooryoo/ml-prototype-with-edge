# Machine Learning - Prototype on Edge network
Machine Learning uses machine to gain knowledge from data.  
Edge network means the network endpoints which are uaually devices that located at the edge of the Internet.  

## Edge Computing Advantages
Embedded micro controllers that compose edge computing have advantages as follows:
* Latency - Reduced network latency
* Reliability - Not affected by network reliability
* Bandwidth - Reduced need for bandwidth
* Privacy - Less data sent over the Internet
* Cost - Less reliant on costly back-end infrastructure

## Machine Learning Elements
* Model - A mathmetical representation that can make decision or prediction based on input data
* Data - The fuel that powers machine learning and needs to be cleaned and preprocessed before used
* Training - Train a model on a dataset to teach it how to make decision or prediction
* Inference - Use the trained model to make predictions on new unseen data.  

Digital Signal Processing (DSP) is the key component of many machine learning algorithms, as it can extract features from data such as frequency, amplitude, and phase. These features can be used to train models that can recoganize patterns in the data.  
Loss function is used to calculate the gap between the prediction and expected result. Multiple epochs will help to train the model to minimize the error.  


## Machine Learning Workflow
1. Problem Formulation - Define the problem that needs to be solved.
2. Data Collection - Collect and prepare the data that will be used to train the model.
3. Feature Engineering - Select the input data and transform them into features to train the model.
4. Training - Select an appropriate model depending on the goal and input data to perform training.
5. Evaluation and tuning - Evaluating model performance by accuracy, precision, and loss, and tuning it.
6. Deployment - Deply the model to production for making predictions or decisions.

## Ubiquitous Ethics
* Bias - ML models could be biased if the source data is biased, on gender, race, or age.
* Privacy - Privacy could be compromised during the data collection or model deplyment processes.
* Transparency - ML model should be transparent and explainable if it affect livelihood or health.
* Fareness - Model and training data must be engineered from the beginning with fairness in mind.
* Accountability - ML model needs clear lines of responsibility to be accountable for its output.
* Uninteded consequences - innocent intentions may be appropriate for less innocent objectives.

## Reasons for Prototyping
* Exploration - especially for new or unfalmiliar material or technology to understand its potential and challenges.
* Communication - to visually present design and product ideas to team members, stakeholders, and customers.
* Evaluation - for the adage of test early and often, iterative design, save time and resources.

Set prototype expectation early to avaoid the following two scenarios:
* Stakeholders see a high fidelity prototype and believe the final product is almost finished.
* Stakeholders see a low fidelity prototype and believe the team is under performing.

## Prototyping vs. Engineering
Prototype creates inexpensive examples of technology and experience that can be easily changed or adjusted in response to feedback and changing requirements. Engineering on a final product needs to consider lots of factors such as raliability, cost, schedule, and ethical and legal considerations.

## Software and Hardware
Arduino Nano 33 BLE Sense and Arduino IDE are used for this project but Edge Impulse also supports many other devices. Arduino Nano 33 BLE Sense is a popular choice for many developers due to its balance of cost and capabilities. It includes a variety of sensors and is well-supported by the Edge Impulse platform.  

## Define and train an ML Model
Create a project on Edge Impulse portal, choose the appropriate data type to deal with, which is audio this time. The next steps are acuiring the data, training the model, and deploy to the target device.  
The project could be voice recoganizing of RGB (Red/Green/Blue), Shield Up (lock computer), or Emoji (pop up emoji pannel during text input). We will not use existing voicie recoganition libraries but will build it from scratch.  

### Collect Data
You can collect data from supported development board, mobile phone, computer, any device with a sensor, or by uploadig the data. We choose from computer this time, then record mutiple sample files that contain many data samples, such a human voice of RED, YELLO, BLUE, SHIELD UP, or EMOJI.  
Give the sample file a label, such as "shield_up", set sample file length to be 60 seconds, set category to training, then start recording for five times to generate five sample files, each of which contains many samples. Then split sample files to samples, you get about 100 samples from the 5 sample files.  
For creating a model that is robust, you can add some noise to the sample data by recording some noise or downloading sample noise online. Note the noise samples need to be labeled as noise. Split the sample data for training and testing purposes respectively with 80% and 20% for each.  

### Design Impulse
This step generates features from the sample data, trains the model, and use the model to classify new data. Choose the DSP method, which is MFCC in this case, used for extracting the features in the processing block, then choose an initial model, which is classifier in this csae, in the next learning block.  
Check the newly added processing and learning tab under the impulse design section. Generate features under the processing tab, which is MFCC in this ase, and you should see feature and noise are seperated well in the feature explorer window. Then start training model in the learning tab, which is Classifier in this case, with default parameters.

### Test and Deply
Still within the Impulse Design section, use the Model Testing feature on the Edge Impulse portal to test the model with the testing sample data first. You can find statistics about the testing result with the testing samples. Then you can click "Launch in browser" under Deployment tab to test alive with real dynamic human voice input from your computer.  
Choose the developer board type under the Deployment tab, which is Arduino Nano 33 BLE Sense in this case. Download the built library and install it on the Arduino IDE, go to Sketch > Include Library > Add .ZIP Library... the downloaded ZIP file. Then open it under File > Examples > Examples from Custom Libraries, upload it to the board, open Serial Monitor, and test. You can get similiar result as testing on your computer's browser. Each "Shield Up" can get a high precent score over 99%.  

## Extend the prototype
By adding LED and keyboard functionalities to the prototype, it becomes useful to light up a LED or lock the computer when the keyword is recoganized. This makes the prototype getting closer to a product that can lock the computer in urgent for any concerns or privacy or security. Similar use case could be facilitating text input such as emojis, or call your smart phone to response with rings and vibration when you cannot find it at home.  