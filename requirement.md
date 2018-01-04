# Theater Company Email Automation
You are asked to automate the process used by a theater company to communicate with its members. Every year the theater company holds a showing of the most popular play for its members. The company sends an email informing each member of the play and the dates. Complimentary tickets are then send using normal mail. The company has grown in the last few years and their manual process is becoming time consuming. They are asking you to help them automate the process.

The theater company has all the information of its members in a CSV file. CSV files are plain text files that contains information such that each piece of data is enclosed in double quotes and separated by a comma. The first line of the file contains the headers for each column.
```
"first_name" , "last_name" , "company_name" , "email"
"James"      , "Butt"      , "Benton"       , "504-845-1427"
"Josephine"  , "R, Darakjy", "Chanay"       , "810-374-9840"
"Art"        , "Venere"    , "Chemel"       , "856-264-4130"
```
For example, the preceding listing has 4 columns named  first_name, last_name,  company_name and email. And the second line has the information for member James Butt. Note that even though information is enclosed in double quotes and separated by comma, there are pieces of information that contains comma, e.g., "R, Darakjy" is one piece of information and not two.

Here is a sample that you can use with some of the theater company's members information theater-company-members.csv. The CSV file contains first and last name, company name, address, city, county, state, zip, phone1 and phone2, email address and web page URL.

Given this CSV file the theater company would like you to create a program that they can run on the command line that would take this file as input and generate, from templates, files that will contain the email messages and letters to send to their members.

The templates are stored as text files with special placeholders in the text that refer to the CSV file's header names. Here are two example templates, one for email and one for letters. Placeholders are placed between [[ and ]]
```
To:[[email]]
Subject:Information on this years members only show!

Dear [[first_name]] [[last_name]], 

   This year's members only theater show will showcase "A Streetcar
   Named Desire" directed by John Jarmush and Susan Mae at our New
   York location between March 1st and April 10th.  Your complementary
   tickets for the show are on their way through mail and should
   reach you within the next couple of days.

   Sincerely, 
```
So given the above email template and the following line from the CSV file
```
"first_name","last_name","company_name","address","city","county","state","zip","phone1","phone2","email"
"Art","Venere","Chemel, James L Cpa","8 W Cerritos Ave #54","Bridgeport","Gloucester","NJ","08014","856-636-8749","856-264-4130","art@venere.org","http://www.chemeljameslcpa.com"
```
The email message that gets generated is
```
To:art@venere.org
Subject:Information on this years members only show!

Dear Art Venere, 

   This year's members only theater show will showcase "A Streetcar
   Named Desire" directed by John Jarmush and Susan Mae at our New
   York location between March 1st and April 10th.  Your complementary
   tickets for the show are on their way through mail and should
   reach you within the next couple of days.

   Sincerely,        
```
Similarly we have a template for the letter
```
[[company_name]].
[[first_name]] [[last_name]]
[[address]], [[city]],
[[county]], [[state]], [[zip]]
([[email]])

Dear [[first_name]] [[last_name]], 

    Please find enclosed your complementary tickets to "A Streetcar
    Named Desire" directed by John Jarmush and Susan Mae. We look
    forward to seeing you at one of our showings at our New York
    theater between March 1st and April 10th.

Sincerely, 
```
Which will generate for the same CSV line we used before, the following text file.
```
Chemel, James L Cpa,
Art Venere
8 W Cerritos Ave #54, Bridgeport,
Gloucester, NJ, 08014.
(art@venere.org)

Dear Art Venere, 

    Please find enclosed your complementary tickets to "A Streetcar
    Named Desire" directed by John Jarmush and Susan Mae. We look
    forward to seeing you at one of our showings at our New York
    theater between March 1st and April 10th.

Sincerely,        
```
What is provided is one example of a CSV file and two examples of templates. Your code should work for any CSV file and any template that uses the CSV file's header values as placeholders.

The theater company would like to write more templates and your program should accommodate for new templates. Templates use the column names from the CSV file as the names to replace inside placeholders, like the examples provided here.

Your program needs to accept certain arguments at the command line.
```
        --email                  only generate email messages
        --email-template <file>  accepts a filename that holds the email template 

        --letter                 only generate letters
        --letter-template <file> accepts a filename that holds the email template 


        --output-dir <path>      accepts the name of a folder, all output is placed in this folder
        --csv-file <path>        accepts the name of the csv file to process
```
Some options take arguments, for example --email-template takes one argument and it is the name of a file, --output-dir takes one argument and it is the name of a folder. Other options take no arguments and indicate an action, i.e., --email indicates that we are to generate emails on this execution of the program.

The command line option --output-dir and csv-file are required. Your program should be able to generate one of the two options (emails or letters) per invocation. If --email is given then --email-template must also be provided, if  --letter is given then --letter-template must also be given. Calling your program and passing any other combination of options should generate an error, e.g. --email --letter-template 
                    letter-template.txt --output-dir letters/ is illegal.

When an illegal combination of inputs is provided by the user the program should exit with a helpful error message and a short explanation of how to use the program along with examples. For example passing
```
 --email --letter-template letter-template.txt --output-dir letters

 Error: --email provided but no --email-template was given. 

 Usage: 

        --email                  only generate email messages
        --email-template <file>  accepts a filename that holds the email template. Required if --email is used

        --letter                 only generate letters
        --letter-template <file> accepts a filename that holds the email template. Required if --letter is used

        --output-dir <path>      accepts the name of a folder, all output is placed in this folder

        --csv-file <path>        accepts the name of the csv file to process

Examples: 

       --email --email-template email-template.txt --output-dir emails --csv-file customer.csv
       --letter --letter-template letter-template.txt --output-dir letters --csv-file customer.csv

```
Also the order that the command line options are given does not matter, i.e. the following examples are valid
```
                  --email --email-template email-template.txt --output-dir emails --csv-file customer.csv
                  --csv-file customer.csv --email-template email-template.txt --output-dir emails --email      
                  --output-dir emails --email --csv-file customer.csv --email-template email-template.txt 
```
Design and implement the email and letter generator program for the theater group. Use theater-company-members.csv, email-template.txt and letter-template.txt to help you develop and test your code. You should also develop your own templates. Also make sure that your program works correctly regardless of how your operating system represents paths and files.