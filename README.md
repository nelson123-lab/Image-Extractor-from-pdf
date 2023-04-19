# Image-Extractor-from-pdf
To extract information images with a border from a pdf.

This a script that I did when the lecture notes provided by our professor was a pdf with each pages a combination of 4 slides. It was difficult to read the pdf as I had to zoom in each slide each time. This is still in construction stage.

Part 1
Purpose is extract all the 4 slides in a page into 4 images and likewise for all pages and finally making a folder name same as the pdf name and moving all the images into the folder. (The order of the slides should be maintained for continuity.) 

Part 2
In the second part the the script should loop through the different folder containing slides of the particular folder and convert each of them into a ppt with the same folder name.

```python

import PyPDF2
import io
from PIL import Image

# Open the PDF file in binary mode
with open('example.pdf', 'rb') as file:
    # Read the contents of the file
    pdf_reader = PyPDF2.PdfFileReader(file)
    # Loop through each page of the PDF
    for page_num in range(pdf_reader.getNumPages()):
        # Get the current page
        page = pdf_reader.getPage(page_num)
        # Get a list of all the objects on the page
        objects = page['/Resources']['/XObject'].getObject()
        # Loop through each object
        for obj in objects:
            # Check if the object is an image
            if objects[obj]['/Subtype'] == '/Image':
                # Get the image data
                stream = io.BytesIO(objects[obj]._data)
                # Use Pillow to open and save the image
                image = Image.open(stream)
                image.save(obj[1:] + '.jpg', 'JPEG')
```
In this code, we first open the PDF file in binary mode using open(). Then, we use the PyPDF2 library to read the contents of the file and loop through each page. For each page, we get a list of all the objects on the page and loop through each object. We check if the object is an image by checking its /Subtype attribute. If it is an image, we get the image data using io.BytesIO() and then use the Pillow library (PIL) to open and save the image as a .jpg file.

Note that this code assumes that all the images in the PDF file are in JPEG format. If there are images in other formats (such as PNG), you'll need to modify the code accordingly.

Pull requests are welcome....
