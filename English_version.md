Engeto: Project 3
===
The third project at the online python academy by Enget.

Description of assignment
---
This project is used to extract the results of the parliamentary elections in 2017. You can find a link to view here.

Installing libraries
---
The libraries that are used in the code are stored in the requirements.txt file. For installation, I recommend using a new virtual environment and running as follows with the installed manager.

```python
$ pip3 --version # verify manager version
$ pip3 install -r requirements.txt # install libraries
```
Starting a project
Running the ```.election-scraper.py```. file from the command line requires 2 required arguments.

```.python election_scraper <referential-file> <result-file>```.
Then the results will be downloaded as a ```..csv```. file.

Sample project
---
Voting results for district Prostějov:

argument: https://volby.cz/pls/ps2017nss/ps32?xjazyk=CZ&xkraj=12&xnumnuts=7103
argument: vysledky_prostejov.csv
Starting the program:

```.python election-scraper.py "https://volby.cz/pls/ps2017nss/ps32?xjazyk=CZ&xkraj=12&xnumnuts=7103" "vysledky_prostejov.csv"```.
Download progress:
```
DOWNLOAD DATA FROM SELECTED URL: https://volby.cz/pls/ps2017nss/ps32?xjazyk=CZ&xkraj=12&xnumnuts=7103
I SAVE TO FILE: vysledky_prostejov.csv
END election-scraper
```

Partial output:
```
Code, City, Registered, Envelopes, ...
506761, Alojzov, 205,145,144,29,0,0,9,0,5,17,4,1,1,0,0,18,0,5,32,0,0,6,0,0,1, 1.15.0
589268, Bedihošť, 834,527,524,51,0,0,28,1,13,123,2,2,14,1,0,34,0,6,140,0,0,26,0,0,0,0,82, 1
589276, Bílovice-Lutotín, 279,279,275,13,0,0,32,0,8,40,1,0,4,0,0,30,0,3,83,0,0,22,0,0, 0,1,38,0
```

Program description
---
At the beginning of the program, it is necessary to import the libraries that we will work with in the program.

line 6 - line 18 - Assigning elements. 
We assign elements of classes to variables, from where we will take both output data and data that we will need in our program.

line 185 - We check the order of the arguments. 
If the user has entered the wrong number of arguments, or the arguments in the wrong order, then the program notifies him and ends.

line 195 - Request HTML code. 
Otherwise, we will ask the user for the HTML code from the specified website. The ```get_html(arg)``` function will take care of this.

line 196 - We download cities, city codes and links. 
Once we have successfully obtained the HTML structure of our website, we can begin crawling it for a cycle. 
Our goal will be to find all city names, codes of individual cities, but also links that are hidden under X. We will find all this data using the variables we
have just declared from line 6 to line 18. Under these elements, this data is hidden. After finding the mentioned data, we save them in sheets 
with the names codes, cities and links. We can leave the first two sheets for a while, but we will need the links in a moment. 
This piece of code is hidden in the get_first_columns function.

line 197 - We are downloading other data. 
We call the function ```get_second_data(arg)```. We will now start downloading the other data. We can find it just under the hidden links that we downloaded a while ago. 
However, the links we found are incomplete because everyone is missing the main part. On line 6 we could notice the variable ```MAIN_URL```, in which the main part of 
the link is currently stored. After linking this variable to each part of the link in the links list, we get to the page from where we will take the other data. 
Our links in the links list are divided into 2 groups, because some municipalities are divided into several smaller districts. This means that for some links we do not 
click on the page from which we want to take the required data, but on the page where the village is divided into these smaller districts. For us, this means that we 
have to take an intermediate step. This intermediate step is located at line 157 - line 160. First we will ask for the HTML structure of the code of this “intermediate page.” 
Then we will find all the links under which our required data is hidden. The summation of values is divided into upper and lower data, taken care of by the 
```sum_header_data``` and ```sum_party_numbers``` functions, all of which are stored in worksheets that we will need when saving to the ```.csv```. file. 
The ```.get_cand_parties(arg)```. function will get us to get these pages.

line 21 - we save to a .csv file. 
Now we have all the data downloaded and we can start saving it to ```..csv```.. The first line will contain the header (line 18) and the candidate parties. 
The next lines will be filled in gradually using the for loop and the writerow method from line 26 - line 31.
