

## Installing Refine

It's really easy. Go to the [OpenRefine website](http://openrefine.org/download.html) and download the package that matches your operating system.

Download and extract the contents of the archive. Then navigate to the folder holding the files you just extracted. Click on openrefine.exe. 

OpenRefine then opens up a terminal window and begins setting up a mini little web server. Once it has finished, point your browser to either 127.0.0.1:3333 or localhost:3333. 

If it worked correctly, you should see something that looks like this. 


![Here's what you want.](../master/refine1.jpg)

## Importing your data 

OK, we're ready to import our data. 

Today we're going to be working with data from the U.S. Department of Labor's Office of Foreign Labor Certification. I worked on a few stories that used this data, including one illustrating Trump companies' use of guest worker programs.

The applicatinon process for the H2A and H2B process first requires firms to ask the DOL for permission to import workers. DOL approves or denies those applications. If the application is approved, DOL also approves the number of guest workers the company wants to bring in. The results of that step are in this dataset. 

*Important caveat: These numbers are not neccessarily the number of workers actually imported by the company. Think of it like a maximum.*

So let's go to [this DOL website](https://www.foreignlaborcert.doleta.gov/performancedata.cfm) and download the 2016 disclosure file for the H2A program. 


![Here's what you want.](../master/refine3.jpg)

Go to the Google Refine tab in your browser. Click on Choose Files. 


![Here's what you want.](../master/refine2.jpg)

Navigate to the H2A data you just downloaded. Click next. OpenRefine will inspect your data and give you a preview of the data. 

First, inspect your data in the preview window. Does it look correct? Are there any problems? At the bottom, OpenRefine gives you a few options on what exactly to import.

At important one you might want to remember: 

Ignore first --- this woud be useful if you have a bunch of junk at the top of your page that you don't want OpenRefine to import. 


![Here's what you want.](../master/refine4.jpg)


If everything is how you wanted, click on "Create Project." 


![Here's what you want.](../master/refine5.jpg)


OpenRefine will think for a minute and then spit out a new screen. 


![Here's what you want.](../master/refine6.jpg)


Now we can get to work. The main thing people want to do with this data typically involves figuring out how many guest workers a company sought. But that's problematic. Let's take a look and see why. 

On the employer_name tab, click on the little down arrow, then choose facet and then text facet. 


![Here's what you want.](../master/refine7.jpg)


Now you're probably going to get something that looks like this. 


![Here's what you want.](../master/refine8.jpg)


What we have to do is tell OpenRefine it is OK to work with more records than its default limit. Click on "Set choice count limit." OpenRefine will make a guess that's higher than the count of our records. Perfect. Click OK. 




