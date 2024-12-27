# Query and Image Based Product Search and Virtual TryOn For Ecom Business with Whatsapp Integration
## Overview
This project delivers a comprehensive AI-driven solution designed to revolutionize the online shopping experience for e-commerce businesses. It integrates cutting-edge technologies to provide the following features:

- **AI-Powered Virtual Try-On**: Helps customers visualize how garments will look on them, reducing uncertainty and return rates.
- **Text and Image-Based Search**: Enhances product discovery with text and image queries.
- **WhatsApp Integration**: A user-friendly interface for customers to interact via their preferred communication channel.

---
## Business Impact

### Problem Statement
E-commerce businesses face challenges in engaging customers and reducing friction in the online shopping experience. Key points include:
- Limited tools for virtual visualization of products.
- Inefficient product search and discovery mechanisms.
- Lack of personalized customer interaction.

### Solution
This project addresses these challenges by:
1. **Improving Customer Engagement**: Virtual try-on boosts confidence in purchasing clothing items.
2. **Streamlining Search**: Text and image-based search ensures customers find products effortlessly.
3. **Convenience Through WhatsApp**: Customers can browse, search, and try products without switching platforms.

### Value Proposition
- **Increase in Sales**: Enhanced customer satisfaction drives higher conversion rates.
- **Reduced Return Rates**: Virtual try-on minimizes sizing and style mismatches.
- **Scalable Solution**: Seamlessly integrates into existing e-commerce systems.

---


## Features and workflow
### Virtual Try-On
- **API Used**: [Gradio Virtual Try-On](https://gradio.app/)
- **Workflow**:
  - Users upload a photo of themselves and a garment image.
  - The Gradio API processes these inputs and generates a try-on image.
  - The result is returned to the customer via WhatsApp.
    
### Pinecone
In this project, Pinecone is used to index and search embeddings generated from product images and text queries. It serves as the backbone for the image and text-based search functionality, providing fast and accurate results.

### Text-Based Search
- **Model Used**: [SentenceTransformers CLIP-ViT-B-32](https://huggingface.co/sentence-transformers/clip-ViT-B-32)
- **Workflow**:
  - User inputs a natural language query (e.g., "blue floral dress").
  - The query is converted to a vector using the CLIP model.
  - A similarity search is performed against a pre-indexed product catalog stored in Pinecone.


### Image-Based Search
- **Model Used**: CLIP (Image Encoding)
- **Workflow**:
  - Users upload an image of a product.
  - The image is resized and converted to a vector representation.
  - A similarity search is performed using Pinecone, returning visually similar products.


### WhatsApp Integration
- **API Used**: [Twilio WhatsApp Business API](https://www.twilio.com/whatsapp)
- **Features**:
  - Menu-driven interaction for users.
  - Supports image uploads and text queries.
  - Delivers processed results directly via WhatsApp.

---

## Project Setup

Before running this project, ensure you have the following:

### Twilio Setup
To integrate WhatsApp functionality into your application, follow these steps:

1. **Create a Twilio Account**:
   - Visit [Twilio](https://www.twilio.com/) and create an account.

2. **Activate the Twilio Sandbox for WhatsApp**:
   - In the Twilio console, navigate to the **Messaging** section and select **Try it Out** under the **WhatsApp Sandbox**.
   - Follow the instructions to join the sandbox by sending a WhatsApp message to the provided Twilio number.

3. **Get Your Twilio Account Credentials**:
   - Go to the **Settings** section in the Twilio console to find your **Account SID** and **Auth Token**.
   - Take note of the Twilio Sandbox number, which will be used to send and receive WhatsApp messages.

Once the sandbox is activated, you can send and receive messages to the WhatsApp sandbox number. This allows you to test your virtual try-on application.

---

### Hugging Face Setup
To leverage the virtual try-on capabilities, use the Nymbo Virtual Try-On API available on Hugging Face Spaces.

1. **Create a Hugging Face Account**:
   - Visit [Hugging Face](https://huggingface.co/) and sign up for an account.

2. **Use the Nymbo Virtual Try-On Model**:
   - This project uses the **Nymbo Virtual Try-On** API, built with the IDM-VTON (Image-based Virtual Try-On Network) model.
   - The model takes input images of a person and a garment to generate realistic try-on results.

---

### Ngrok Setup for Local Development
Since the Flask server runs locally, we use **ngrok** to expose the server to the internet, enabling Twilio's WhatsApp Sandbox to communicate with it.

1. **Download and Install ngrok**:
   - Visit the [ngrok website](https://ngrok.com/) and download the appropriate version for your operating system.
   - Follow the installation instructions provided on the website.

2. **Authenticate ngrok**:
   - After installing, authenticate ngrok by running:
     ```bash
     ngrok authtoken your_ngrok_auth_token
     ```
   - You can find your authentication token in your ngrok dashboard after signing up.

3. **Start ngrok**:
   - Run the following command to expose your local Flask server:
     ```bash
     .\ngrok http 8080
     ```
   - This will generate a forwarding URL (e.g., `https://e3e3-xxxx.ngrok-free.app`).

4. **Set Up Twilio Webhook**:
   - Copy the ngrok forwarding URL and set it as your Twilio webhook:
     - Navigate to the **WhatsApp Sandbox Settings** in the Twilio console.
     - Use the URL format:
       ```
       https://your-ngrok-url/webhook
       ```

---

## Installation

### Step 1: Clone the Repository
Clone this repository to your local machine:
```bash
git clone https://github.com/your-username/Query_and_Image_Based_Product_Search_and_Virtual_TryOn_For_Ecom_Business_with_Whatsapp_Integration.git
cd Query_and_Image_Based_Product_Search_and_Virtual_TryOn_For_Ecom_Business_with_Whatsapp_Integration
```

### Step 2: Install Required Dependencies
Install all necessary Python packages using the provided `requirements.txt` file:
```bash
pip install -r requirements.txt
```

### Step 3: Set Up Variables
Change the following variables in app.py:
```plaintext
TWILIO_ACCOUNT_SID=your_account_sid
TWILIO_AUTH_TOKEN=your_auth_token
NGROK_URL = your_ngrok_auth_token
```

### Step 4: Run the Application
Start the Flask server to run the application:
```bash
python app.py
```
