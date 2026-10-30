# Microsoft Dynamics NAV Inventory AI Assistant

A small integration that connects a Microsoft Dynamics NAV (Navision) API codeunit to an AI workflow on Dify. It allows users to query item availability in a chat interface and returns structured inventory information (item, description, unit price, available quantity, minimum order quantity, availability status).

## Table of Contents
- [Features](#features)
- [Architecture / Workflow Overview](#architecture--workflow-overview)
- [Configuration](#configuration)
- [Example User Questions](#example-user-questions)

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

## Configuration
This repository omits secrets for security. Set the environment variables or configuration values when you run the project such as the endpoint URL, username, password etc.

## Example User Questions
- What is the availability of item 1000?
- Check stock for item ABC123?
- Do we have item 2500 available?

