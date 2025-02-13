# Flipkart_Product_page_URL
#Python Webscraping | Scrape Flipkart Product Page URL
#Get data from flipkart product list page 
#then get all the product name as well as product page lunks(URL)
#and then save it on the local machine like csv and other format.

import requests
from bs4 import BeautifulSoup
import pandas as pd

url="https://www.flipkart.com/mobiles/mi~brand/pr?sid=tyy,4io&otracker=nmenu_sub_Electronics_0_Mi"

req=requests.get(url)
#print(req.status_code)

content=BeautifulSoup(req.content,'html.parser')
#print(content.prettify)

data=content.find_all('div',{'class':'tUxRFH'})

links=[]
phone_name=[]
start_link="https://www.flipkart.com"

for items in data:
    rest_link=items.find('a')['href']
    name=items.find('div',attrs={'class':'KzDlHZ'})

    phone_name.append(name.text)
    links.append(start_link+rest_link)

#print(phone_name[0])
#print(links[0])

#df=pd.DataFrame({'name':phone_name,'links':links})
#print(df)

df={'name':phone_name,'links':links}
new_df=pd.DataFrame(df)
#print(new_df)

new_df.to_csv('flipkart_productURL.csv')
print("file successfully saved at the same location")
