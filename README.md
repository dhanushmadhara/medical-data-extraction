********PDF to Text Extraction and Processing with Tesseract OCR********

*Project Overview*

This project automates the extraction of text from PDF files, especially those that are scanned or captured as images.
By leveraging advanced Optical Character Recognition (OCR) technology and image processing techniques, the project converts images into structured text data, 
even in challenging scenarios such as shaded regions in photographs.
The final output is a structured JSON format that provides easy access to specific data fields, such as patient names and details.

Table of Contents
Introduction
Installation
Project Workflow
Step 1: Convert PDF to Image
Step 2: Extract Text from Image
Step 3: Image Processing
Step 4: Convert Text to Structured Data
Usage
Contributing
License
Introduction
Extracting text from PDF files can be challenging, particularly when dealing with scanned documents or images taken with mobile devices. This project addresses these challenges by combining the Tesseract OCR engine with OpenCV-based image processing techniques. The aim is to enhance image quality for more accurate text extraction, and then to organize this text into a structured JSON format for easy analysis and access.

Installation
To set up the project locally, follow these steps:

Clone the repository:

bash
Copy code
git clone https://github.com/yourusername/pdf-to-text-extraction.git
cd pdf-to-text-extraction
Install required Python packages:

bash
Copy code
pip install -r requirements.txt
Install Tesseract-OCR:

Download and install Tesseract-OCR from here.
Ensure that tesseract.exe is accessible in your system's PATH, or set the pytesseract path manually in your script.
Install Poppler:

Download and install Poppler from here.
Add the Poppler bin folder to your system's PATH, or set the poppler_path in your script.
Project Workflow
Step 1: Convert PDF to Image
The first step involves converting the PDF file into an image. This step is crucial for applying image processing techniques and performing OCR.

Library Used: pdf2image

Functionality: Converts each page of a PDF into a high-resolution image.

python
Copy code
from pdf2image import convert_from_path

pages = convert_from_path('path_to_pdf.pdf', poppler_path='path_to_poppler')
Step 2: Extract Text from Image
Once the PDF is converted to an image, the next step is to extract the text using the pytesseract Python module, which utilizes Google's Tesseract OCR engine.

Library Used: pytesseract

Functionality: Extracts text from the processed image.

python
Copy code
import pytesseract

text = pytesseract.image_to_string(image, lang='eng')
Step 3: Image Processing
In cases where the image quality is poor—such as when images are taken from mobile phones with shading or uneven lighting—image processing techniques are applied to enhance the image and improve OCR accuracy.

Library Used: OpenCV

Techniques: Grayscale conversion, thresholding, noise reduction, and more.

python
Copy code
import cv2

# Convert image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply thresholding
processed_image = cv2.threshold(gray_image, 150, 255, cv2.THRESH_BINARY)[1]
Step 4: Convert Text to Structured Data
After extracting the text, the final step is to convert this unstructured text into a structured format, such as JSON. This involves parsing the text to identify key fields, such as patient name, age, and diagnosis.

Library Used: json

Functionality: Organizes extracted text into a JSON object for easy access.
'''
python
Copy code
import json

data = {
    "patient_name": "John Doe",
    "age": 30,
    "diagnosis": "Hypertension"
    # Add more fields as necessary
}

json_data = json.dumps(data, indent=4)
Usage
'''
To run the project, execute the main script. Ensure that the PDF you want to process is located in the appropriate directory, and adjust paths as necessary.

bash
Copy code
python main.py
This will process the PDF, extract text, apply image processing, and output the results as a JSON file.

Contributing
We welcome contributions! If you have ideas to improve the project, feel free to fork the repository, make changes, and submit a pull request. Please ensure your code follows the existing style and includes necessary documentation.
