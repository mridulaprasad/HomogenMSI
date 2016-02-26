homogenPy
=====
homogenPy is a python pipeline to perform homogeneity assessment of MSI dataset(s). 
Our pipeline contains different functions to understand drug distribution by taking advantage from different texture analysis based methods, such as intensity histogram based, gray-level co-occurence matrix (GLCM) based, size-zone matrix (SZM) based and shape factor based. 

The pipeline relies mainly on numpy, scipy, skimage, argparse python modules. There are some specific dependencies as well, discussed below. Pipeline main methods are : 

1) GetIonImage : import and visualization of data from Analyze 7.5 format. This function offers ion intensity map at user defined mass range (.sim),  three different types of segmentation map :
	a) drug mask(default, _drug.msk, drug mask.jpg) b) tic image mask (_tic.msk, _ticmsk.jpg)  c) maximum intensity value mask(_mim.msk, _mimmsk.jpg)
 	 
2) GCLM_features : This function will return 13 Haralick texture features based on gray-level co-occurence matrix for input image. Before features calculation, tissue image will multiple with corresponding mask image to place tissue object on uniform background. Hence results were obtained from tissue object only.

3) GLRLM_features : This function will return 11 features based on gray-level run-length matrix.

4) SZM_features : This function will return 11features calculated on size-zone based matrix. Required : rpy2 python module and r-library radiomics

5) SB_features : This function will calculate shape based features for tissue mask image. It will return: number of small disconnected objects within tissue, their area and perimeter. Required : cv2 python module.

![alt text](https://github.com/pietrofranceschi/homogenPy/blob/master/github.jpeg "Pipeline workflow")

## How to use it 

All scripts run as command line argument. Since output files obtained from GetIonIntensity method will use as an input for other methods, hence it is important to run this script first. After that feature calculation can be done in any order. 

To get help about method, use -h argument. It will give details about input arguments, method function and other optional arguments. 
 
~/MSIdataset$ python GetIonImage.py -h 
usage: GetIonImage.py [-h] [-mz MASSRANGE [MASSRANGE ...]] [-fr MFILTRAD] 
                                       [-tic] [-mim] 

Create an extracted ion image and its corresponding binary mask 

optional arguments: 
  -h, --help                   show this help message and exit 
  -mz MASSRANGE [MASSRANGE ...] 
                                     Desired m/z range 
  -fr MFILTRAD          Radius of the median filter 
  -tic                              TIC based tissue identification 
  -mim                           Maximum Intensity Ion tissue identification 

### Run GetIonImage method example

From above description it is clear all input arguments are optional. Hence, in case of zero argument it will return ion intensity image summed over whole mass scale and drug mask map. While user can define desired mass range as below: 
~/MSIdataset/ python GetIonImage -mz  284.2 284.3

output image from above method: 

![alt text](https://github.com/pietrofranceschi/homogenPy/blob/master/HCT116_AVA.5943_150521.jpg "Drug mask image")
