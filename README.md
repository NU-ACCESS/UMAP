# Spectral Imaging Data Treatment - UMAP
***

This repository is a companion to the following paper: 

**Application of Uniform Manifold Approximation and Projection (UMAP) in spectral imaging of artworks** <br>
> *Spectrochimica Acta Part A: Molecular and Biomolecular Spectroscopy*, (2021) 252:119547, DOI: 10.1016/j.saa.2021.119547 <br>

Marc Vermeulen (1), 
Kate Smith (2),
Katherine Eremin (2),
Georgina Rayner (2),
and Marc Walton (1)<br>

> 1. Northwestern University / Art Institute of Chicago Center for Scientific Studies in the Arts (NU-ACCESS), 2145 Sheridan Road, Evanston, IL, United States
> 2. Harvard Art Museums, Straus Center for Conservation, 32 Quincy St, Cambridge, MA, United States

**Abstract:** *This study assesses the potential of Uniform Manifold Approximation and Projection (UMAP) as an alternative tool to t-distributed stochastic neighbor embedding (t-SNE) for the reduction and visualization of visible spectral images of works of art. We investigate the influence of UMAP parameters—such as, correlation distance, minimum embedding distance, as well as number of embedding neighbors— on the reduction and visualization of spectral images collected from Poèmes Barbares (1896), a major work by the French artist Paul Gauguin. The use of a cosine distance metric and number of neighbors equal to 10 preserves both the local and global structure of the Gauguin dataset in a reduced two-dimensional embedding space thus yielding simple and clear groupings of the pigments used by the artist. The centroids of these groups were identified by locating the densest regions within the UMAP embedding through a 2D histogram peak finding algorithm.  These centroids were subsequently fit to the dataset by non-negative least square thus forming maps of pigments distributed across the work of art studied. All findings were correlated to macro XRF imaging analyses carried out on the same painting. The described procedure for reduction and visualization of spectral images of a work of art is quick, easy to implement, and the software is opensource thus promising an improved strategy for interrogating reflectance images from complex works of art.*

***

The aim of this repository is to give full access to the Jupyter notebook, associated macros, test dataset, and instructions allowing the reduction and visualization of visible spectral images of works of art as well as pigments identification and their spatial distribution using UMAP, 2D histogram peak finding algorithm and non-negative least square fitting to the original data. <br>

The intention is that the presented research can be fully replicated and implemented by other scientists in their host institutions. <br>

Efforts have been made to the best of the authors' abilities to make the data processing procedures accessible and reusable in support of the growing Open Science movement. <br>

## 1. Overview of contents
#### 1.1. Jupyter notebook (Spectral Imaging Data Treatment - UMAP)
Most of the data treatment is undertaken in the Jupyter notebook. To successfully produce the final text figures, cells within the notebook should be run sequentially. Further pertinent instructions are provided throughout the notebook.

Required versions: Jupyter notebook >=5.5, Python >=3.4.

#### 1.2. Install requirements
All python packages required to run the notebook can be install through the Python 3 or Anaconda navigator command prompt.  

#### 1.3. Test dataset
The Gauguin *Poèmes Barbares* spectral stack used in the associated article can be [downloaded here](https://northwestern.box.com/s/5cjughjrl5eznon2jiojf8x6y0ufkj3b) <br>

#### 1.4. RGB conversion scripts
>>LambdaStack_to_XYZ <br>
>>XYZ_to_RGB <br>

Refer to [NU-ACCESS/Spectral-Microscope-Tools](https://github.com/NU-ACCESS/Spectral-Microscope-Tools) to download the required scripts

>LambdaStack_to_XYZ <br>
>>converts a stack of monochromatic wavelength images into an XYZ tristimulus space. This is accomplished by multiplying each wavelength image by the CIE 1931 Standard Observer matching function, thus producing X, Y, and Z tristimulus value images. The input parameters are the spacing between wavelengths (dependant on the camera used for acquisition, default: 2) as well as the starting and ending wavelengths (default = 393 and 750 nm).

>XYZ_to_RGB <br>
>>converts the XYZ stack into adobe RGB color space assuming a standard D65 Illuminant.

The scripts here were written in Python for use in ImageJ (Fiji) and are based on algorithms detailed in Oakley et. al. "Improved spectral imaging microscopy for cultural heritage through oblique illumination", Heritage Science, 8:1 <br>

To run the scripts, download the latest version of [Fiji](https://fiji.sc) and place the scripts into the plugins folder. Launch Fiji or "refresh menus" if already running. <br>
Both scripts will be available in the Plugins drop-down menu. <br>
The scripts should be ran in the following order: 1) LambdaStack_to_XYZ and 2) XYZ_to_RGB. <br>
The final RGB composite image should be transformed into a RGB color image (Image>Type>RGB color) prior to be saved as a TIF image (File>Save as>Tiff)

## 2. Notebook
Markdown cells provide the instructions and expected output of the subsequent cells of code. When numbers are provided in the markdown cells, they correspond to the position of the cell in the subsequent block of cells of code: "(1) xxxxx" corresponds to the instructions for the first following code cell whereas "(2) xxxx" corresponds to the instruction of the second cell of code. 

## 3. Endmember spectra
Endmember spectra are exported as a .csv file using space as delimiter. They can be imported in Excel for further data processing. 

## 4. Creating the endmember distribution maps from the .txt text image files saved
A stack of endmember distribution maps can be created in ImageJ (Fiji). To create them, follow the following steps:
>1) Open the save txt file as a text image (File>Import>Text Image...)
>2) Select the desired txt file
>3) Transform the txt montage to a stack (Image>Stacks>Tools>Montage to Stack)
>4) In the Stack Maker pop-up window, input: <br>
Columns: the Y value of the original data set dimensions (it will be given when running the *Import the .tif spectral data* cell of the Notebook) <br>
Rows: 1 <br>
Click "OK" <br>
>5) Reslice the stack from the top to create a stack of the distribution maps (Image>Stacks>Reslice).<br>
Select outspacing (pixels): 1 <br>
Start at: Top <br>
Tick "Avoid interpolation (use 1 pixel spacing)<br>
Click OK <br>
>5) The stack of images can be broken into individual images (Image>Stack>Stack to Images)
