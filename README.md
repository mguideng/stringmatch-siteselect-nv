README
================
Maria Guideng

stringmatch-siteselect-nv
=========================

Top Site Selection Factors for Incentived Companies Relocating or Expanding in Nevada
-------------------------------------------------------------------------------------

I recently read the results of this year's *AreaDevelopment* site selection factor surveys. Executives from the companies considering new locations ranked the "availability of skilled labor" in the \#3 spot. The consultants that advise them on location strategy viewed it as the most critical, ranking it \#1. This had me reflecting on my home state. Which factors are most important to companies looking to relocate or expand in Nevada? One might guess a business-friendly tax environment, and that's right. That's one of them.

It can vary considerably whether a company, through an internal representative or outside consultant, works the most with state or local-level economic development organizations throughout this process. Not here in Nevada. It's pretty clear cut. We have a unified economic development ecosystem where the local and regional development partners are at the forefront of this process (with some exceptions, of course). Having previously worked at the state-level Nevada Governor's Office of Economic Development, I was a liason between the regional partners and the companies. Even in my somewhat limited exposure, it was evident that workforce considerations were a big deal; companies were very much interested in knowing more about workforce training opportunities and information about the concentration of workers in various industries and job types.

This is conventional wisdom is this field, or common sense really, but I was still interested in seeing what the numbers had to say for Nevada. I knew this was possible. A survey section to rate various site selection factors was added in the applications that companies filled out to apply for state incentives four years ago. Since then, over 150 companies have applied for incentives.

Aside from satiating my own curiosities, this project is more about applying R's regular expressions (regex) capabilities to mine text (and my learning how to put together a dashboard in Tableau afterwards). After some thought, this was an ideal fit and simple enough. I knew exactly what I wanted to do, but definitely wasn't so sure if that exact way was possible! This turned out to be a pretty fun learning project.

Not surprisingly, workforce was indeed a resounding top criteria for the companies across industry sectors and regions in Nevada. Visualization results are available via my [PublicTableau profile](https://public.tableau.com/profile/maria.guideng#!/) and a write up can be found [here](https://mguideng.github.io/2018-05-14-workforce-matters-nv/).

This repo is for demo purposes, shown as an example of scraping PDF reports using text pattern matching. It contains a sample of files from the source (the first five PDF reports from the latest May meeting) and scripts that mine text for select variables.

Workflow
--------

The source of the data is from publically available PDF reports from the Nevada Governor's Office of Economic Development, which holds bimonthly [open meetings](http://www.diversifynevada.com/meetings/category/goed-board) to approve applicant companies and their expansion projects for tax incentives.

Start by downloading and unzipping the "workflow.zip" folder. Contents include the following subfolders:

-   `1downloadspdf`: the source data files
-   `2downloadstxt` and `3finalfiles`: empty folders to catch the scripts' outputs
-   `4script`: contains the R scripts for the two-step process outlined below

**Step 1 - Screen PDF reports for presence of survey.**
Start with script `1 script-to-screen-ssf.R`, which converts from PDF to text format (character vectors) for each report. Contains a for-loop to check whether there is a valid survey present, which evaluates to True or False. Output is a list with the Boolean result for each corresponding PDF file (`ssfboolean.csv`).

**Step 2 - Mine text from report.**
Script `2.1 script-stringmatch-wrapperfunction.R` creates CSV versions of the PDF reports (outputs to ' the `2downloadstxt` subfolder). Text is mined from the CSV files using a wrapper function, which calls on an external source script (`2.2 script-stringmatch.R`). Regular expressions and functions for pattern matching were used to identify and extract survey ratings for the site selection factors, plus other information about the company's expansion project (e.g., county location, industry sector, number of new jobs planned, and so on). The results are exported to the `3finalfiles` subfolder. Finally, the information is combined into a single CSV file (`masterR.csv`).
