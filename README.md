## BlogApp

### Install Java
* sudo apt-get install openjdk-8-jdk

###Setup Tomcat server to deploy application
* sudo apt-get install tomcat7

###Install Maven - used for building project
* sudo apt-get install maven 

### Install Mysql Server
* sudo apt-get install mysql-server

###Deploy project 
* Go to current project directory
* mvn clean install //build the project
* sudo cp target/BlogApp.war /var/lib/tomcat7/webapps/.
* sudo service tomcat7 restart //restart the server after code ddeploment

###Dump database in mysql
* Install Mysql dump data in mysql
Mysql -uroot -p < blog_db.sql

###Get list of blogs:- 
 * Start<Optional Parameter> - Default value 0 - start offset of result
 * NoOfBlogs<optional parameter>- default value is 5 per page.

**Request:**
http://localhost:8080/BlogApp/blogs?start=22&noOfBlogs=3

**Response**

```[
  {
    "id": 23,
    "title": "Lorem Ipsum",
    "created": "2016-12-05",
    "paragraphs": null,
    "authors": null,
    "tags": null,
    "deleted": false
  },
  {
    "id": 24,
    "title": "Lorem Ipsum",
    "created": "2016-12-05",
    "paragraphs": null,
    "authors": null,
    "tags": null,
    "deleted": false
  },
  {
    "id": 25,
    "title": "Lorem Ipsum Part II",
    "created": "2016-12-05",
    "paragraphs": null,
    "authors": null,
    "tags": null,
    "deleted": false
  }
]
```

###Get Blog by Id:

**Request**
http://localhost:8080/BlogApp/blog/24/

**Response**
```
{
  "id": 24,
  "title": "Lorem Ipsum",
  "created": "2016-12-05",
  "paragraphs": [
    {
      "id": 46,
      "paragraphText": "Quisque varius iaculis dapibus. Praesent vel ultrices arcu, a porta magna. Nullam tristique justo nec massa tincidunt sodales. In consectetur enim vel finibus dignissim. Suspendisse vitae lacus nunc. Aliquam at odio vel dolor feugiat dignissim. Vestibulum a sem hendrerit magna pulvinar rutrum eu nec eros. Curabitur rhoncus dignissim velit, ut rhoncus lacus. Nulla nunc diam, scelerisque vel enim nec, semper tristique ipsum. Curabitur dictum augue risus. Aliquam at bibendum lorem.",
      "comments": [],
      "deleted": false
    },
    {
      "id": 47,
      "paragraphText": "Praesent condimentum semper lacinia. Vivamus fermentum cursus ante. Sed accumsan semper convallis. Vivamus interdum felis vel augue feugiat mollis. Nulla facilisi. Sed libero dolor, rhoncus sed elit a, semper gravida dui. Donec sem sem, molestie sed ullamcorper at, mattis mollis tortor. Etiam malesuada lectus rutrum elit lacinia dapibus. Suspendisse ac sapien scelerisque, cursus orci id, rutrum odio. Aliquam eros urna, placerat at enim vitae, ultrices elementum nulla. Nunc at ex at tellus elementum vestibulum ac id ipsum. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Integer tincidunt nibh porttitor, eleifend turpis nec, suscipit sapien. Vivamus posuere dolor a laoreet ornare.",
      "comments": [
        {
          "id": 15,
          "commentText": "Generated 5 paragraphs",
          "created": "2016-12-05",
          "deleted": false
        },
        {
          "id": 16,
          "commentText": " 449 words",
          "created": "2016-12-05",
          "deleted": false
        },
        {
          "id": 17,
          "commentText": " 3063 bytes of Lorem Ipsum",
          "created": "2016-12-05",
          "deleted": false
        }
      ],
      "deleted": false
    }
  ],
  "authors": null,
  "tags": null,
  "deleted": false
}
```

###Add Blog:-
http://localhost:8080/BlogApp/addBlog/

**Request Body:-**
* title:- title of the blog
* content:- Paragraphs and comment of the blogs.
* All the paragraphs are separated by \n\n and comments on paragraph are separated by "^^".

```
{
"content":"Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum^^What is Lorem Ipsum?\n\nThere are many variations of passages of Lorem Ipsum available, but the majority have suffered alteration in some form, by injected humour, or randomised words which don't look even slightly believable. If you are going to use a passage of Lorem Ipsum, you need to be sure there isn't anything embarrassing hidden in the middle of text. All the Lorem Ipsum generators on the Internet tend to repeat predefined chunks as necessary, making this the first true generator on the Internet. It uses a dictionary of over 200 Latin words, combined with a handful of model sentence structures, to generate Lorem Ipsum which looks reasonable. The generated Lorem Ipsum is therefore always free from repetition, injected humour, or non-characteristic words etc.^^Where can I get some?",
"title":"Lorem Ipsum"
}
```

**Successresponse:-(Return created object)**

```
{
  "id": 22,
  "title": "Lorem Ipsum",
  "created": 1480954768985,
  "paragraphs": [
    {
      "id": 42,
      "paragraphText": "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum",
      "comments": [
        {
          "id": 0,
          "commentText": "What is Lorem Ipsum?",
          "created": 1480954769355,
          "deleted": false
        }
      ],
      "deleted": false
    },
    {
      "id": 43,
      "paragraphText": "There are many variations of passages of Lorem Ipsum available, but the majority have suffered alteration in some form, by injected humour, or randomised words which don't look even slightly believable. If you are going to use a passage of Lorem Ipsum, you need to be sure there isn't anything embarrassing hidden in the middle of text. All the Lorem Ipsum generators on the Internet tend to repeat predefined chunks as necessary, making this the first true generator on the Internet. It uses a dictionary of over 200 Latin words, combined with a handful of model sentence structures, to generate Lorem Ipsum which looks reasonable. The generated Lorem Ipsum is therefore always free from repetition, injected humour, or non-characteristic words etc.",
      "comments": [
        {
          "id": 0,
          "commentText": "Where can I get some?",
          "created": 1480954769399,
          "deleted": false
        }
      ],
      "deleted": false
    }
  ],
  "authors": null,
  "tags": null,
  "deleted": false
}
```


