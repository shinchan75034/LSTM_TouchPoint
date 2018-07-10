# LSTM_TouchPoint

The adoption of LSTM in touchpoint prediction stems from the need to model customer journey or the conversion funnel as a series of touchpoints. For an advertiser or marketer, taking into account the sequence of events that leads to a conversion will add tremendous value to the understanding of conversion funnel, impact of types of touchpoints, and even identify high potential leads for retargeting.


LSTM networks are widely used in solving sequence prediction problems. Most notably in natural language processing (NLP) and neural machine translation (NMT). In particular, sequence-to-sequence (seq2aeq) models have been the workhorse for translation, speech recognition and text summarization. If a collection of individual sequence of events are organized as a corpus, then an LSTM model may be constructed to predict the target outcome (I.e., conversion) or target sequence of events (predicted touchpoint sequence that leads to conversion). 


This example shows how the encoder-decoder paradigm may be implemented with Keras to create an LSTM model that can predict touchpoint sequence given observed sequence of touchpoints.

The training data is stored in Google Cloud Platform (GCP) bucket as a csv. The platform for machine learning model development and scoring is Colab Jupyter notebook offered by Google Research, free for anyone with gmail. 

In general, this example contains the following steps:

1. Create client to access data storage: Get authentication client in Colab to access GCP bucket. 
2. Make data available for Notebook instance: Download the training data from the bucket to /tmp directory of Colab.
3. Read and split data for machine learning: Build, train, and test the encoder-decoder LSTM model using Keras.
4. Save the work: tore models, output data, and any necessary data structure in /tmp directory.
5. Backup: Transfer the aforementioned files to a GCP bucket.

At the test phase in step 3 above, holdout data is used. In general, the model reads the holdout data's input sequence, then:

1. The model predicts a sequence of touchpoints by words. Each word represents a touchpoint. The sequence may or may not include the word 'visit'.
2. If the prediction contains the word 'visit', this sequence is labeled as 1.
3. Compare this prediction to the corresponding truth sequence. If the truth sequence contains 'visit', the truth sequence is also labeled as 1. 
4. Build the confusion matrix between truth and predicted sequences.
5. Calculate and output model KPI.

