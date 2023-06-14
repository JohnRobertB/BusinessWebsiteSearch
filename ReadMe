import pandas as pd
from googlesearch import search
import time
import signal
from tqdm import tqdm

# Define a handler for the alarm
def handler(signum, frame):
    raise Exception("Timeout")

# Set the signal handler
signal.signal(signal.SIGALRM, handler)

def find_website(business_name):
    try:
        # Set an alarm for 10 seconds
        signal.alarm(10)
        for url in search(business_name, num_results=1):
            # Cancel the alarm
            signal.alarm(0)
            return url
    except TimeoutError:
        print(f"Timeout occurred while searching for {business_name}")
    except Exception as e:
        print(f"An error occurred: {e}")
    finally:
        # Cancel the alarm
        signal.alarm(0)

# Load the Excel file
df = pd.read_excel('Clients.xlsx')

# Assume the business names are in a column named 'Clients'
# and websites are in a column named 'Website'
for i in tqdm(range(len(df))):
    business_name, website = df.loc[i, 'Clients'], df.loc[i, 'Website']

    if pd.isnull(website):  # if the website field is empty
        website = find_website(business_name)
        df.loc[i, 'Website'] = website  # add the website to the DataFrame
        print(f"Found website for {business_name}: {website}")

# Write the DataFrame back to the Excel file after all updates
df.to_excel('Clients.xlsx', index=False)

