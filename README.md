# Moreno-OCR-files
OCR files of 374 Spanish chapbooks published by the same printer (José María Moreno) during the 19th century. These files have been produced by the OCR tool [Transkribus](https://readcoop.eu/transkribus/?sc=Transkribus). The workflow followed to train a model and transcribe the chapbooks is described bellow.

## Description of the directories
Each sub-directory of "OCR-files" includes the PAGE-XML files (One per page) produced by the OCR, and a masterfile that gathers all these files to transform them into a single XML-TEI file via XSLT. The results of this transformation and the XSLT stylesheet can be found in the directory [Moreno-TEI-files](https://github.com/DesenrollandoElCordel/Moreno-TEI-files).

## Transcription workflow
### 1. Transcription of the train set (Ground Truth)
The train set was first OCRed with ABBYY FineReader and then manually corrected with the following transcription rules:
* Accents, spelling, punctuation, spaces and capital letters were preserved;
* Line breaks and paragraphs were followed.

The transcriptions obtained after the manual corrections can be found in [Moreno_GroundTruth](https://github.com/DesenrollandoElCordel/Moreno-OCR-files/tree/main/Moreno-GroundTruth).

### 2. Training of a model with Transkribus
The train set was composed of 121 pages (8109 lines). 48 pages (2283 lines) was dedicated to the validation set.
Evaluation and accuracy of the model on the validation set (Values calculated by Transkribus):
* Word Error Rate: 2,95%
* Character Error Rate: 1,29%
* Word Accuracy: 94,99%
* Character Accuracy: 98,21%

### 3. Export and encoding
The transcriptions obtained with our model have been exported in PAGE-XML (one file per page). For each document, we created a masterfile that gathers all the pages to make a single XML-TEI file. The masterfiles have been automatically produced with the script [creation_masterfiles.py](https://github.com/DesenrollandoElCordel/code-python/blob/main/creation_masterfiles.py).
Then we applied the XSLT stylesheet [Page_TEI.xsl](https://github.com/DesenrollandoElCordel/Moreno-TEI-files/blob/main/xslt/Page_TEI.xsl) to the masterfiles to produce [XML-TEI files](https://github.com/DesenrollandoElCordel/Moreno-TEI-files) with a common structure, which is manually enriched with new XML-TEI tags afterwards.
