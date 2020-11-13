# PythonLiveProject
For two weeks my Team Mates and I worked on creating  Apps with Django.We each were responsible for our own Applications so I focused my time on building an App where you could store and update characters for your D and D campagin. I also utilized Beautiful Soup for web scrapping to link relevant articles. Below is an overview of what I accomplished over the project.
# [HOME](https://github.com/Driventobraise/PythonLiveProject/blob/main/home2.png)| [CHARATERS](https://github.com/Driventobraise/PythonLiveProject/blob/main/add_character2.png)| [INDEX](https://github.com/Driventobraise/PythonLiveProject/blob/main/indexpg2.png)| [ARTICLES](https://github.com/Driventobraise/PythonLiveProject/blob/main/webscraperpg2.png)
Above are links to the app lay ouy. I utilized bootstrap and basic css for styling, in the future I would like to refine my look for the app.
# Starting my app and setting up the base model:
For Story 1 I set up the basic structure for my app creating templates with Django. I utilized Django templating language to maintain a constant style throught the project. I had to use [url paths](https://github.com/Driventobraise/PythonLiveProject/blob/main/urlpatterns.png) and views based functions to render the different pages of the application.
* Views Function for rendering Home page and Character page
```

# Home Page
def d_and_d_home(request):
    return render(request, 'DandDApp/DandD_home.html')


# ADD- adds character to DB
def add_character(request):
    form = CreateCharacterForm(data=request.POST or None)
    if form.is_valid():
        form.save()
        return redirect('d_and_d_home')
    else:
        print(form.errors)
        form = CreateCharacterForm()
    context = {'form': form}
    return render(request, 'DandDApp/Add_Character.html', context)


# Index--Shows all entries in DB
def d_and_d_index(request):
    form = CreateCharacterForm()
    characters = CreateCharacter.object.all()
    paginator = Paginator(characters, 5)
    page_number = request.GET.get('page')
    page_obj = paginator.get_page(page_number)
    context = {'form': form, 'characters': characters}
    return render(request, 'DandDApp/DandD_index.html', {'page_obj': page_obj}, context)
    
```
# Implementing crud functionalities:
In story 2 I created [The Data Base Model](https://github.com/Driventobraise/PythonLiveProject/blob/main/DBmodel.png) and added the ability to create a [character](https://github.com/Driventobraise/PythonLiveProject/blob/main/views1.png) in the database. For story 3 I created an [Index page](https://github.com/Driventobraise/PythonLiveProject/blob/main/index.png) to display all characters entered into the database. I used the inbuilt django paginator class to create pagination for viewing the database entries. In Story 4 I added the functionality to [inspect](https://github.com/Driventobraise/PythonLiveProject/blob/main/detailspage.png) each entery. In Story 5 I added the ability to [edit](https://github.com/Driventobraise/PythonLiveProject/blob/main/editpage.png) and [delete](https://github.com/Driventobraise/PythonLiveProject/blob/main/views2.png) any database entery. Durning these steps I was using sqlite db and django queries to interact with the DB.
# Beautiful Soup:
During story 6 and 7 I utilized a [web scraper](https://github.com/Driventobraise/PythonLiveProject/blob/main/views4.png) to pull article summarys and their authors from dnd.wizards.com and rendered it on my articles page. In the future I would like to add direct links to the full articles and display the images attached to the articles.

* Template for receiving web-scrapping
```
{% extends "DandDApp/DandD_base.html" %}
{% load static %}
{% block title %}D&D | Articles{% endblock%}

{% block header %}Check out the latest stories!{% endblock %}


{% block content %}
<table class="table" >
      <thead class="index_display">
        <tr>
          <th scope="col">Author:</th>
          <th scope="col">Summary:</th>
        </tr>
      </thead>
      <tbody class="index_display">
      <!--Loop through article/author list-->
      {% for item in articleList %}
        <tr>
          <td>{{ item.Author }}</td>
          <td>{{ item.Summary }}</td>
       {% endfor %}
        </tr>

      </tbody>
    </table>
{% endblock %}

```
# Skills Learned
* Learned VCS through Azure DevOps.
* A deeper more meaningful understanding of Django.
* How to utilize web-scraping.
* Keeping up with a work load while working remotely.
