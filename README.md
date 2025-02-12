# Starbucks-menu
echo "# Starbucks-menu" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/ariel816/Starbucks-menu.git
git push -u origin main
pip install requests beautifulsoup4 selenium pandas
import requests
from bs4 import BeautifulSoup
import pandas as pd

url = "https://www.menuwithprice.com/menu/starbucks/"
headers = {"User-Agent": "Mozilla/5.0"}

response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.text, "html.parser")

# Find the table with prices
menu_items = []
for item in soup.select(".menu-row"):
    name = item.select_one(".menu-item-name").text.strip()
    price = item.select_one(".menu-item-price").text.strip()
    menu_items.append({"Drink": name, "Price": price})

# Convert to DataFrame
df = pd.DataFrame(menu_items)
print(df)

# Save to CSV
df.to_csv("starbucks_prices.csv", index=False)
