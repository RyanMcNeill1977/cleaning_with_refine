

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



![Here's what you want.](../master/refine9.jpg)



OK, so these are the distinct entries from our employer_name column. First, notice you have a couple options on how to sort those entries. Try clicking on count. 



![Here's what you want.](../master/refine10.jpg)



Now your distinct entries are sorted by the number of times they appear. Take a look in the box at the two entries I've highlighted for the North Carolina Growers Association.



![Here's what you want.](../master/refine11.jpg)



Therein lies the No. 1 problem with this dataset. There's no standardization of employer names. If you were to use this field in a crosstab or SQL group by statement, you wouldn't get the right answer. That's where OpenRefine really sings. 

Click on Cluster.



![Here's what you want.](../master/refine12.jpg)



What happens now is OpenRefine uses some different methodologies to attempt to identify similar values. Right out of the chute, we see that Google Refine has recognized a number of different variations of the North Carolina Growers Association. 



![Here's what you want.](../master/refine13.jpg)



### Brief interlude

As you can see at the top of our cluster box, OpenRefine lets you choose the method and keying function. These are just different methodlogies for how OpenRefine attempts to cluster the values.

Below is the best explainer I've found on the topic and what I use for reference. It's a tipsheet from a NICAR session by Nils Mulvad and Rob Gebeloff. You can [see more here](https://github.com/gebelo/nicar2016/blob/master/refine.pdf).



![Here's what you want.](../master/refine14.jpg)

![Here's what you want.](../master/refine15.jpg)




### Back to cleaning 


If you hover your mouse over a particular group of results, a link will show up called "Browse this cluster." 



![Here's what you want.](../master/refine16.jpg)



Click on "Browse this cluter" for the North Carolina Growers Association. It'll return to the data window, but with a couple different things happening. 



![Here's what you want.](../master/refine17.jpg)



What's happening here is OpenRefine has highlighted all 54 rows it thinks should be turned into a single North Carolina Growers Association entry. This is an important step, in my opinion. It allows you to eyeball the data in its entirety before changing it. 

Why is this important?

Say we're looking at a company called Ryan's Refining Co. OpenRefine might think all Ryan Refining Co.-like entries are the same. Maybe they are. But to really know for sure, we might want to eyeball the city and state, or some other information. This allows you to do that. 

If you look in the employer_name box on the left, you'll see all the incarnations of North Carolina Growers Association are highlighted in orange. 



![Here's what you want.](../master/refine18.jpg)



If you didn't want one or more of those entries to be included, you could click exclude. 



![Here's what you want.](../master/refine19.jpg)



Now click on Cluster. 


Because we're OK with all the proposed changes, click the "Merge?" button. Then select "Merge Selected & Re-Cluster." 



![Here's what you want.](../master/refine20.jpg)



Once it is done, select "Close." 

Now lets cluster the column again. Then click on count to sort the column based on the number of records. Notice that North Carolina Growers Association Inc. now has 54 records?

Let's cluster again. 

Scroll down until you find the records that OpenRefine wants to turn into A and J Farms. 



![Here's what you want.](../master/refine21.jpg)



See a problem? What is it?

Let's click on "Browse this cluster" .... 

One of these things is not like the other. We can tell that two of them belong together, in part based on the city and state of the employer. A and J Farms LLC clearly doesn't belong with the others. 

Click on exclude. 



![Here's what you want.](../master/refine22.jpg)



Then hit Cluster again. Now everything looks how it should. 



![Here's what you want.](../master/refine23.jpg)

## Fine tuning your efforts

No matter what I'm using to clean data, whether it's SQL or OpenRefine, I try and concentrate on the most frequent records. Let's say we're planning to examine the top 10 law firms or employers. In that case, I'm going to try to focus on the entries that have a shot at being in the top 10. 

One way to do that is by using the slider in the Cluster & Edit screen. 


![Here's what you want.](../master/refine25.jpg)



Try adjusting the slider. See what happens?


## Exporting your data

![Here's what you want.](../master/refine24.jpg)

## Now you try

Take a look at the lawfirm_name field. Clean it up. Try different combinations of method and distance function while clustering. 

Which lawfirm name appears the most?




