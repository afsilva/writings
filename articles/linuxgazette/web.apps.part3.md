Developing Web Applications - Part III LG #50 [![[ Table of Contents ]](../gx/indexnew.gif)](index.html) [![[ Front Page ]](../gx/homenew.gif)](../index.html) [![[ Prev ]](../gx/back2.gif)](rogers.html) [![[ Linux Gazette FAQ ]](./../gx/dennis/faq.gif)](../faq/index.html) [![[ Next ]](../gx/fwd.gif)](silva2.html)  

#### "Linux Gazette..._making Linux just a little more fun!_"

* * *

Developing Web Applications - Part III
======================================

#### By [Anderson Silva](/cdn-cgi/l/email-protection#2f4e495c4643594e6f43464d4a5d5b56014a4b5a)

* * *

  
At this time, I will close the **Developing Web Applications** series with a very helpful example that if you understand it, you will be able to apply the same type of application to several other types of online applications. I am talking about **creating your own online bookmark**. Once you understand this example, you will be able to do basic **mySQL** operations with php3.

But before I get to the php3 code for the bookmark application, you will need to create a mysql table to store your bookmarks. There are several ways to administrate mySQL databases:

*   Command Line: You can create all your tables, insert data, and query them out from the mysql client. To do this, I would suggest you read the mySQL Language reference at [http://www.mysql.com](https://www.mysql.com)
*   GUI Based: You can download several different types of graphical interface to administrator a mysql database. For example: xmysql and kmysql. To download this tools, I would suggest: [http://www.tuxfinder.com](http://www.tuxfinder.com)
*   Online Interface: This is definitely my favorite option. There is a very nice tool called  phpMyAdmin, which allows you to administrate one or more mySQL database remotely through your browser. Here is the URL: [http://www.phpwizard.net/phpMyAdmin](http://www.phpwizard.net/phpMyAdmin)

Choose whatever fits you better. For this small project, I will give you the configuration that fits the needs for this application.

    Database Host: **myserver**  
    Username: **myusername**  
   Password: **mypassword**  
   Database Name:  **mydatabase**  
   Table Name: **bookmark**  
    Fields in the **bookmark** table:  **id, url, description**

All the information above is relevant when coding the application. **Note:** The fields are the columns on the database. The id was defined to allow every entry in your database to be unique (**primary key**), it should be defined to be unique, and auto-increment.

Once you have your database defined and working, you may start coding your application, and here is how it goes:  
 

The HTML form that will capture the data and send it in to the database: \[[text copy of this listing](misc/silva/book_form.html.txt)\]

    <HTML>
    <head>
    <title>Anderson's bookmark</title>
    </head>
    <body bgcolor=white>
    <form ACTION="sendbook.php3" METHOD="Post">
          <center><p>Enter The Bookmark Title:</font>

          <input TYPE="text" SIZE="40" NAME="description"> </p>

          <center><p>Enter The Bookmark URL:</font>

          <input TYPE="text" SIZE="40" NAME="URL"> </p></center>

          <p><input TYPE="Submit" VALUE="Check"><br>
     </form>
    <a href="book.php3">View Bookmarks</a>
    </body>
    </html>

The above form will have to text fields: one for the URL, the other for the URL description. The **form** tag will be responsable for telling the browser what to do when the **Submit** button is pressed. In this case it will call the php3 script **sendbook.php3**, and send the data to that script.

The following script is the **sendbook.php3**. This script will open a connection to the mySQL database, and send the data from the HTML form to the database. \[[text copy](misc/silva/sendbook.php3.txt)\]

         <?php
           //if any of the two fields is left blank, don't send data, but send an error message.
           if(!($description=="") || !($URL==""))
           {
 
              //connects to database  server
              mysql\_connect(myserver, myusername, mypassword);
 
              //connects to the database
              mysql\_select\_db('mydatabase');
 
              //this is the query command to insert into the bookmark 
              // table the values from $description and $URL
              // inside the Columns description and URL
              mysql\_query("insert into bookmark(description, URL) values ('$description', '$URL')");
 
              //closes connection to database.
              mysql\_close();
 
              //After the data is inserted, the browser will form a web page with 
              // the following information.
              echo "Thanks for adding the bookmark<br>";
              echo "<a href=book.php3>View BookMraks</a><br>";
              echo "<a href=sendbook.html>Add Another One</a><br>";
            }else{
              echo "You need to go to the form: <a href=sendbook.html>Sendbook</a>";
            }
         ?>

The third and last script is called **book.php3**. This script will query the data entered by sendbook.php3, and display on the screen all of your bookmarks. \[[text copy](misc/silva/book.php3.txt)\]

    <?     echo "<HTML>";
           echo "<HEAD><TITLE>Afsilva's Bookmark</title></head>";
           echo "<body bgcolor=white>";
           echo "<IMG SRC=bookmark.jpg><br><br>";

                //Connect to DB server
                mysql\_connect(myserver, myusername, mypasword);
                //Connect to Database
                mysql\_select\_db("mydatabase");
                //Query the database for everything(\*) that is on it.
                $result = mysql\_query("SELECT \* FROM bookmark");

                //mysql\_num\_rows() returns the number of bookmarks found.
                $rows = mysql\_num\_rows($result);
                echo "Number of bookmarks:";
                //outputs the number of records (rows)
                echo $rows;
                echo "<br><br>";
                $i=0;
                echo "<a href=sendbook.html>Insert More BookMarks</a>\\n<br><br>";
                echo "<table border=1>";

                //This allows you to access the query in a form of an array.
                //The array index is the name of the field of the database.
                while ($row = mysql\_fetch\_array($result))
                {
                      echo "<tr><td>\\n";
                      // The . operator adds string together.
                      echo "<a href=".$row\["URL"\].">".$row\["description"\]."</a>\\n";
                      echo "</td></tr>";
                }
                echo"</table>";
                mysql\_close();
                echo"<a href=../index.html target=\_top>";
                echo "</HTML>";
      ?>

With these three files you should be able to get your first bookmark application working, but just don't stop there. Work upon it, and make your bookmark better, and smarter. From this example, you should be able to build several other types of online utilities, like: guestbooks, counters, surveys, etc.

I hope that this article was useful, and taught you something new. Feel free to email me at: [\[email protected\]](/cdn-cgi/l/email-protection#660700150f0a1007260a0f040314121f48030213), and send me your comments and questions.

* * *

##### Copyright © 2000, Anderson Silva  
Published in Issue 50 of _Linux Gazette_, February 2000

* * *

[![[ Table of Contents ]](../gx/indexnew.gif)](index.html) [![[ Front Page ]](../gx/homenew.gif)](../index.html) [![[ Prev ]](../gx/back2.gif)](rogers.html) [![[ Linux Gazette FAQ ]](./../gx/dennis/faq.gif)](../faq/index.html) [![[ Next ]](../gx/fwd.gif)](silva2.html)
