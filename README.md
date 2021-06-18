# Web-scraping
>Web Scripting is an automatic method to obtain large amounts of data from websites.</br> 
>Most of this data is unstructured data in an HTML format which is then converted into structured data in a spreadsheet or a database so that it can be used in various applications.

## Implementing web scraping in python using BeautifulSoup

*Beautiful Soup is a Python library that is used for web scraping purposes to pull the data out of HTML and XML files. It creates a parse tree from page source code that can be used to extract data in a hierarchical and more readable manner.*

## Steps to be followed
- Installing the required third-party libraries
- Request the content (source code) of a specific URL from the server
- Parsing the HTML content that is returned
- Identify the elements of the page that we want
- Extract and (if necessary) reformat those elements into a dataset we can analyze or use in whatever way we require.

### Installing the required third-party libraries
```
pip install requests
pip install bs4
pip install pandas
```
### Requesting content of a specific URL
```
import requests
URL = "https://www.xyz/lmn/"
response = requests.get(URL)
print(response.content)
```
### Parsing the HTML content
```
from bs4 import BeautifulSoup

htmlcontent=response.content

soup = BeautifulSoup(htmlcontent, 'html.parser')
print(soup.prettify())
```
### Identify the elements of the page that we desire
```
products=[]
prices=[]
ratings=[]

for i in soup.findAll('a',href=True,attrs={'class':'_1fQZEK'}):
    product=i.find('div',attrs={'class':'_4rR01T'})
    price=i.find('div',attrs={'class':'_30jeq3 _1_WHN1'})
    rating=i.find('div',attrs={'class':'_3LWZlK'})
        
    products.append(product.text)
    prices.append(price.text)
    ratings.append(rating.text)
```
### creating a dataframe from the extracted data
```
df=pd.DataFrame({'Product Name':products,'Price':prices,'Rating':ratings})
```
### Then, the extracted data can be exported into a csv file using the 'pandas' library in Python.
```
df.to_csv('laptops.csv')
```
