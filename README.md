# ReceiptsBot
Automates the extraction and translation of data from the bills sent via Telegram.

# Receipt OCR Processor (N8N Workflow)

This project automates the processing of the receipts using an N8N workflow. It receives receipt images via Telegram, performs OCR with Mistral AI, translates the extracted text using Google Gemini, and stores the results in Google Drive. Finally, it sends a summary of the receipt back to the Telegram user.

## Features

* **Telegram Integration:** Receives receipt images directly from Telegram.
* **OCR with Mistral AI:** Extracts text from the receipt images.
* **Translation with Google Gemini:** Translates the extracted the text. Any language to any language.
* **Google Drive Storage:** Saves the original image and translated text to Google Drive.
* **Telegram Summary:** Sends a processed summary of the receipt back to the user via Telegram.
* **Text Sanitization:** Sanitizes the text for Telegram Markdown compatibility.

## Workflow Overview

The N8N workflow consists of the following nodes:

1.  **Telegram Trigger:**
    * Triggers the workflow when a file (specifically a photo) is sent via Telegram.
    * Retrieves the file ID of the received photo.
2.  **Telegram (File Download):**
    * Downloads the photo file from Telegram using the file ID.
    * Retrieves the webContentLink of the downloaded file.
3.  **Google Drive (File Upload):**
    * Uploads the downloaded photo to a specified Google Drive folder.
4.  **Mistral IMAGE OCR:**
    * Sends the Google Drive image URL to the Mistral AI OCR API.
    * Extracts the text from the image.
5.  **Basic LLM Chain (Google Gemini):**
    * Uses Google Gemini to translate the extracted text and create a summary of the bill.
6.  **Code (Text Sanitization):**
    * Sanitizes the generated text for telegram markdown.
7.  **Telegram1 (Message Send):**
    * Sends the translated summary back to the user via Telegram.

## Prerequisites

* An N8N instance.
* A Telegram Bot API token.
* Google Cloud Platform credentials for Google Drive API.
* Mistral AI API Key.
* Google Gemini (PaLM) API Key.
* N8N Telegram node installed.
* N8N Google Drive node installed.
* N8N HTTP Request node installed.
* N8N Langchain Google Gemini chat Model node installed.
* N8N Code node Installed.

## Installation and Setup

1.  **Import the Workflow:**
    * Copy the provided JSON workflow.
    * In your N8N instance, import the workflow using the "Import from JSON" option.
2.  **Configure Credentials:**
    * Set up the Telegram API credentials in the "Telegram Trigger," "Telegram", and "Telegram1" nodes.
    * Set up the Google Drive OAuth2 API credentials in the "Google Drive" node.
    * Set up the Mistral Cloud API credentials in the "Mistral IMAGE OCR" node.
    * Set up the Google Gemini (PaLM) Api credentials in the "Google Gemini Chat Model" Node.
3.  **Configure Google Drive Folder:**
    * In the "Google Drive" node, specify the folder where you want to save the receipts.
4.  **Activate the Workflow:**
    * Activate the workflow in N8N.
5.  **Setup Telegram Bot:**
    * Setup the telegram bot and be sure that is configured to receive files.

## Usage

1.  Start a conversation with your Telegram bot.
2.  Send an image of a bill or receipt.
3.  The workflow will automatically process the image, translate the text, and send you a summary.
4.  The original image and extracted data will be saved to your Google Drive folder.

## Notes

* Ensure that your API keys are securely stored and not exposed.
* The workflow is configured to process images sent as photos via Telegram.
* This workflow is configured to work with any receipts.
* You may need to adjust the prompt in the "Basic LLM Chain" node to better suit your needs.
