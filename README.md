MangaTextDetection
==================

Forked from an ancient repo. Updated with new Tesseract models and Python interface. Compatibility updated to Python 3.7.
Experiments in text localization and detection in raw manga scans. Mostly using OpenCV, PIL and python API.


Overview
--------
This repository holds some experiments ~I did in summer 2013 during a sudden interest~ I did in summer 2020 in text detection in images. It uses some standard image processing techniques (run length smoothing, connected component analysis) and some experimental stuff. Overall, the result is okay. Will add more codes to search for masks in the near future.

State
-----
I haven't bothered to form this into a python library. It's just a series of scripts each trying out various things, such as:
* Isolating bounding boxes for text areas on a raw manga page.
* Identifying ares of furigana text (pronunciation guide, which can screw up OCR) in text bounding boxes.
* Preparing identified text areas for basic OCR.


Text Location Example
---------------------
Here's an example run of a page from Weekly Young Magazine #31 2013. The input image is as follows (jpg).
![Input image](https://github.com/johnoneil/MangaTextDetection/blob/master/test/194.jpg?raw=true)

An initial estimate of text locations can be found by the 'LocateText.py' script:

```
 ../LocateText.py '週刊ヤングマガジン31号194.jpg' -o 194_text_locations.png
```

With the results as follows (estimated text marked with red boxes):

![locate text output](https://github.com/johnoneil/MangaTextDetection/blob/master/test/194_text_locations_thumb.png?raw=true)

Note that in the output above you see several of the implementation deficiencies. For example, there are several small false positives scattered around, and some major false positives on the girl's sleeve and eyes in panels 2 and 3.
Also note that many large areas of text were not detected (false negatives). Despite how pleased I was with the results (and I was more pleased than you could possibly believe) significant improvements are needed.

Text Segmentation Example
-------------------------
To more easily separate text from background you can also segment the image, with text areas and non text being separated into different (RGB) color channels. This easily allows you to remove estimated text from image entirely or vice-versa.
Use the command:
```
./segmentation.py '週刊ヤングマガジン31号194.jpg' -o 194_segmentation.png
```
The results follow:

![Input image](https://github.com/johnoneil/MangaTextDetection/blob/master/test/194_segmentation_thumb.png?raw=true)


Dependencies
-----------------------
### Python 3.7

https://www.python.org/

Install as per OS instructions. Should work with all Python 3.


### Scipy

http://www.scipy.org/index.html

```
pip install scipy
```

### Matplotlib (contains PyLab)

http://matplotlib.org/

```
pip install matplotlib
```

### Pillow

http://pillow.readthedocs.org/en/latest/

```
pip install Pillow
```

### OpenCV

http://opencv.org/

```
Install as per OS instructions, this should also include the python bindings.
```

### Tesserocr

https://github.com/sirfz/tesserocr/

```
pip install tesserocr
```

### Pytesseract

https://github.com/sirfz/tesserocr/

Install as per OS instructions, then use pip to install the python bindings.
Don't forget to include your target language's trained data sets.

```
pip install pytesseract
```
