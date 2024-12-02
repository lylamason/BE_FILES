# Read Me

## PDF OCR Information Extraction Script with LLM Integration

This Python script processes PDF files in a specified directory, performs Optical Character Recognition (OCR) on the first page of each PDF, utilizes a Large Language Model (LLM) to extract specific information from the OCR text, and compiles the extracted data into a Pandas DataFrame for easy analysis.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Script Overview](#script-overview)
- [Configuration](#configuration)
- [Output](#output)
- [Troubleshooting](#troubleshooting)
- [License](#license)

## Prerequisites

Before running the script, ensure you have the following installed:

### Python 3.x

### Tesseract OCR Engine

- **Windows**: Download the installer from UB Mannheim's GitHub.
- **macOS**: Install via Homebrew: `brew install tesseract`
- **Linux**: Install using apt: `sudo apt-get install tesseract-ocr`

### Poppler (for PDF conversion)

- **Windows**: Download from Poppler for Windows.
- **macOS**: Install via Homebrew: `brew install poppler`
- **Linux**: Install using apt: `sudo apt-get install poppler-utils`

### OpenAI Account and API Key

Sign up for an OpenAI account and obtain an API key from the OpenAI API.

## Installation

Install the required Python packages using pip:

- `pip install pytesseract==0.3.10`
- `pip install pdf2image==1.16.3`
- `pip install pandas==2.0.3`
- `pip install langdetect==1.0.9`
- `pip install Pillow==10.0.0`
- `pip install openai`

Alternatively, if you're running the script in a Jupyter notebook or Google Colab, include the following commands at the top of your script:

- `!pip install pytesseract==0.3.10`
- `!pip install pdf2image==1.16.3`
- `!pip install pandas==2.0.3`
- `!pip install langdetect==1.0.9`
- `!pip install Pillow==10.0.0`
- `!pip install openai`

## Usage

### Prepare Your PDF Files

Place all the PDF files you want to process in a specific directory. By default, the script looks in the `/content` directory.

### Set Up OpenAI API Key

Obtain your API key from OpenAI and set it as an environment variable named `OPENAI_API_KEY`.

- **Linux/macOS**: `export OPENAI_API_KEY='your-api-key-here'`
- **Windows**: `set OPENAI_API_KEY=your-api-key-here`

Alternatively, set it within the script (not recommended for security reasons): `openai.api_key = 'your-api-key-here'`

### Adjust the PDF Directory Path (if necessary)

Modify the `pdf_folder` variable in the script to point to your directory: `pdf_folder = "/path/to/your/pdf/folder"`

### Run the Script

Execute the script using your preferred method (e.g., command line, IDE, Jupyter notebook).

### View the Results

The script will output a Pandas DataFrame displaying the extracted information from each PDF file.

## Script Overview

### Importing Libraries

The script imports necessary libraries for OCR, PDF processing, data manipulation, language detection, image processing, and OpenAI API interaction.

### Helper Functions

- **`clean_text(text)`**: Cleans the OCR-extracted text to normalize whitespace and standardize characters for better processing.
- **`preprocess_image(image)`**: Enhances the image by converting it to grayscale, increasing contrast, and applying a sharpening filter to improve OCR accuracy, especially for handwritten text.
- **`extract_information(text)`**: Uses an LLM via OpenAI's API to extract fields such as Company Name, Company Identifier, Document Purpose, and Key Terms from the OCR text.

### Processing PDF Files

#### Listing PDF Files

The script lists all PDF files in the specified directory.

#### Processing Each File

For each PDF file, it:

- Converts the first page to an image using pdf2image.
- Preprocesses the image for better OCR results.
- Performs OCR on the image using Tesseract with multi-language support (`eng+fra+ned+deu`).
- Extracts information using the LLM and appends the data to a list.

### Data Compilation

#### DataFrame Creation

Compiles all extracted data into a Pandas DataFrame for easy viewing and analysis.

#### Displaying Results

The script displays the DataFrame, showing the extracted information for each PDF file processed.

## Configuration

Add any configuration details here if necessary.

## Output

Describe the expected output of the script.

## Troubleshooting

### OpenAI API Errors

Ensure your API key is correctly set and has sufficient privileges. Handle API exceptions and rate limits as per OpenAI's guidelines.

### TesseractNotFoundError

Ensure Tesseract OCR is installed and added to your system's PATH. Verify installation by running `tesseract --version` in your command line.

### Poppler Installation Issues

pdf2image requires Poppler to be installed. Make sure Poppler is installed and the path is correctly set.

### Incorrect OCR Results

Poor image quality can affect OCR accuracy. Adjust the `preprocess_image` function parameters to improve image clarity.

### JSON Parsing Errors

The LLM may occasionally return improperly formatted JSON. Ensure proper exception handling is in place in the `extract_information` function.

### File Not Found Error

Ensure the `pdf_folder` path is correct and that it contains PDF files.

