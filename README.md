# cs6300-project3-solved
**TO GET THIS SOLUTION VISIT:** [CS6300-Project3 Solved](https://mantutor.com/product/cs6300-project3-solved/)


---

**For Custom/Order Solutions:** **Email:** mantutorcodes@gmail.com  

*We deliver quick, professional, and affordable assignment help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;65214&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;3&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (3 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS6300-Project3 Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (3 votes)    </div>
    </div>
<ol>
<li>We collected all the words from the TIMIT dataset sentences and chose the words with a repetition of at least 250. This is done so as to get sufficient features for each word which we want to classify. We get a set of 27 words which have occurance frequency as shown in 1.</li>
<li>We go through each of the word files for all the utterances and collect the frames (which are sampled 16kHz) which correspond to these words.</li>
<li>We then compute the MFCC features for each of these frames and divide the entire thing into 80% for train and remaining for test.</li>
<li>The training input contains the MFCC features of 38 coefficients stacked. Each of these datapoints have features which are calculated over windows of 0.008 seconds with an overlap of 0.004 seconds.</li>
<li>The number windows are made uniform for all the datapoints, and those with lesser than maximum number of windows are padded with zeros.</li>
<li>The output form is number between 1-27 which indicate the corresponding class of the word.</li>
</ol>
<h1>Encoder-Decoder</h1>
<h2>Without attention</h2>
The inputs so obtained upon pre-processing has to be first passed into in Encoder-Decoder (E-D) structure so that the representation and information of MFCC features can be compressed into a context/hidden vector of dimension 256 (for each datapoint). The E-D network is made up of GRU units. The output and input of the E-D network is same. Upon training, the test inputs are also made to pass through the E-D and we obtain the hidden vectors for all of them. These hidden vectors are passed through the ANN and SVM for classification.

The training for this was done with a learning rate of 0.001 and batch size of 20&nbsp; With attention In the case of attention, instead of just taking the context/hidden vector for the final stage, the hidden vectors of previous few stages are also considered. The previous hidden vectors are weighted so that some of them are given more importance than the others. This helps especially in case of translation related tasks where the words in a sentence of different languages are not in the same order. In this particular case, attention does not help significantly since the input and the output are the same. As a result the weightage will not affect significantly.

<h1>Classification</h1>
The accuracy for different models is as shown in the table. The accuracy for Isolated digits model was almost 100% using a single hidden layer and hence no more experiments were done on the same.

<table width="442">
<tbody>
<tr>
<td width="286">Network type</td>
<td width="156">Accuracy for TIMIT</td>
</tr>
<tr>
<td width="286">ANN with 1 hidden layer</td>
<td width="156">59.7%</td>
</tr>
<tr>
<td width="286">ANN with 2 hidden layers</td>
<td width="156">61.9%</td>
</tr>
<tr>
<td width="286">ANN with 1 hidden layer and attention</td>
<td width="156">66.5%</td>
</tr>
<tr>
<td width="286">SVM</td>
<td width="156">57.2%</td>
</tr>
</tbody>
</table>
<h2>ANN</h2>
Upon obtaining the hidden vectors from the E-D network we proceed to classify the utterances using a Deep Neural Network. We experiment for both single and double hidden layers. We also classify the attention based model also. The plots for the loss v/s epochs and the Accuracy v/s epochs are shown in the plots below. If we look at the tSNE plots, we see that initially (input/hidden layer 1) there is no clear boundaries. However for latter 2 layers we see that there are visible boundaries that emerge. These show that at the output layer it is much easier to classify the words. Again we use a learning rate of 0.001 and batch size of 20.

<h2>SVM</h2>
The feature vectors are passed through an SVM Classifier. The variation of regularization v/s SVM accuracy is shown. Linear kernel is used here for classification, since it is the simplest and gives accurate. Non-linear kernel might overfit the data in case of large number of features, so the linear kernel would give the best performance in this scenario. As you can see in Figure 8, the accuracy increases with regularization parameter. This is to be expected since increasing the regularizatoin parameter would allow more leeway for samples to be further from the margin of the classifier. As the restriction is relaxed, the accuracy increases both in the case of training and validation data. The regularization punishes the misclassficati

&nbsp;

&nbsp;
