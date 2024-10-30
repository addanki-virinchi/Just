# Web Scraper Code Documentation

## Overview
This document explains a Python web scraping script that collects company information from websites using Selenium with undetected-chromedriver. The script includes error handling, multiprocessing, and logging capabilities.

## Table of Contents
1. [Dependencies and Setup](#dependencies-and-setup)
2. [Core Components](#core-components)
3. [Main Functions](#main-functions)
4. [Error Handling](#error-handling)
5. [Best Practices](#best-practices)
6. [Usage Guide](#usage-guide)

## Dependencies and Setup

### Required Libraries
```python
import os
import time
import pandas as pd
import undetected_chromedriver as uc
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import multiprocessing
import logging
```

### Key Components:
- `undetected_chromedriver`: Helps bypass anti-bot measures
- `selenium`: For web automation and scraping
- `pandas`: For data handling and CSV operations
- `multiprocessing`: For parallel processing
- `logging`: For tracking operations and errors

## Core Components

### 1. Chrome Driver Initialization
```python
def initialize_chrome_driver():
    """Initialize Chrome driver with enhanced options"""
```
This function:
- Sets up Chrome with specific options for stability
- Handles both new installations and existing ChromeDriver
- Configures browser settings to minimize detection
- Includes error handling and logging

### 2. Safe Element Finding
```python
def safe_find_element(driver, by, selector, timeout=10, retries=3):
    """Safely find an element with retries"""
```
Purpose:
- Reliably locate web elements
- Implement retry mechanism
- Handle timeouts and stale elements
- Return None instead of throwing exceptions

### 3. Page Load Handling
```python
def wait_for_page_load(driver, timeout=30):
    """Wait for page to load completely"""
```
Features:
- Ensures complete page loading
- Handles dynamic content
- Prevents premature element access
- Includes timeout protection

## Main Functions

### 1. Data Scraping Function
```python
def scrape_company_data(url):
    """Main scraping function"""
```
This function:
- Initializes data structure for company information
- Manages ChromeDriver lifecycle
- Implements retry mechanism
- Extracts company details:
  - Location
  - Phone Number
  - Website
  - Description
  - Company Name
  - Fax
  - Tags

### 2. URL Management
```python
def read_urls_from_csv(filename='company_urls_2.csv'):
    """Read URLs from CSV file"""
```
Features:
- Reads URLs from CSV
- Validates input data
- Handles file operations
- Includes error logging

### 3. Results Handling
```python
def save_results(results, filename='lawyers_1.csv'):
    """Save results to CSV"""
```
Capabilities:
- Saves scraped data to CSV
- Calculates success rates
- Logs operation results
- Handles save errors

## Error Handling

### 1. Retry Mechanism
- Multiple attempts for failed scrapes
- Increasing delays between retries
- Detailed error logging
- Status tracking for each attempt

### 2. Exception Types Handled
```python
try:
    # Scraping operations
except (TimeoutException, StaleElementReferenceException) as e:
    # Specific error handling
except Exception as e:
    # General error handling
```

### 3. Logging System
```python
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(levelname)s - %(message)s',
    filename=f'scraping_log_{datetime.now().strftime("%Y%m%d_%H%M%S")}.log'
)
```
Features:
- Timestamped log files
- Different log levels
- Detailed error tracking
- Operation status logging

## Best Practices

### 1. Resource Management
- Proper driver cleanup
- Memory management
- Process pool handling
- File handle management

### 2. Performance Optimization
- Parallel processing
- Efficient waiting strategies
- Resource cleanup
- Memory usage optimization

### 3. Anti-Detection Measures
- Randomized delays
- Browser fingerprint management
- Request pattern variation
- Error recovery strategies

## Usage Guide

### 1. Basic Usage
```python
if __name__ == "__main__":
    try:
        main()
    except KeyboardInterrupt:
        logging.info("Scraping interrupted by user")
    except Exception as e:
        logging.error(f"Fatal error: {e}")
```

### 2. Configuration
Required files:
- Input: 'company_urls_2.csv' with URLs
- Output: 'lawyers_1.csv' for results
- Logs: Automatically generated with timestamp

### 3. Customization Points
- Number of parallel processes
- Retry attempts
- Timeout values
- Selectors for different websites

### 4. Monitoring
- Check log files for progress
- Monitor success rates
- Track error patterns
- Adjust parameters as needed

## Common Issues and Solutions

### 1. Connection Issues
- Implement longer timeouts
- Add retry mechanism
- Use proxy rotation if needed
- Handle network errors

### 2. Element Location
- Use multiple selector strategies
- Implement wait conditions
- Handle dynamic content
- Use robust element finding

### 3. Anti-Bot Detection
- Randomize actions
- Add natural delays
- Use undetected-chromedriver
- Implement session management

## Maintenance and Updates

### 1. Regular Updates
- Keep dependencies updated
- Check for ChromeDriver updates
- Monitor website changes
- Update selectors as needed

### 2. Performance Monitoring
- Track success rates
- Monitor execution times
- Check resource usage
- Optimize as needed

## Conclusion
This web scraper is designed for reliability and efficiency, with robust error handling and logging. Regular maintenance and monitoring will ensure optimal performance. For specific issues or customizations, consult the logs and adjust parameters accordingly.
