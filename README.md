# A Data Analysis of USDA (U.S. Department of Agriculture) Data on the per capita availability, importation and exportation (and other findings) of _corn sweeteners_

*Note: For the purposes of this data analysis, the term "corn sweeteners" includes the following: High Fructose Corn Syrup (HFCS), dextrose, and glucose.*

Jenny (Jennifer) Kwon · Final project for Professor Jeremy Rue's J124 (Introduction to Data Journalism) @ U.C. Berkeley's School of Journalism

### So, uh, why choose USDA data on *corn sweeteners*? 

As an American, I consider myself lucky that I had a Korean mom who stopped me from consuming a ton of junk food as a kid. (I still have a sweet tooth, though.)

(Sorry, Mom.)

I always thought she was just being unfair when she would snatch the Skittles out of my hand that I had nabbed during trick-or-treat or Halloween events, telling me that I shouldn't eat sweets like these because it was "bad for me."

She wasn't wrong. One particular ingredient she probably was talking about was high fructose corn syrup (HFCS), a type of *corn sweetener* that causes ["weight gain, type 2 diabetes, metabolic syndrome and high triglyceride levels,"](https://www.mayoclinic.org/healthy-lifestyle/nutrition-and-healthy-eating/expert-answers/high-fructose-corn-syrup/faq-20058201 "Link to MayoClinic website") effects that raise the risk of getting heart disease.

