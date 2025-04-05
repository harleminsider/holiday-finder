# holiday-finder
import requests

def get_holidays(country, year):
    api_url = f"https://date.nager.at/api/v3/PublicHolidays/{year}/{country}"
    response = requests.get(api_url)
    
    if response.status_code == 200:
        holidays = response.json()
        return holidays
    else:
        return {"error": "Could not fetch holiday data."}

def display_holidays(country, year):
    holidays = get_holidays(country, year)
    
    if "error" in holidays:
        print(holidays["error"])
        return
    
    print(f"🎉 Public Holidays in {country.upper()} for {year} 🎉\n")
    for holiday in holidays:
        print(f"📅 {holiday['date']} - {holiday['localName']}")
    
# Example usage
country_code = "US"  # Replace with country code (e.g., US, GB, DE, FR)
year = 2025  # Replace with desired year
display_holidays(country_code, year)
