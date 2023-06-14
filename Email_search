import pandas as pd
import numpy as np
import re
import requests
from bs4 import BeautifulSoup
import time
from tqdm import tqdm

def find_email(url, user_agent):
    try:
        # Send a GET request to the website
        headers = {"User-Agent": user_agent}
        response = requests.get(url, headers=headers)

        # Parse the response with BeautifulSoup
        soup = BeautifulSoup(response.text, 'html.parser')

        # Find all text on the page
        text = soup.get_text()

        # Use a regular expression to find email addresses
        email_addresses = re.findall(r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b', text)

        # Return the email addresses
        return ', '.join(email_addresses)
    except requests.exceptions.RequestException as e:
        return f"Network error: {e}"
    except Exception as e:
        return f"An error occurred: {e}"

# Load the Excel file
df = pd.read_excel('Clients.xlsx')

# If the 'Email' column does not exist, add it
if 'Email' not in df.columns:
    df['Email'] = np.nan

# List of user agents
user_agents = [
    'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3',
    # add more user agent strings here
]

# Assume the websites are in a column named 'Website'
for i in tqdm(range(len(df))):
    website = df.loc[i, 'Website']
    email = df.loc[i, 'Email']

    if pd.isnull(website):  # if the website field is empty
        continue  # skip this row

    if pd.isnull(email):  # if the 'Email' field is empty
        user_agent = np.random.choice(user_agents)  # choose a random user agent
        email = find_email(website, user_agent)
        df.loc[i, 'Email'] = email  # add the email addresses to the DataFrame
        print(f"Found email addresses for {website}: {email}")
        time.sleep(5)  # wait for 5 seconds to throttle requests

# Write the DataFrame back to the Excel file after all updates
df.to_excel('websites.xlsx', index=False)
