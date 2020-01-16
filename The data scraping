import requests
import pandas as pd
import csv   
import datetime
url = 'https://www.nigeriapropertycentre.com/for-sale/houses?q=for-sale+houses'
page = requests.get(url)
from bs4 import BeautifulSoup
soup = BeautifulSoup(page.content, 'html.parser')
items = soup.find_all('div', {'class' : 'col-md-12'})
end_page_num = 23

filename = "nigeriaprop_houses.csv"
with open(filename, "w+") as f:

    writer = csv.writer(f)
    writer.writerow(["Listing_type", 'Location', "Price","Bedroom", 'Bathroom', 'Toilet', 'Parking'])
    i = 1
    while i <= end_page_num:

        r = requests.get("https://www.nigeriapropertycentre.com/for-sale/houses?q=for-sale+houses?page={}".format(i))

        soup = BeautifulSoup(r.text, "html.parser")
        items = soup.find_all('div', {'class' : 'col-md-12'})
        x = items[2:]
        
        for item in x:
            try:
                Listing_type = item.find('span').get_text()
            except:
                Listing_type = 'N/A'
            try:
                price = item.find_all('span', {'class' : "price"})
                Price = price[1].get_text()
            except:
                Price = '0'
            try:
                Location = item.find('address').get_text()
            except:
                Location = 'N/A'
            try:
                footer = item.find('div', {'class' :"wp-block-footer"})
                specs = footer.find_all('span')
                try:
                    Bedroom = specs[0].get_text()
                except:
                    Bedroom = '0'
                try:
                    Bathroom = specs[2].get_text()
                except:
                    Bathroom = '0'
                try:
                    Toilet = specs[4].get_text()
                except:
                    Toilet = '0'
                try:
                    Parking = specs[6].get_text()
                except:
                    Parking = '0'
            except:
                footer = 'N/A'

            writer.writerow([Listing_type, Location, Price, Bedroom, Bathroom, Toilet, Parking])
        i += 1
