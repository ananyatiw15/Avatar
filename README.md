# Avatar AI Character Composer Service
# Overview
The Avatar AI Character Composer Service ("Avatar") integrates Azure AI Custom Vision and Azure OpenAI to create character images based on user prompts. The service leverages a library of images from sources like Storior or Picrew and utilizes various Azure and Google Cloud services to deliver a seamless experience.
# Table of Contents
•	Overview
•	Architecture
•	Features
•	Prerequisites
•	Setup Instructions
•	Usage
•	Functions
•	Authentication
•	Contributing
•	License
# Architecture
1	User Interaction: User sends a POST request with a prompt from a Flutter app to the API Gateway in Google Cloud.
2	Prompt Processing: The request is handled by the process_prompt Google Cloud Function, which extracts keywords from the prompt and publishes them to a Google Pub/Sub topic.
3	Image Retrieval: The get_relevant_images function retrieves relevant tags and image URLs from Azure Cosmos DB and publishes this data to another Pub/Sub topic.
4	Image Composition: The compose_image function assembles a character image using the URLs from the Pub/Sub message. If suitable images are not found, Azure OpenAI generates a matching image.
5	Storage and Response: The composed image is stored in Azure Blob Storage, and its URL is sent back to the API Gateway via a POST request, which then returns it to the user.
# Features
•	Integration with Azure Custom Vision for image tagging and model training.
•	Use of Azure OpenAI for generating images when needed.
•	Storage of images and metadata in Azure Blob Storage and Cosmos DB.
•	Seamless communication between Google Cloud Functions using Pub/Sub.
•	Authentication using Azure Active Directory.
# Prerequisites
•	Azure Subscription
•	Google Cloud Platform (GCP) Account
•	Azure Custom Vision service
•	Azure Blob Storage
•	Azure Cosmos DB
•	Google Cloud Functions and Pub/Sub
•	Flutter development environment
# Setup Instructions
Azure Setup
1	Custom Vision
◦	Create a Custom Vision project in the Azure portal.
◦	Train the model with your dataset of images.
2	Blob Storage
◦	Create an Azure Blob Storage account and container.
◦	Upload your image dataset to the container.
3	Cosmos DB
◦	Create an Azure Cosmos DB account and database.
◦	Set up containers to store image metadata and tags.
4	OpenAI Service
◦	Set up Azure OpenAI service for image generation.
5	Authentication
◦	Register an application in Azure Active Directory for authentication.
◦	Grant necessary permissions to the application for accessing Blob Storage and Cosmos DB.
Google Cloud Setup
1	Cloud Functions
◦	Deploy the following functions:
▪	process_prompt
▪	get_relevant_images
▪	compose_image
2	API Gateway
◦	Set up an API Gateway to accept POST requests from the Flutter app.
3	Pub/Sub
◦	Create Pub/Sub topics for communication between cloud functions.
4	Authentication
◦	Configure service accounts and roles in GCP.
◦	Set up identity federation with Azure AD.
# Usage
1	Flutter App
◦	Users send a prompt via a POST request to the API Gateway.
2	API Gateway
◦	Forwards the request to the process_prompt function.
3	Cloud Functions and Pub/Sub
◦	Functions process the prompt, retrieve relevant images, and compose the final image.
4	Response
◦	The composed image URL is sent back to the user via the API Gateway.
Functions
process_prompt
•	Extracts keywords from the user prompt.
•	Publishes the keywords to a Pub/Sub topic.
get_relevant_images
•	Retrieves image tags and URLs from Azure Cosmos DB based on the keywords.
•	Publishes the retrieved data to another Pub/Sub topic.
compose_image
•	Assembles a character image using the image URLs from the Pub/Sub message.
•	Generates an image using Azure OpenAI if suitable images aren't found.
•	Stores the final image in Azure Blob Storage.
•	Sends the image URL back to the API Gateway.
Authentication
•	Use Azure Active Directory (AAD) for secure access to Azure services.
•	Configure service control policies to grant access to Google Cloud Functions.
•	Utilize identity federation between GCP and Azure for seamless authentication.
# Contributing
Contributions are welcome! Please open an issue or submit a pull request for any enhancements or bug fixes.
# License
This project is licensed under the MIT License. See the LICENSE file for details.


