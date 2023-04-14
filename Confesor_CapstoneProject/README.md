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
liter. A bloom for the purposes of this model is defined as any presence of a cell count (cells per liter > 100). A model is necessary as <em>K. brevis</em> HAB events have changed over the past decade, and we 
do not have a clear hypothesis as to what causes these blooms to occur yet. </p>

### **Data Access**

<p> For this project, <em>K. brevis</em> cell counts taken over 2015-2023 around the coasts 
of Florida are used as the target variable. This data  is documented by the Florida 
Fish and Wildlife Conservation Commission (FWC) and continuously updated in a .csv file (accessed from the FWC-FWRI HAB Monitoring Database, contact habdata@myfwc.com for details and full data access). This dataset contains Date, Latitude, Longitude, Temperature, Salinity, and cell count data for each sample taken, with some samples having incomplete parameters. Currently, it has over 60,000 samples that span from 2015 through 2020 with some salinity and temperature data missing. Also, the FWC data currently does not have nutrient data available to the public. Instead, other dataset variables such as chlorophyll a, nitrate, silica, and oxygen, will be accessed from the GLORYS12V1 (0.12° × 0.12° spatial resolution)) datset as well ass the Global ocean biogeochemistry hindcast (0.25° × 0.25° spatial resolution) dataset (https://tinyurl.com/uvcxw8xt and https://tinyurl.com/yc79ycck respectively). The CMEM dataset has been taken since 1993 and cover the time and geographic range that the K. brevis cell counts were taken up until 2020. This dataset is in the form of a NetCDF file, where variables will  have to be extracted on the basis of the cell count locations. For the model itself, the python  package scikitlearn has the Multilayer Perceptron (MLP) Classifier program that will be used, and <em> K.brevis </em> blooms will be predicted on other datasets (in this case randomly generated). </p>

### **Package Requirements**
<p> This code uses Python Version: 3.11.2.
<p> The ConfesorCapstoneEnv.yaml environment contains all the necessary packages, be sure to make this the active kernel.
<p> List of specific packages: pandas,numpy,seaborn,matplotlib,cartopy,gsw,scikit-image,scikit-learn,scikit-learn-intelex,scipy,cmocean,netcdf4,xarray
<p> On Anaconda Powershell Prompt if you don't have the above already):

conda install pandas,numpy,seaborn,matplotlib,cartopy,scikit-image,scikit-learn,scikit-learn-intelex,scipy,xarray
<p>conda install -c conda-forge gsw
<p>conda install -c conda-forge netcdf4
<p>conda install -c conda-forge cmocean
<p>conda install -c conda-forge gsw


### **Instructions**
Full details can be found below. Make sure all files are in the same directory!
### <em> Downloading Data</em>
.nc files have been provided in the GitHub Repository
Instructions are included below for download directly from CMEMs.

**In Anaconda Powershell Prompt: Need to install the motuclient in order to download CMEMS data (Need an account first!) https://data.marine.copernicus.eu/products**
<p>python -m pip install motuclient==1.8.4 --no-cache-dir  </p>

**Downloading Salinity & Temperature data (~0.5 m depth in study area, from 2015-2020). Need to input your username, password, and desired directory to put .nc file**

<p> python -m motuclient --motu https://my.cmems-du.eu/motu-web/Motu --service-id GLOBAL_MULTIYEAR_PHY_001_030-TDS --product-id cmems_mod_glo_phy_my_0.083_P1D-m --longitude-min -86.546279567723 --longitude-max -79.31701110062916 --latitude-min 24.073184112638952 --latitude-max 30.579525733023395 --date-min "2015-01-01 00:00:00" --date-max "2020-12-31 23:59:59" --depth-min 0.49402499198913574 --depth-max 0.49402499198913574 --variable so --variable thetao --out-dir Input/Directory/here  --out-name NutrientsTotal.nc --user InsertUsernameHere --pwd “InputPasswordHere" </p>

**Downloading Nutrient data (0.5 m depth in study area, from 2015-2020). Need to input your username, password, and desired directory to put .nc file**

<p> python -m motuclient --motu https://my.cmems-du.eu/motu-web/Motu --service-id GLOBAL_MULTIYEAR_BGC_001_029-TDS --product-id cmems_mod_glo_bgc_my_0.25_P1D-m --longitude-min -86.546279567723 --longitude-max -79.31701110062916 --latitude-min 24.073184112638952 --latitude-max 30.579525733023395 --date-min "2015-01-01 00:00:00" --date-max "2020-12-31 23:59:59" --depth-min 0.51 --depth-max 0.51 --variable chl --variable no3 --variable o2 --variable po4 --variable si --out-dir Input/Directory/here  --out-name NutrientsTotal.nc --user InsertUsernameHere --pwd “InputPasswordHere" </p>

**The nc files I downloaded are included in this repository (SalTempTotal.nc & NutrientsTotal.nc)**

**FWC Data**
<p> Contact habdata@myfwc.com for complete access to dataset (Not allowed to share publicly!). If you have data of your own make sure it's in a .csv file.

### <em> Jupyter Notebook</em>
<p> Run ConfesorCapstone.ipynb on JupyterLab or JupyterNotebook while having all the necessary files in the same directory.

### **Impact**
<p>
How HAB-associated species like K. brevis are induced is important for monitoring the onset and severity of such blooms. Currently, there is no single hypothesis explaining the occurrences of <em>K. brevis</em> HABs along the WFS. My research focuses on one of the hypothesis where nitrogen (N2) fixation, as a source of bioavailable N, is a primary contributor to growth and maintenance of these blooms (Vargo, 2009). The specific N2-fixation source remains to be elucidated but I suspect that the new N input from <em>Trichodesmium</em>, a diazotrophic cyanobacteria, is what contributes to <em>K. brevis</em> HAB occurrences. In my dissertation, I hope to be able to create a model that classifies/predicts <em>K. brevis</em> blooms via the listed variables above as well as N2-fixation rates from <em>Trichodesmium</em> and/or <em>Trichodesmium</em> associated variables. </p>

### **References**
<p> Fleming, E., Backer, C., & Baden, G. (2005). Overview of Aerosolized Florida Red Tide Toxins: Exposures and Effects. Environmental Health Perspectives, 113(5), 618-620. https://doi.org/10.1289/ehp.7501 

<p> Hansen, N., Larsen, J., & Moestrup, Ø. (2000). Phylogeny of some of the major genera of dinoflagellates based on ultrastructure and partial LSU rDNA sequence data, including the erection of three new genera of unarmoured dinoflagellates. Phycologia, 39, 302-317. 

<p> Kirkpatrick, B., Fleming, L. E., Squicciarini, D., Backer, L. C., Clark, R., Abraham, W., Benson, J., Cheng, Y. S., Johnson, D., Pierce, R., Zaias, J., Bossart, G. D., & Baden, D. G. (2004). Literature review of Florida red tide: implications for human health effects. Harmful Algae, 3(2), 99-115. https://doi.org/https://doi.org/10.1016/j.hal.2003.08.005 

<p>Pierce, R. H., & Henry, M. S. (2008). Harmful algal toxins of the Florida red tide (Karenia brevis): natural chemical stressors in South Florida coastal ecosystems. Ecotoxicology, 17(7), 623-631. https://doi.org/10.1007/s10646-008-0241-x 

<p> Vargo, G. A. (2009). A brief summary of the physiology and ecology of Karenia brevis Davis (G. Hansen and Moestrup comb. nov.) red tides on the West Florida Shelf and of hypotheses posed for their initiation, growth, maintenance, and termination. Harmful Algae, 8(4), 573-584. https://doi.org/https://doi.org/10.1016/j.hal.2008.11.002 
