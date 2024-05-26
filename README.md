# Text-Summarization-using-TxtAI
Text Summarization GenAI project using TxtAI

# Overview
This project focuses on developing a textual paragraph summarizer using the TxtAI library, Streamlit, and PyPDF2. The application allows users to input text or upload PDF documents, and then generates concise summaries using advanced natural language processing techniques.

# Features
* Text Summarization: Summarizes user-provided text inputs in real-time.
* Document Summarization: Extracts and summarizes text from uploaded PDF files.
* User-friendly Interface: Interactive and intuitive interface built with Streamlit.
* Real-time Processing: Provides instant summarization results.

# Installation
* Prerequisites
  Python 3.6 or higher

# Step-by-Step Installation
* Clone the repository:
  git clone https://github.com/yourusername/text-summarization-gen-ai.git
  cd text-summarization-gen-ai

* Install Streamlit:
  pip install streamlit

* Install TxtAI:
  pip install txtai

* Install PyPDF2:
  pip install PyPDF2

# Usage
* Run the Streamlit application:
  streamlit run app.py

* Interact with the application:
  ^ Summarize Text: Enter your text in the provided text area and click "Summarize Text".
  ^ Summarize Document: Upload a PDF file and click "Summarize Document".
# Example Code
  Below is the core code for the application:
* Python Code:
from txtai.pipeline import Summary
import streamlit as st
from PyPDF2 import PdfReader

st.set_page_config(layout="wide")

@st.cache_resource
def text_summary(text, maxlength=None):
    summary = Summary()
    result = summary(text, maxlength=maxlength)
    return result

def extract_text_from_pdf(file_path):
    with open(file_path, "rb") as f:
        reader = PdfReader(f)
        page = reader.pages[0]
        text = page.extract_text()
    return text

choice = st.sidebar.selectbox("Select your choice", ["Summarize Text", "Summarize Document"])

if choice == "Summarize Text":
    st.subheader("Summarize Text using txtai")
    input_text = st.text_area("Enter your text here")
    if input_text:
        if st.button("Summarize Text"):
            col1, col2 = st.columns([1, 1])
            with col1:
                st.markdown("*Your Input Text*")
                st.info(input_text)
            with col2:
                st.markdown("*Summary Result*")
                result = text_summary(input_text)
                st.success(result)

elif choice == "Summarize Document":
    st.subheader("Summarize Document using txtai")
    input_file = st.file_uploader("Upload your document here", type=['pdf'])
    if input_file:
        if st.button("Summarize Document"):
            with open("doc_file.pdf", "wb") as f:
                f.write(input_file.getbuffer())
            col1, col2 = st.columns([1, 1])
            with col1:
                st.info("File uploaded successfully")
                extracted_text = extract_text_from_pdf("doc_file.pdf")
                st.markdown("*Extracted Text is Below:*")
                st.info(extracted_text)
            with col2:
                st.markdown("*Summary Result*")
                text = extract_text_from_pdf("doc_file.pdf")
                doc_summary = text_summary(text)
                st.success(doc_summary)

# Project Contributions
* Innovative Features: Introduces real-time text summarization and PDF document processing.
* Enhanced NLP Techniques: Utilizes advanced natural language processing models from TxtAI.
* User-centric Design: Focuses on providing an intuitive and interactive user experience.
  
# Future Work
* Expand Supported Document Types: Add support for more document formats beyond PDF.
* Improve Summarization Accuracy: Continuously refine and enhance the summarization algorithms.
* Add Multilingual Support: Extend the summarization capabilities to multiple languages.
  
# License
This project is licensed under the MIT License. See the LICENSE file for details.

# Acknowledgements
* TxtAI for providing the summarization pipeline.
* Streamlit for the interactive web framework.
* PyPDF2 for PDF text extraction.

Feel free to customize this README file to better suit your project's specific details and requirements!
