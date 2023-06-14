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