In the U.S., heart disease is the *number one* ["leading cause of death for men, women, and people of most racial and ethnic groups in the United States."](https://www.cdc.gov/heartdisease/facts.htm#:~:text=Heart%20disease%20is%20the%20leading,1%20in%20every%204%20deaths.) 

HFCS is found in several kinds of food (yeah, not just Halloween candY) that we find ourselves eating *daily*:

* yogurt (sweetened)
* salad dressing
* certain kinds of breads 
* canned fruits
* juice 
* boxed dinners
* granola bars
* cereal 
* sauces/condiments
* coffee creamer
* energy/sports drinks 
* ice-cream (I know, real bummer)

A non-comprehensive list can be found on [this Healthline article](https://www.healthline.com/nutrition/20-foods-with-high-fructose-corn-syrup#section20).

Of course, HFCS isn't the *only* kind of corn sweetener there is, but it has a particular bad reputation among healthcare professionals and conscious consumers watching out for their health.

That being said, other substances categorized by the USDA as a "corn sweetener" like dextrose and glucose also have negative health effects when not consumed in moderation.

Which raised questions I was curious about: *_Was the amount of corn sweetener the U.S. was producing, importing, exporting, etc. being tracked? How much corn sweetener is made in comparison to population?_*

The answer to the first question was yes, which brings us here to this mini data cleaning & analysis project today. 

## Getting and cleaning/refining the data

*Note for @Jrue: The tool **Open Refine** corrupted on my computer - the macOS system wouldn't let me use this tool because it blocked all "malware" apps and I didn't find a workaround in time, unfortunately. I was limited to Google Sheets for cleanup because my data wasn't **messy** enough or only in pdf form to use a tool like **Tabula**. Thank you for your understanding!*

Finding the data on USDA's website on corn sweeteners actually wasn't too hard. The department has the data on a page titled ["Sugar and Sweeteners Yearbook Tables"](https://www.ers.usda.gov/data-products/sugar-and-sweeteners-yearbook-tables/).

!!!! ATTACH IMAGE OF USDA PAGE WITH CORN SWEETENER DATA !!!!

The exact dataset I chose was titled "Corn Sweetener Supply, Use, and Trade."

When I loaded the dataset onto Google Sheets, I saw this introduction to the dataset:

!!!! ATTACH IMAGE OF USDA INTRO !!!!

I decided after looking at data on "Caloric sweeteners, per capita availability, 1966-2017" and the supply and use of glucose, dextrose, HCFS, and corn sweeteners as a whole in comparison with the U.S. population per year, each different corn sweetener with its own data on separate tab sheets, to **combine** these sheets.

I had to first modify the sheets so that if I created charts or pivot tables from this data that Google Sheets would be able to *read* this data in the first place.

The USDA data was fairly cleaned already but the headings were merged to be aesthetically pleasing (which wouldn't work for data analysis) and also vague. 

!!! ATTACH IMAGE OF UNUSABLE DATA !!!!

After cleaning the headings, the data looked something like this.

!!! ATTACH IMAGE OF BEFORE MERGING !!!!

I wanted to merge more data, however, so the final datasheet I was working with looked more like this:

!!! ATTACH IMAGE OF MERGED DATA 1 !!!!

!!! ATTACH IMAGE OF MERGED DATA 2 !!!!

The way I made my unique merged dataset was by taking columns from the original datasheets and merging them onto a new spreadsheet copied from the "per capita" data, because that was originally the dataseet I was most curious about analyzing. 

!!! ATTACH IMAGE OF dextroseorig_usedcolshighlighted !!!!

The image above is for **dextrose** specifically, but I repeated this same process of copying and pasting particular columns I was interested in investigating (**production, imports, and exports**) for **hcfs, glucose, and dextrose** as well. This information wasn't available for **refined and raw cane and beet sugar or other substances like edible syrups and honey, which were labeled as sweeteners,** which is why I decided to focus on **corn sweeteners** specifically and delete the extra columns related to non-corn sweetener substances (which I highlighted in red). 

##### Issues

I noticed *__two major problems__* right off the bat after I went through this merging process.

1. The unit for "per capita availability" was in **pounds, dry weight.** The unit for "exports," "imports," and "production," however, were in **1000 short tons.**

Solution? A simple unit conversion, done easily through Google Sheets. 

I created a new column with the same column name I was going to convert (i.e. I took the "Total Imports (HFCS) in 1000 short tons" and created a new column beside it titled "Total Imports (HFCS) in pounds." 

In the new column, I typed in the first cell a function similar to this:

```
=A2 * 2000000  
```

Quick explanation: An equal sign is needed for Google Sheets functions! A2 was the cell I was referencing from the old column that I wanted to be converted in the *new* column. "200000" is the value I was multiplying it by because 1 ton equals 2000 pounds, and since the unit was 1000 short tons, 1 "1000 short ton" was actually equal to "2000 * 1000" or "200000" pounds. 

Magical, right? I did such basic conversion and cleaning for this dataset that I'm actually embarrassed. I'm sorry you have to see this @Deena or @Jrue. I swear I tried really hard. The process of making the dataset nice enough to make charts from was actually more difficult than it looks here.

Using the process above, I converted the data on imports, exports, and production of each of the corn sweeteners into pounds to match the per capita availability unit as best as I could.

But there was a second issue.

2. "NA" was showing up on a lot of the columns, specifically for information on total imports of HCFS per year in 1000 short tons. This not available data was causing the new columns showing the conversion to display "#VALUE!"

I wanted to compare data that was available for all sweeteners in all categories, so I decided to omit analyzing these years. When I was preparing the data for analysis, I used the "paste values only" special function. 

!!! ATTACH IMAGE OF paste_value !!!!

!!! ATTACH IMAGE OF afterpaste_value !!!!

Unfortunately, this move also caused this issue (because it was VERY unlikely that any imports of a corn sweetener like dextrose would be at "0" for a country like the U.S. (no offense):

!!! ATTACH IMAGE OF arefulwithzeroes_errorwithpastevalue !!!!

I had to go back to the original column, double check my data, and then manually correct and convert the data. It's good to double check! 

## Filtering through my merged dataset

After this tedious process was over, I thought it would be cool to look through this merged data using the **filter** function on Google Sheets.

Because all of this data hinged on the *year* they were collected, I thought it would be interesting to see which year(s) experienced the highest corn sweetener production and per capita availability.

Some example images of what I found:

!!! ATTACH IMAGE OF whichyearhighestglucoseprod !!!!

!!! ATTACH IMAGE OF whichyearhighestdextroseprod !!!!

!!! ATTACH IMAGE OF whichyearhighestHFCSprod !!!!

!!! ATTACH IMAGE OF whichyearhighestavailabilityTOTAL !!!!

!!! ATTACH IMAGE OF percapitaAtLow2013 !!!!

The year **1999** saw the highest per capita availability and production for HFCS, the year **1996** saw the highest dextrose production, and the year **2013** saw the highest glucose production (but **1997** saw the highest per capita availability for glucose - 2 different years). 

Data notifies people of inconsistencies, but they don't tell the full story. I wonder if there have been certain **policies or laws** that explain why these dates saw the highest rates of production or availability or why there was a drop after these years? 

The data showed interesting results when I organized them from A --> Z (least to greatest) instead of Z --> A (greatest to least). While I expected earlier years to have *less* production or per capita availability of corn sweeteners (especially because the population was smaller then), **2013** - a fairly recent time relative to the years in this dataset - was actually the year with the 5th lowest per capita availability for HFCS. The same question emerged: Are there certain **policies or laws** that explain this discrepancy?

Interrogating this data past "filtering" it was somewhat unsuccessful. Pivot tables don't reveal much else about the data that filtering could, but they do enable the creation of clean graphs (below is a pivot table of per capita availability of all corn sweeteners).

!!! ATTACH IMAGE OF pivottable_notmuch !!!!

## Visualizations from my merged dataset

I wanted to compare the **per capita availability** of **all corn sweeteners** per pound with the U.S. population for the years 1981-2013 (the span of years where data was available for ALL categories (production, imports, exports, per capita availability) for ALL corn sweeteners). 

<iframe width="600" height="371" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSjQYJanahYRgjMdP2bRpHYrrGwKR1pwsMcw9gPp77WAGtbg0Y0WN1f8t-ZUQUU0cSa7md7EkkEwfqA/pubchart?oid=841126474&amp;format=interactive"></iframe>

Per capita availability of *all corn sweeteners* seems to be declining in comparison to overall U.S. population. 

I then wanted to focus on a culprit of several health conditions and diseases in the eyes of health professionals and concerned moms: HCFS.

<iframe width="668" height="413" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSjQYJanahYRgjMdP2bRpHYrrGwKR1pwsMcw9gPp77WAGtbg0Y0WN1f8t-ZUQUU0cSa7md7EkkEwfqA/pubchart?oid=687936202&amp;format=interactive"></iframe>

Total production of **HCFS** seems to start dropping after 1999 (again, I wonder if there was key legislation passed specifically about corn sweeteners), with noticeable drops in 2009/2010 and 2013. However, because of the large rise starting from the 80s, the production of HCFS still seems relatively high. 

I also wanted to investigate per capita availability of HFCS in pounds compared to the U.S. population.

<iframe width="680" height="420" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSjQYJanahYRgjMdP2bRpHYrrGwKR1pwsMcw9gPp77WAGtbg0Y0WN1f8t-ZUQUU0cSa7md7EkkEwfqA/pubchart?oid=1742885696&amp;format=interactive"></iframe>

Per capita availability of HFCS in pounds noticeably **rose** in the 90s before dropping again in the early 2000s. 

I thought it would also be interesting to compare the total imports and exports of HFCS per year from 1981 to 2013 (unfortunately there wasn't data for this on all corn sweeteners - but for *future* analysis I would want to conduct this process for dextrose and glucose as well). 

<iframe width="600" height="371" seamless frameborder="0" scrolling="no" src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSjQYJanahYRgjMdP2bRpHYrrGwKR1pwsMcw9gPp77WAGtbg0Y0WN1f8t-ZUQUU0cSa7md7EkkEwfqA/pubchart?oid=1530179053&amp;format=interactive"></iframe>

I found it interesting but not surprising that around the same time as per capita availability and total production of HFCS was at its peak during this time period, imports exceeded exports of HFCS as well. What also is fascinating is the large gap that exists between importation and exportation of HFCS - this gap brings up more questions beyond the scope of this rudimentary analysis such as "**Who** (which countries in the world) would the U.S. be exporting all this HFCS to?" and "Why those particular countries?"

## Conclusions & Further Investigation

This data seems boring on the surface, and even before I created visualizations from the merged dataset I crudely compiled, I didn't think I would stumble across anything noteworthy. Yet, it's always worth thinking about how the U.S. handles (exports/imports/produces) products like these that have been proven through multiple studies to be detrimental to our health and how prevalent these substances are. 

I would want to take a deeper dive with this data and other data centered on which countries import corn sweeteners from the U.S. Additionally, if I had more time, I would have taken a closer look at any legislation that was passed in the late 90s regarding corn sweetener consumption or if any USDA-related legislation aligned with the trends that this data show. 
