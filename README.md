# Microsoft Dynamics NAV Inventory AI Assistant

A small integration that connects a Microsoft Dynamics NAV (Navision) API codeunit to an AI workflow on Dify. It allows users to query item availability in a chat interface and returns structured inventory information (item, description, unit price, available quantity, minimum order quantity, availability status).

## Table of Contents
- [Features](#features)
- [Architecture / Workflow Overview](#architecture--workflow-overview)
- [Prerequisites](#prerequisites)
- [Configuration](#configuration)
- [Local Setup & Run](#local-setup--run)
- [Example User Questions](#example-user-questions)
- [Sample Response (structured)](#sample-response-structured)
- [Development Notes](#development-notes)
- [Testing](#testing)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## Features
- Extracts item numbers from user requests using the Dify parameter-extraction step.
- Queries ERP inventory via Microsoft Dynamics NAV SOAP service.
- Returns structured inventory details:
  - Item Number
  - Description
  - Unit Price
  - Available Quantity
  - Minimum Order Quantity
  - Availability Status
- Restricts responses to inventory-related queries (intent filtering in the workflow).
- Dify workflow includes: Parameter Extraction → HTTP Request to NAV SOAP → LLM Processing → Structured Response Generation.

## Architecture / Workflow Overview
1. User sends a chat prompt (e.g., "Do we have item 2500 available?").
2. Dify workflow extracts parameters (item IDs/strings).
3. Workflow issues an HTTP request to your API codeunit (which calls NAV SOAP).
4. NAV SOAP returns inventory data.
5. Dify processes the response with LLM logic to produce a concise, sanitized output and a structured JSON payload.

(Consider adding a small diagram or flowchart here in /docs or the repo root.)

## Prerequisites
- Microsoft Dynamics NAV instance with a SOAP service or codeunit that exposes inventory lookup.
- Dify account and a workflow configured for the assistant.
- Node / Python / whatever runtime the repo uses (document exact stack here).
- Access to repository and ability to set secrets (API keys, SOAP credentials).

## Configuration
This repository omits secrets for security. Set the following environment variables or configuration values when you run the project:

- NAV_SOAP_URL — The NAV SOAP endpoint (e.g., `https://nav.company.local/WS/Codeunit/InventoryAPI`)
- NAV_USERNAME — SOAP auth username (if required)
- NAV_PASSWORD — SOAP auth password (if required)
- DIFY_API_KEY — API key to call Dify (if you call Dify from a server)
- DIFY_WORKFLOW_ID — ID of your Dify workflow (if applicable)
- OTHER_API_ENDPOINT — local/hosted endpoint if your codeunit is wrapped by an API gateway

Add examples or .env template in the repo (e.g., `.env.example`).

## Local Setup & Run
1. Clone the repo:
   git clone https://github.com/MarshallCheng0807/Dify-AI-Agent-and-NAV-Check-Inventory-API-Project.git
2. Copy `.env.example` to `.env` and fill values.
3. Install dependencies (example):
   - Node: `npm install` or
   - Python: `pip install -r requirements.txt`
4. Start the app:
   - Node: `npm start`
   - Python: `python app.py`
5. Trigger a sample request (see below) or connect to the chat UI.

(Adjust commands to match the project stack; add exact scripts.)

## Example User Questions
- What is the availability of item 1000?
- Check stock for item ABC123?
- Do we have item 2500 available?

## Sample Response (structured)
The assistant returns a friendly text response and a structured JSON payload. Example structured response:

```json
{
  "item_number": "2500",
  "description": "Widget Model X",
  "unit_price": 12.50,
  "available_quantity": 32,
  "minimum_order_quantity": 1,
  "availability_status": "In Stock",
  "raw_source": {
    "nav_response_id": "abc123",
    "timestamp": "2026-07-27T12:00:00Z"
  }
}
