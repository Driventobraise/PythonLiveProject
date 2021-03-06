# Dungeons and Dragons App
For two weeks my teammates and I worked on creating  Apps with Django. On this full stack project we each were responsible for our own applications, so I focused my time on building an App where you could store and update characters for your Dungeons and Dragons campaign. I also utilized Beautiful Soup for web scraping to link relevant articles. Below is an overview of what I accomplished over the project.
# [HOME](https://github.com/Driventobraise/PythonLiveProject/blob/main/home2.png)| [CHARACTERS](https://github.com/Driventobraise/PythonLiveProject/blob/main/add_character3.png)| [INDEX](https://github.com/Driventobraise/PythonLiveProject/blob/main/indexpg2.png)| [ARTICLES](https://github.com/Driventobraise/PythonLiveProject/blob/main/webscraperpg2.png)
Above are links to the app layout. I utilized bootstrap and basic css for styling, in the future I would like to refine my look for the app.
# Starting my app :
For Story 1 I set up the basic structure for my app creating templates with Django. I utilized Django template inheritance to maintain a constant style throughout the project. I created a base template that I extended on all the pages of my app. I had to use [url paths](https://github.com/Driventobraise/PythonLiveProject/blob/main/urlpatterns.png) and views based functions to render the different pages of the application.
* Base HTML Template that my other pages inherited.
```

{% load staticfiles %}

<!DOCTYPE html>
<html lang="en" class="bg_img">
    <head>
        <meta charset="UTF-8">
        <title>{% block title %}Dungeons and Dragons App{% endblock %}</title>
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <!-- Bootstrap css links -->
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
        <link rel="stylesheet" type="text/css" href="{% static '/css/DandD.css' %}">
        <link href="//fonts.googleapis.com/css?family=Playball" rel="stylesheet" type="text/css">
    </head>

    <body>
        <div class="homeimage">
            {% include './DandD_navbar.html' %}
            <div class="title">
                <h1>{% block header %}{% endblock %}</h1>
            </div>
            {% block content %}{% endblock %}
        </div>
            {% include './DandD_footer.html' %}

        <!-- Bootstrap javascript links -->
        <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN"      crossorigin="anonymous"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.9/umd/popper.min.js" integrity="sha384ApNbgh9B+Y1QKtv3Rn7W3mgPxhU9K/ScQsAP7hUibX39j7fakFPskvXusvfa0b4Q" crossorigin="anonymous"></script>
        <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl"    crossorigin="anonymous"></script>
    </body>
</html>
    
```
# Implementing CRUD (create, read, update- delete) functionalities :
* ## Create :
In story 2 I created [The Data Base Model](https://github.com/Driventobraise/PythonLiveProject/blob/main/DBmodel.png) and added a views function that rendered the create Character  page. I then added the ability to create a [character](https://github.com/Driventobraise/PythonLiveProject/blob/main/views1.png) and save it in the database .  
* ## Read :
For story 3 I created an [Index page](https://github.com/Driventobraise/PythonLiveProject/blob/main/index.png) to display all characters entered into the database. I used the inbuilt django paginator class to create pagination for viewing the database entries. In Story 4 I added the functionality to [read](https://github.com/Driventobraise/PythonLiveProject/blob/main/detailspage.png) each entery by using a views function that finds the single desired instance from the database and sending it to the details template.
* ## Update - Delete :
In Story 5 I added the ability to [edit](https://github.com/Driventobraise/PythonLiveProject/blob/main/editpage.png) and [delete](https://github.com/Driventobraise/PythonLiveProject/blob/main/views2.png) any database entry. During this project I was using sqlite db and django queries to interact with the database.

<img src="https://github.com/Driventobraise/PythonLiveProject/blob/main/edited_delete2.png">

# Beautiful Soup :
During story 6 and 7 I utilized a [web scraper](https://github.com/Driventobraise/PythonLiveProject/blob/main/views4.png) to pull article summaries and their authors from dnd.wizards.com and rendered it on my articles page. In the future I would like to add direct links to the full articles and display the images attached to the articles.

* views function for web-scrapping
```
# Article -- uses beautiful soup to parse page for article summaries and authors.
def d_and_d_article(request):
    page = requests.get("https://dnd.wizards.com/articles")
    soup = BeautifulSoup(page.content, 'html.parser')
    articles = soup.find_all('div', class_='content')
    articleList = []
    for item in articles:
        Author = item.find(class_='author')
        if Author is not None:
            # prints authors name to console
            print(Author.find('a').text)
            # .text is calling on the beautiful soup property to pull text
            AuthorRefined = Author.find('a').text
            Summary = item.find(class_='summary').text
            artsum = {"Author": AuthorRefined, "Summary": Summary}

            articleList.append(artsum)
    # prints article author and summary to console 
    print(articleList)

    return render(request, 'DandDApp/DandD_soup.html', {'articleList': articleList})

```
# Skills Learned :
* Learned VCS through Azure DevOps and Git.
* A deeper more meaningful understanding of Django.
* learning to use technologies new to me like web scraping.
* Keeping up with a work load while working remotely.
* learning to investigate errors and solve them.
