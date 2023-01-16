<p align="center" width="100%">
  <img src="/images/coverdrillhole.png" style="height:400px" />
</p>
<p align = "center">
  <em>Designed by Freepik</em>
</p>

## My Uni Thesis Experience: Automatic Extraction of Mineral Exploration Results using NLP

As part of my mechatronics engineering degree, I was required to complete a yearlong thesis project. This involved picking a supervisor and a thesis topic who I would work with over the year to complete. The assessment for the thesis involved a proposal document, a seminar presentation, and a research paper to hand in at the end. The aim of requiring engineering students to do a yearlong thesis is to:

- allow a much more detailed and thorough learning experience that could not be achieved in a single semester

- Apply and demonstrate a more advanced level of knowledge that students otherwise would not get to show

- Develop skills for working in academic and professional environment

Machine learning is an area I wanted to get more experience, the thesis topic I chose was on the automatic extraction of mineral exploration results using natural language processing (NLP), specifically the effectiveness of different neural models. This thesis topic led to the development a unique database to train models on extracting mineral exploration results for this thesis and for future models. In addition, I co-authored as short paper with my supervisor Ash Rahimi, about our research which was accepted at the COLING computational linguistics conference in 2022 where I presented our work. In this blog I'll discuss what my thesis topic is and what I achieved.

### The Topic

The focus of this thesis was on assessing if NLP could be able to automatically extract drillhole results from mining company reports. For context, it’s relevant to understand what are drillhole results.

#### What are drilllhole results?

Drillhole results are sentences that show the mineral composition of the ground when doing mineral exploration. These results are typically found in mining company reports such as annual reports and press releases, and publicly listed companies are required to report this data to the public. Here is an example of a report from a mining company; in the middle, there a list of drillhole sentences e.g. ***15 meters @ 2.35% Li2O and 100ppm Ta2O5 from 142m (PLS1315)***. This is a drillhole sentence, and this is what we want to extract from the report.

<p align="center" width="100%">
  <img src="/images/drillholeresults.png" style="height:400px" />
</p>
<p align = "center">
  <em>Example drillhole result from Pilbarra Mineral ASX Announcement</em>
</p>



Drillhole results are helpful for investors, industry professionals, and mining companies assess the performance of a mineral exploration project. Mining minerals is ever more important with the move to renewable energy technologies such as electric cars. A world bank report estimates that mining key minerals must increase by 400% to meet the target of reducing global warming by 2050, particularly in countries with existing mineral mining like Australia. Access to up-to-date mineral exploration results is vital for growth in the exploration industry.

<p align="center" width="100%">
  <img src="/images/worldbank.png" style="height:400px" />
</p>
<p align = "center">
  <em>World Bank report for key minerals insert citation</em>
</p>

With many states in Australia not mandating reporting of exploration results, efforts by government and private industry to develop an up to date drillhole result databases have all required the data to be manually extracted from the reports. However, the vast majority of these mining companies do promptly provide the results in reports to the public in the form of press releases and annual reports.

<p align="center" width="100%">
  <img src="/images/drillholesites.png" style="height:400px" />
</p>
<p align = "center">
  <em>Map of drillhole sites in Western Australia</em>
</p>

#### The problem

In my thesis, I assessed whether these drillhole results can be automatically extracted from reports using NLP, specifically by performing sequence labelling on these drillhole sentences. As far as I know, minimal prior research has been done on using neural network models to extract mineral exploration data, particularly in an Australian context. This led to the development of a novel corpus for sequence labelling drillhole data in mining company reports and was a significant part of our work. In addition, the challenges I faced were that drillhole sentences do not have a consistent format.



### Project Difficulties

#### Irregular Sentence Format

Here is an example of just some of the various drillhole sentence formats in a single report. Significant differences also occurred between different companies. Drillhole sentences also are very similar to other geological sentences. The primary identifier of a drillhole sentence is the Hole ID code, which was implemented to identify drillhole sentences from different sentence types.

<p align="center" width="100%">
  <img src="/images/sentencestructure.png" style="height:400px" />
</p>
<p align = "center">
  <em>Example of the various drillhole sentence structures</em>
</p>

This variation in sentence format in addition to other challenges such as PDF text extraction and sentence segmentation confirmed that a neural NLP approach was required to extract the drillhole results by performing sequence labelling. Initially, the use of regular expressions may have been a valid solution if the drillhole sentence formats were more similar to each other and could form a valid benchmark test to compare against the neural NLP models. Instead, the neural NLP models were compared against each other.

#### Novel Corpus

For the novel corpus, I sampled mining companies on the Australian stock exchange by size and recent listings and collated their reports. The focus was on drillhole sentences in a free text, non-tabular form and in the end, the result was 23 companies across 50 reports.

For the Annotation, the IOB tagging format was used to tag each part of the drillhole sentence. The corpus contains over 660K words and 23K sentences. Three datasets were created with a train/dev/test split. One was random, and the other two had materials and companies in the dev/test sets not found in the training set to assess how well the models would perform on material and companies not in the existing dataset.



<p align="center" width="100%">
  <img src="/images/corpus.png" style="height:400px" />
</p>
<p align = "center">
  <em>Corpus Statistics</em>
</p>

### The Solution

Two neural network models were assessed as benchmarks: a bi-directional LSTM model with CRF layer and BERT. These models were chosen as they are suited for sequence labelling on structured sentences. Both models performed well, with the best average F<sub>1</sub> score by BERT at 87%, and the LSTM model achieved 78%. In addition, the scores were consistent across all three datasets: random, material and company datasets. This was a surprising as this shows that the models can generalise for unseen materials and companies. However, overall, BERT was substantially better, where the scores were consistent across all tags and datasets and demonstrated robustness against variations in sentence structure.

<p align="center" width="100%">
  <img src="/images/results.png" style="height:400px" />
</p>
<p align = "center">
  <em>Benchmark F<sub>1</sub> Results</em>
</p>

It was demonstrated that neural network models are a viable solution for the automatic extraction of drillhole data from mining company reports. In addition, the results showed that BERT could perform better than LSTM models for sequence labelling structured sentences in unstructured text.

### Summary

The yearlong thesis was one of the highlights of my engineering degree. I'm grateful for the opportunity to have gotten to publish a short paper on our work and be able to have experience in some academic research, particularly in the machine learning domain. The short paper I co-authored is available [here](https://aclanthology.org/2022.wnut-1.16/) the ACL anthology and links to the novel corpus are available [here](https://github.com/adamdimeski/Automatic-Extraction-of-Mining-Company-Drillhole-Results).
