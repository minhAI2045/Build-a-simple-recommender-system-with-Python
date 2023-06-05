
The first thing we need to do is install `beautifulsoup` with the following command:

        pip3 install beautifulsoup4
Beautiful Soup is a library that makes it easy to get information from Web pages.

Next, we install the requests module:

        pip3 install requests
The requests module allows you to send HTTP/1.1 requests extremely easily. There's no need to manually add query strings to the URL.

And finally, the webbrowser module in Python is also used but we won't need to install it. It is part of the standard library in python.
# 1 
The first thing to do is to import the necessary modules to build the program.
```
import requests
from bs4 import BeautifulSoup
import webbrowser

```

# 2 
Next, the while loop with the condition always True is used to repeat continuously to make recommendations about the articles that the user wants to see.

Inside this while loop,

1. We execute the command `url = requests.get("https://dantri.com.vn") `to get the path of the dantri site.

2. `soup = BeautifulSoup(url.content, "html.parser")` is used to get content on dantri homepage with articles.

3. We perform a search for all title names of the article and save it in the title variable with the following statement:
    ```titles = soup.find_all(class_="article-title")```
4. Then we remove the leading and trailing spaces in the title of the article with the command:
    ```new_title = titles[count].text.strip()```
In the above code, I have used the `count `variable to cycle through each article on the homepage of the dantri site to give different articles to the user.
5. To access the article, we need to find the `a` tag containing the article's title content, note that this `a` tag is a child tag inside the tag containing the title of the article with the command:
    ```children = titles[count].findChildren("a" , recursive=False)
        find_a = children[0]['href']```
6. Next, we allow the user to enter the characters yes or no or 'y' and 'n' to see if the user wants to see the article. If the user wants to see that article, the user will enter the character 'y' and we will get the url of that article in the `href` attribute of the `a` tag that we have done the search above. save in the `find_a` variable, and finally open the web page containing the article the user wants to see.
    ```url = "https://dantri.com.vn/%s" % find_a
       webbrowser.open(url)```
If the user does not want to see this article, they can enter the character 'n' to have the program show another article they want to see. If the user does not enter any characters, we will print a message that they can only enter 'y' or 'n', i.e. whether or not they want to see the post.