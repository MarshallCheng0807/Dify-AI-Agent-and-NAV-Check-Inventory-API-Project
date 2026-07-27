This is a Microsoft Dynamics NAV Inventory AI Assistant that uses a Dify workflow
It integrates Microsoft Dynamics NAV SOAP service to retrieve inventory availability information and provide responses through an LLM-powered chat interface
FEATURES:
-Extract item numbers from user requests
-Query ERP inventory service through SOAP
-Returns Item Number, Description, Unit Price, Available Quantity, Minimum Order Quantity, and Availability Status
-Restricts responses to inventory-related quesitons
-Dify workflow uses Parameter Extraction, HTTP Request, LLM Processing, and Structured Response Generation
NOTES:
This repository contains a sanitized verison fo the workflow for demonstration and portfolio purposes.
The follow have been removed or replaced:
-API endpoints
-Authentication details
-Service account information
-Internal hostnames
-Identifiers
-Model names
EXAMPLE USER QUESTIONS:
-What is the availability of item 1000?
-Check stock for item ABC123?
-Do we have item 2500 available?
