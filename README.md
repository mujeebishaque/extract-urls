# extract-urls
collect all the URLs from the given link


```python

import requests
from bs4 import BeautifulSoup

if __name__ == '__main__':
    
    user_input_url = input("Input URL: ")
    
    if not user_input_url or len(user_input_url) < 1:
        raise Exception("INFO: Invalid Input")

    _start = user_input_url.find('//')
    _end   = user_input_url.find('.com')

    readable_website_name = user_input_url[_start+2:_end].strip()
    
    try:
        website_content = requests.get(user_input_url.strip()).text
    except:
        check_internet = requests.get('https://google.com').status_code
        
        if check_internet != requests.codes.ok:
            raise ConnectionError("ERROR: Check internet connection.")
    
    _soup = BeautifulSoup(website_content, features='lxml')
    
    internal_url_links = []
    external_url_links = []
    
    for link in _soup.find_all('a', href=True):
        if readable_website_name in link.get('href'):
            internal_url_links.append(link['href'])
        
        if readable_website_name not in link.get('href') and len(link.get('href')) > 3:
            external_url_links.append(link['href'])
    
    print(internal_url_links, '\n')
    print(external_url_links, '\n')

```

Above code is the same as in the file. It's for quick copy-pasting. As you can see you can get both internal web links and external links from the code. 

Open to further contributions. 
