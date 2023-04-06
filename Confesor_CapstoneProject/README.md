
# <em> **Karenia Brevis </em> HAB Preliminary Modeling on the WFS** 
# Capstone Project - Kristina Confesor, 2023
<p>

### **Background**
<p align="center">
<img src="https://images.marinespecies.org/thumbs/33875_karenia-brevis.jpg?w=700" alt="K.brevis Morphology" style="height: 200px; width:300px;"/>

<p align="center">
Figure 1: <em> K. brevis </em> morphology (Hansen, 2000).
<p> Harmful algal blooms (HABs) have devastating impacts on both marine and human health. 
Monitoring and predicting HAB events is crucial in improving the ability to mitigate their 
effects. One example of a HAB causing species is <em>Karenia brevis</em> (Figure 1), a toxic dinoflagellate 
contributing to red tide bloom events on the West Florida Shelf (WFS). What makes <em>K. brevis</em> of 
interest is the brevotoxins they produce during HAB events (Pierce & Henry, 2008). Shellfish 
harvested and consumed from brevotoxin produced by <em>K. brevis</em> infested waters can result in 
oceanic and human mortalities (Kirkpatrick et al., 2004). Wave actions of <em>K. brevis</em> HABs 
around beach areas has also resulted in documented cases of brevotoxins aerosolized and 
ingested via breathing (Fleming et al., 2005). The lethal toxicity of the brevotoxins produced as 
well as the documented prolific growth results in <em>K. brevis</em> as a designated prominent HAB 
species at the WFS. </p>

### **Purpose**

<p>Creating models to predict <em>K. brevis</em> HAB events is crucial in understanding what causes 
them and where they are likely to occur. This capstone project utilizes supervised machine 
learning (MLP Classifier from the <em>scikitlearn</em> toolkit) to classify <em>K. brevis</em> bloom occurences on the WFS. Cell counts will be used as a 
measure of bloom formation, with the target variable specifically as <em>K. brevis</em> cells counted per 
liter. A bloom for the purposes of this model is defined as any presence of a cell count (cells per liter > 0 ). A model is necessary as <em>K. brevis</em> HAB events have changed over the past decade, and we 
do not have a clear hypothesis as to what causes these blooms to occur yet. </p>

### **Data Access**

<p> For this project, <em>K. brevis</em> cell counts taken over 2015-2023 around the coasts 
of Florida are used as the target variable. This data  is documented by the Florida 
Fish and Wildlife Conservation Commission (FWC) and continuously updated in a .csv file (accessed from the FWC-FWRI HAB Monitoring Database, contact habdata@myfwc.com for details and full data access). This dataset contains Date, Latitude, Longitude, Temperature, Salinity, and cell count data for each sample taken, with some samples having incomplete parameters. Currently, it has 38,312 complete samples that span from 2015 through 2020. However, the 
FWC data currently does not have nutrient data available to the public. 
Instead, other dataset variables such as chlorophyll a, nitrate, and phosphate, will be accessed from the Global 
ocean biogeochemistry hindcast (0.25° × 0.25° spatial resolution) datasets (https://tinyurl.com/yc79ycck). The CMEM
dataset has been taken since 1993 and cover the time and geographic range that the K. brevis 
cell counts were taken up until 2020. This dataset is in the form of a NetCDF file, where variables will  have to be extracted on the basis of the cell count locations. For the model itself, the python  package scikitlearn has the Multilayer Perceptron (MLP) Classifier program that will be used, and <em> K.brevis </em> blooms will be predicted on WFS cruises taken in 2015, 2018, and 2019 not done by the FWRC 
(Confesor et al., 2022). </p>

### **Package Requirements**
<p>

### **Instructions**

### **Impact**
<p>
How HAB-associated species like K. brevis are induced is important for monitoring the onset 
and severity of such blooms. Currently, there is no single hypothesis explaining the occurrences 
of <em>K. brevis</em> HABs along the WFS. My research focuses on one of the hypothesis where nitrogen 
(N2) fixation, as a source of bioavailable N, is a primary contributor to growth and maintenance 
of these blooms (Vargo, 2009). The specific N2-fixation source remains to be elucidated but I 
suspect that the new N input from <em>Trichodesmium</em>, a diazotrophic cyanobacteria, is what 
contributes to <em>K. brevis</em> HAB occurrences. In my dissertation, I hope to be able to create a model 
that classifies/predicts <em>K. brevis</em> blooms via the listed variables above as well as N2-fixation rates from 
<em>Trichodesmium</em> and/or <em>Trichodesmium</em> associated variables. </p>