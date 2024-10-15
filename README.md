# An overview of plant root segmentation using 3D-Unet 

### Overview
Segmenting plant roots from CT (computed tomography) data presents a unique set of challenges due to the intricate and often complex nature of root structures. CT imaging provides detailed three-dimensional information, making it invaluable for studying root architecture non-destructively. However, the segmentation process involves distinguishing roots from surrounding soil and other tissues, which can be particularly challenging due to variations in root density, morphology, and the presence of organic matter. Additionally, the resolution of CT scans may vary, impacting the clarity and accuracy of root segmentation. Overcoming these challenges requires sophisticated image processing techniques, including thresholding, edge detection, and machine learning algorithms tailored to handle the specific characteristics of root structures in CT data. Effective segmentation is crucial for advancing research in plant biology, agronomy, and environmental science, enabling deeper insights into root growth dynamics, nutrient uptake, and interactions with the soil environment.
<br>
<br>
Here we show that deep learning, focusing on 3D-Unet, is an excellent tool to segment plant roots in growing media. We show this firstly for data we have collected, we then show that in some cases our deep learning model will segment data from different experiments. Lastly, we show how the model can be retrained to segment new data, avoiding the need to “start from scratch”. 
<br>

### Creating Training Data and Training a model
The goal of training data is to train the model what our object(s) of interest are. Realistically a whole CT scan cannot be used to train as such we need to break the 3D volume down into “patches”. This step involves hand labelling the raw data slice by slice (often in different orthogonal views to capture roots in different directions, Figure 1 a,b) to create a 3D mask 

<p align="center">
<img  src="content/validation eg.png" > 
</p>

###### Figure 1: The deep learning workflow. Example 3D training data (a) and a corresponding 2D slice with the root mask overlayed (b). An example of comparing the testing data (manually segmented data that the model has never seen (c)) to the model output (d). The difference between (c) and (d) are captured in the quality control metrics (for this image: precision: 0.97, recall: 0.80 and f1:0.87). The model is then used to segment 3D images stacks (f).      

Here we use the PyTorch 3D-Unet, in particualr, the package described in Wolny et al., (2022) (https://github.com/wolny/pytorch-3dunet). For nuanced details about tweaking models (e.g. loss functions, evaluation functions etc we recommend the Wolny et al., 2022 paper but note that the PyTorch documentation is the best place to start). Essentially the package created by Wolny et al., 2022 is an excellent interface to leverage the deep learning tools within PyTorch. In essence, to successfully use AI as microscopists (or anyone just incorporating imaging into their experiments) the bulk of the time should be spent on creating high quality training data. Realistically, most researchers are not invested in enough to explore dozens of model iterations but rather want an “out the box” tool for their image analysis problem. 
