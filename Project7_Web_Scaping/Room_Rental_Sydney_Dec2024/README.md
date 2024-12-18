# Room Listings Scraper - Sydney

## Project Overview
This project is a web scraping script designed to extract room rental listings from [ozflatmates.com](https://ozflatmates.com) for Sydney. The script automates the process of gathering room details such as the room description, suburb, price, and publish date from multiple pages of listings. The extracted data is saved into a CSV file (`room_listings.csv`) for easy analysis and further processing using tools like Python, Excel, or Tableau.

## Features
- Scrapes room listings from six pages of room rentals in Sydney.
- Extracts key details including Listing ID, Room Description, Suburb, Price, and Publish Date.
- Saves the extracted data into a CSV file.
- Implements a delay between requests to avoid overwhelming the server.
- Fetches additional details like the publish date by accessing individual listing pages.
- Uses Python libraries `requests`, `BeautifulSoup`, `csv`, `time`, and `pandas`.

## Requirements
- Python 3.x
- Required Libraries:
  ```bash
  pip install requests beautifulsoup4 pandas
  ```

## Usage
1. **Clone or download the project files**.
   
2. **Run the script**:
   ```bash
   python scraper.py
   ```
   The script will start scraping room listings from ozflatmates.com, fetching details for each listing and saving them to `room_listings.csv`.

3. **Analyze the Data**:
   Once the data is scraped, you can use `pandas` or any other data analysis tool to analyze the `room_listings.csv` file. Here's an example of loading the data using `pandas`:
   ```python
   import pandas as pd
   df = pd.read_csv('room_listings.csv')
   print(df.head())
   ```

## Data Output
The output file `room_listings.csv` contains the following columns:
- `Listing ID`: Unique identifier for each listing.
- `Room Description`: Brief description of the room or flat.
- `Suburb`: Suburb where the room is located.
- `Price`: Rental price of the room.
- `Publish Date`: The date the listing was published.

## Example Output
| Listing ID | Room Description                              | Suburb         | Price | Publish Date |
|------------|-----------------------------------------------|----------------|-------|--------------|
| ID32860    | Sydney CBD Room                               | Sydney         | 450   | 15.10.2024   |
| ID32846    | Parramatta, quiet modern single room, female  | Granville      | 300   | 15.10.2024   |
| ID32838    | Active Christian Guys house, ideal for Medic  | Wentworthville | 390   | 13.10.2024   |
| ID32835    | Homey Room in 2 Bedroom 2 Bathroom Flat!      | Rydalmere      | 340   | 13.10.2024   |

## Notes
- The script includes a delay of 2 seconds between requests to avoid overwhelming the server.
- It scrapes six pages of listings but can be adjusted by modifying the `for` loop.

## Future Improvements
- Add error handling for network issues or missing data.
- Scrape additional details such as room images, room type (shared/private), and contact information.
- Expand the scraping functionality to cover more cities or regions.

## License
MIT License

Copyright (c) [2024] [Aimee Le]
