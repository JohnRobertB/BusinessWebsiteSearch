# BusinessWebsiteSearch

This script is designed to work with an Excel file named Clients.xlsx. The script assumes that this file contains a column titled 'Clients' that contains the names of businesses. If a business name does not have an associated website in the 'Website' column, the script will use the googlesearch library to search Google for the business name and retrieve the first result as the business's website.

This script uses the pandas library to read and manipulate the Excel file, and the tqdm library to display a progress bar during the search process. In order to prevent a single search from taking too long, the script uses the signal library to set a timeout of 10 seconds for each search.

Once the search process is complete, the script writes the updated DataFrame back to the Excel file.

Dependencies: 
pandas
googlesearch
tqdm
signal
time


#Email_search 
the script is designed to work with an Excel file named Clients.xlsx. This file should contain a column titled 'Website' with the URLs of business websites. If an email address is not already provided in the 'Email' column, the script will send a GET request to the URL in the 'Website' field and scrape the page for email addresses.

To avoid being blocked by the website, the script rotates the user agent for each request from a list of user agent strings. After each request, it waits for 5 seconds to throttle the requests and be respectful to the server.


Disclaimer

Please note that the use of web scraping tools should comply with the terms and conditions of the service being scraped. In the case of many websites, extensive automated queries can be seen as a violation. Always respect the rules and regulations related to data scraping to avoid any legal issues.

