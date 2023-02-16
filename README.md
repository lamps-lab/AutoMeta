
#### AutoMeta

AutoMeta is a metadata extractor tool for scanned Electronic Theses and Dissertations (ETDs). It has been built to extract seven metadata fields from the cover page of scanned ETDs. These fields are: Title, Author, Advisor, University, Degree, Program, and Year. It utilize learning based model such as CRF model with text-based and visual-based features.

#### Steps

##### 1. Create a virtual environment:
```
We are creating a virtual environment named as "autometa".

conda create -n autometa python=3.7.7 anaconda

* To activate this environment, use:
conda activate autometa

* To deactivate an active environment, use:
conda deactivate

* If you no longer needed the virtual environment:
conda env remove -n autometa
``` 

##### 2. Clone this repository using https:
```
git clone https://github.com/lamps-lab/AutoMeta.git
```
##### 3. Install requirements.txt:
```
python -m pip install -r requirements.txt
```
##### 4. Change the directory to src/  and Create a directory for the PDFs (ETDs):
```
cd AutoMeta/src/
mkdir -p etdrepo/scanned/PDF
```
* Once you create the directory, put all the PDFs inside the PDF directory. Or you can grab the input examples that has been provided in the inputExample directory.
```
cd ..
cp inputExample/pdf/*.pdf ./src/etdrepo/scanned/PDF/
cd src/
```

##### 5. Run the following script but you have to change the file permission:
```
Changing the file permission:
chmod 775 extract_metadata.sh

Running the script:
./extract_metadata.sh
``` 
This script takes PDFs ETD as input and output a CSV file containing their Metadata. The intermediate steps are as below.

(a) Obtain the cover page from the PDF and convert it to TIF format.
(Currently, the first page of an ETD is assumed to be the cover page in all cases)

(b) Use Tesseract OCR to extract the text from the TIF image as well as the hOCR output.

(c) To make the extracted text files the same format as the input to the CRF model (XML format), adding dummy tags.

(d) To use visual features, the script utilize text-align.py file and save the final result (i.e., visual_features_test.csv) to the output directory.

(e) AutoMeta comes with two separate model: crf_model.sav and crf_model_visual.sav

* The output will be a CSV file containing metadata for each ETD.

File Location: CRF_output/metadata.csv (text-based) or CRF_output/metadata_visual.csv (visual-based)

If you are using our tool, please cite the following paper:

```
Plain Text:
M. Hasan Choudhury, H. R. Jayanetti, J. Wu, W. A. Ingram and E. A. Fox, "Automatic Metadata Extraction Incorporating Visual Features from Scanned Electronic Theses and Dissertations," 2021 ACM/IEEE Joint Conference on Digital Libraries (JCDL), 2021, pp. 230-233, doi: 10.1109/JCDL52503.2021.00066.

BibTeX:
@INPROCEEDINGS{9651772,
  author={Hasan Choudhury, Muntabir and Jayanetti, Himarsha R. and Wu, Jian and Ingram, William A. and Fox, Edward A.},
  booktitle={2021 ACM/IEEE Joint Conference on Digital Libraries (JCDL)}, 
  title={Automatic Metadata Extraction Incorporating Visual Features from Scanned Electronic Theses and Dissertations}, 
  year={2021},
  volume={},
  number={},
  pages={230-233},
  doi={10.1109/JCDL52503.2021.00066}}
```
