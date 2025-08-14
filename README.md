# FCJ-Workshop-MARKENDATION

# Workshop Proposals

# Markendation: Grocery Intelligence Platform

## 1. Executive Summary

Markendation is an intelligent grocery shopping platform designed as a personal project to help users find optimal stores and calculate costs for their ingredient shopping lists.

![Screenshot 2025-08-13 at 16.02.10.png](Workshop%20Proposals%2024ec60951d8880fa9f17e09a1330f1d6/Screenshot_2025-08-13_at_16.02.10.png)

## Project Overview

### Business Objectives

- **Smart Shopping Experience**: Powered ingredient matching and store recommendations
- **Cost Optimization**: Real-time price comparison across multiple grocery chains
- **Personal Learning**: Hands-on experience with AWS cloud services

### Core Platform Features

- **Intelligent Ingredient Matching**: Powered fuzzy matching using n-grams and Jaccard similarity
- **Location-Based Store Finder**: GPS-enabled store recommendations with distance calculations
- **Dynamic Price Comparison**: Real-time cost analysis across grocery chains (BHX, WM, etc.)
- **Recipe Management System**: Dish creation with automated ingredient extraction
- **User Authentication**: Secure Google OAuth integration
- **Administrative Dashboard**: Comprehensive store management and analytics

## AWS Cloud Architecture

![AWS-MARKENDATION.drawio.png](Workshop%20Proposals%2024ec60951d8880fa9f17e09a1330f1d6/AWS-MARKENDATION.drawio.png)

### Simplified Multi-Tier Architecture

**Tier 1: Content Delivery & API Management**
- **Amazon CloudFront**: CDN for static assets
- **API Gateway**: Centralized API management with basic rate limiting

**Tier 2: Network Infrastructure (Single AZ)**
- **VPC (Virtual Private Cloud)**: Basic network environment in single availability zone
- **Public Subnet**: Internet-facing resources (NAT Gateway, Load Balancer)
- **Private Subnet**: Backend services and databases
- **Internet Gateway**: Internet connectivity
- **NAT Gateway**: Outbound internet access (or NAT Instance for cost savings)

**Tier 3: Application Layer**
- **Application Load Balancer**: Basic traffic distribution
- **Amazon ECS with Fargate**: Serverless containers
- **Amazon ECR**: Container image registry

**Tier 4: Data Layer**
- **Amazon DynamoDB**: On-demand billing for cost efficiency
- **Amazon ElastiCache**: Single node Redis for caching (t3.micro)

**Tier 5: Serverless Processing**
- **AWS Lambda**: Event-driven functions for crawling and processing
- **Amazon SQS**: Message queuing
- **Amazon CloudWatch**: Basic monitoring and logging

## Microservices Architecture

### Core Service Components

**Location Service (AWS Lambda)**
- Basic geospatial calculations for store proximity
- Simple distance calculations using GPS coordinates
- Basic store recommendations based on distance

**Crawling Service (AWS Lambda)**
- Scheduled web scraping for grocery store prices
- Simple data collection from 2-3 retail websites
- Basic data validation and storage
- Cost-effective serverless execution

**User Management Service (ECS Fargate - 1 instance)**
- Basic user authentication with Google OAuth
- Simple JWT token management
- User profile storage in DynamoDB
- Minimal resource allocation

**Store & Product Service (ECS Fargate - 1 instance)**
- Combined service for cost efficiency
- Basic store catalog management
- Simple product matching algorithms
- Price comparison for limited stores

**Cost Calculation Service (AWS Lambda)**
- Basic cost optimization algorithms
- Simple shopping list calculations
- Lightweight recommendation engine
- Event-driven processing

## Data Architecture & Storage Strategy

### Primary Database: Amazon DynamoDB

- **Users Table**: Basic user profiles and authentication
- **Stores Table**: Store information with basic location data
- **Products Table**: Product catalog with current pricing
- **Ingredients Table**: Basic ingredient database with Vietnamese translations
- **Shopping Sessions**: User shopping baskets

### Caching Strategy: Amazon ElastiCache (t3.micro)

- **Product Cache**: Popular product information and prices
- **Location Cache**: Recent location queries

### Data Processing

- **Lambda Functions**: Simple data processing and ETL operations
- **Scheduled Jobs**: Daily price updates and data cleanup
- **Basic Analytics**: Simple usage statistics and reporting

## Cost Analysis & Budget

### Estimated Monthly Operational Costs

| Services | Cost estimation |
| --- | --- |
| **ECS Fargate Services** | $50-100 (2 small containers) |
| **AWS Lambda Functions** | $10-30 (low execution frequency) |
| **DynamoDB On-Demand** | $20-50 (based on actual usage) |
| **ElastiCache (t3.micro)** | $15-25 (single node) |
| **API Gateway** | $10-20 (based on API calls) |
| **CloudWatch & Other Services** | $10-20 (basic monitoring) |
| **Data Transfer & Storage** | $5-15 |
| Total | $120-260 |
