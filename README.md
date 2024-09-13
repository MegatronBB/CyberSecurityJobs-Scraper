![AIM](AIM.jpg)

# Cybersecurity Job Scraper
This Python script is designed to scrape entry-level cyber security job postings from the [JSearch API](https://rapidapi.com/jsearch/api/job-search). It retrieves job data, processes it, and saves it into both JSON and CSV formats for easy analysis.
 Overview
The script performs the following tasks:

1. **Send API Request**: It sends a request to the JSearch API to retrieve job postings related to "cybersecurity".
2. **Process Response**: It processes the JSON response to extract relevant job details.
3. **Save Data**: It saves the raw data into a JSON file and formats the data for CSV output.
4. **Export Data**: It writes the formatted data into a CSV file.

# Prerequisites
 - Python 3.x
 - `requests` library
 - `json` library (standard in Python)
 - `csv` library (standard in Python)
 - `datetime` library (standard in Python)

# Installations 
Install the `requests` library if you haven't already:

pip install requests
 
## How It Works
1.	API Request:
○	The script defines the API URL and query parameters for retrieving job postings.
○	It includes headers for authentication with the JSearch API.
2.	Handle API Response:
○	The script makes a GET request to the API and checks if the response status is 200 OK.
○	It then saves the JSON response to a file named jobs_data.json.
3.	Extract and Clean Data:
○	The script extracts job details from the JSON response.
○	It handles missing or incomplete data by using default values and ensures all data is properly formatted.
○	It combines fields for better readability (e.g., Location combining city, state, and country).
4.	Prepare CSV Data:
○	The script formats the extracted job data into a list of dictionaries.
○	It sorts the job list by Job Title and Company Name.
5.	Write to CSV:
○	It writes the formatted job data into a CSV file named jobs_data.csv with appropriate headers.

## Usage
1.	Set Up Your API Key: Replace YOUR_RAPIDAPI_KEY in the headers dictionary with your own RapidAPI key.
2.	Run the Script: Execute the script using Python. It will fetch the job data, process it, and create jobs_data.json and jobs_data.csv files in the current directory.
3.	Review Output: Check the jobs_data.json for raw data and jobs_data.csv for the formatted data.

## Notes
●	Ensure you have a valid API key from RapidAPI.
●	The API query is set to retrieve jobs related to "cybersecurity". Modify the query string parameters if you need different search criteria.
●	The script handles basic data cleaning and formatting. Further customization may be needed based on specific requirements or API changes. For further information or assistance, please refer to the RapidAPI documentation or contact the API provider.
This `README.md` provides a clear overview of how the script works, installation instructions, and usage guidelines. Feel free to customize it further based on your specific needs or preferences.

## Script
    # import requests
    import json
    import csv
    from datetime import datetime
    
    url = "https://jsearch.p.rapidapi.com/search"
    querystring = {"query":"cybersecurity","page":"1","num_pages":"1","date_posted":"all"}
    
    headers = {
    "x-rapidapi-key": "09a4dda10fmshab2b1b95642a0e3p1ea115jsn662ff359d59c",
    "x-rapidapi-host": "jsearch.p.rapidapi.com"
    }
    
    response = requests.get(url, headers=headers, params=querystring)

    print(response.json())

 ## Making the API request
response = requests.get(url, headers=headers, params=querystring)

 ## Check if the request was successful
if response.status_code == 200:
    data = response.json()

    # Save JSON response to a file
    with open('jobs_data.json', 'w') as json_file:
        json.dump(data, json_file, indent=4)

    # Extract relevant data
    jobs = data.get('data', [])
    job_list = []

    # Extract job details and prepare data for CSV 
    
## Data cleaning and handling
    # job_list = []
    for job in jobs:
    job_id = job.get('job_id', 'N/A').strip()
    employer_name = job.get('employer_name', 'N/A').strip()
    employer_logo = job.get('employer_logo', 'N/A').strip()
    employer_website = job.get('employer_website', 'N/A')
    if employer_website: # Check if employer_website is not None
        employer_website = employer_website.strip()
    employer_company_type = job.get('employer_company_type')
    if employer_company_type:
        employer_company_type = employer_company_type.strip()
    else:
        employer_company_type = 'N/A'
    employer_linkedin = job.get('employer_linkedin', 'N/A')
    job_publisher = job.get('job_publisher', 'N/A').strip()
    job_employment_type = job.get('job_employment_type', 'N/A').strip()
    job_title = job.get('job_title', 'N/A').strip()
    job_apply_link = job.get('job_apply_link', 'N/A').strip()
    apply_options = job.get('apply_options', 'N/A')
    job_description = job.get('job_description', 'N/A').strip()
    job_is_remote = 'Remote' if job.get('job_is_remote') else 'On-Site'
    job_posted_at_timestamp = str(job.get('job_posted_at_timestamp', 'N/A')).strip()
    job_posted_at_datetime_utc = job.get('job_posted_at_datetime_utc', 'N/A').strip()
    job_city = job.get('job_city', 'N/A')
    if job_city:
        job_city = job_city.strip()
    job_state = job.get('job_state', 'N/A').strip()
    job_country = job.get('job_country', 'N/A').strip()
    job_latitude = str(job.get('job_latitude', 'N/A')).strip()
    job_longitude = str(job.get('job_longitude', 'N/A')).strip()
    job_benefits = job.get('job_benefits', 'N/A')
    job_google_link = job.get('job_google_link', 'N/A').strip()
    job_offer_expiration_datetime_utc = job.get('job_offer_expiration_datetime_utc', 'N/A')
    job_offer_expiration_timestamp = str(job.get('job_offer_expiration_timestamp', 'N/A')).strip()
    job_required_experience = job.get('job_required_experience', 'N/A')
    job_required_skills = ', '.join(job.get('job_required_skills', [])) if job.get('job_required_skills') else 'N/A'
    job_required_education = job.get('job_required_education', 'N/A')
    job_experience_in_place_of_education = str(job.get('job_experience_in_place_of_education', 'N/A')).strip()
    job_min_salary = str(job.get('job_min_salary', 'N/A')).strip()
    job_max_salary = str(job.get('job_max_salary', 'N/A')).strip()
    job_salary_currency = job.get('job_salary_currency', 'N/A')
    if job_salary_currency: # Check if job_salary_currency is not None
        job_salary_currency = job_salary_currency.strip()
    job_salary_period = job.get('job_salary_period', 'N/A')
    if job_salary_period:
        job_salary_period = job_salary_period.strip()
    job_highlights = job.get('job_highlights', 'N/A')
    job_posting_language = job.get('job_posting_language', 'N/A').strip()
    job_onet_soc = job.get('job_onet_soc', 'N/A').strip()
    job_onet_job_zone = job.get('job_onet_job_zone', 'N/A').strip()
    job_occupational_categories = ', '.join(job.get('job_occupational_categories', [])) if isinstance(job.get('job_occupational_categories', []), list) else 'N/A'


## Append cleaned and formatted data to job list
    job_info = {
        'Job Title': job_title,
        'Company Name': employer_name,
        'Location': f"{job_city}, {job_state}, {job_country}",  # Combined city, state, and country into 'Location'
        'Experience': job_required_experience,
        'Date Posted': job_posted_at_datetime_utc,
        'Job Description': job_description,
        'Job URL': job_apply_link,
        'Job Type': job_employment_type,
        'Salary': f"{job_min_salary} - {job_max_salary} {job_salary_currency}",  # Combined salary info
        'Industry': employer_company_type,
        'Skills': job_required_skills,
        'Qualifications': job_required_education,
        'Employment Type': job_employment_type,
        'Remote Status': job_is_remote,
        'Company Reviews': job_benefits,
        'Job Remote': job_is_remote
    }

## Append the job information to the job list
    job_list.append(job_info)

## Sort the job list by 'Job Title' and then by 'Company Name'
    # job_list.sort(key=lambda x: (x['Job Title'], x['Company Name']))

## Define CSV file headers
headers = [
    'Job Title', 'Company Name', 'Location', 'Experience', 'Date Posted', 'Job Description', 'Job URL',
    'Job Type', 'Salary', 'Industry', 'Skills', 'Qualifications', 'Employment Type', 'Remote Status',
    'Company Reviews', 'Job Remote'
]

## Write cleaned and sorted data to a CSV file
    # with open('jobs_data.csv', 'w', newline='', encoding='utf-8') as csv_file:
        writer = csv.DictWriter(csv_file, fieldnames=headers)
        writer.writeheader()
        writer.writerows(job_list)
     print("Data has been successfully written to jobs_data.json and jobs_data.csv")


