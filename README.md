# assignment-2

This is the second assignment of the semester for HES 505.

For the rest of the course, I'll be asking you to use pseudocode to plan your analysis steps before you start using any functions (or writing your own). Pseudocode allows you to think about the important steps of your process and identify your desired results before your start down the path of coding. You can think of pseudocode as an outline for syntax, much like the one you might use for writing an manuscript or report. Quarto documents are designed to let you both outline your report and plan your analysis all in the same place! This assingment is meant to give you some practice setting up your outlines before you start coding. By the end of this assignment you should be able to:

* Use Quarto to set up headings for a manuscript (like Intro, Methods, etc)

* Write out the pseudocode necessary to replicate a figure from a manuscript you like

* Insert and name code chunks to correspond to the code you'll write in the future and use knitr hooks to set up the options for how your code will run when your document is rendered.

## Instructions

1. After you've joined the assignment repository, you should have this file (named Readme.md) inside of a R project named assignment-2-xx where xx is your github username (or initials). 

2. Once you've verified that you've correctly cloned the assignment repository, create a new Quarto document. Name this file assignment-2-xxx.qmd and give it a title (like M Williamson Assignment 2). Make sure that you select the html output option (Quarto can do a lot of cool things, but the html format is the least-likely to cause you additional headaches). We'll be using Quarto throughout the course so it's worth checking out the other tutorials in the getting started section.

3. Copy the questions below into your document and change the color of their text.

4. Save the changes and make your first commit!

5. Answer the questions making sure save and commit at least 4 more times (having 5 commits is part of the assignment).

6. Render the document to html (you should now have at least 3 files in the repository: Readme.md, assignment-2-xx.qmd, and assignment-2-xx.html). Commit these changes and push them to the repository on GitHub. You should see the files there when you go to github.com.


## The Assignment

Find a figure that you'd like to mimic with your research. The figure should be from a manuscript or report and present the results of a quantitative analysis (i.e., not a conceptual model or an image). Once you've found one you should:

1. Create a section called "Introduction" in your Quarto document. In that section, you should give me the citation for the article and a brief description (similar to the caption) of the figure.
2. Create a second section called "Methods" and write out the steps necessary to create the figure. These should be similar to the pseudocode we discussed in clase (e.g., "Load Data", "Summarize by county", "Run linear regression", "Build Figure"). The methods section of the manuscript you've chosen should provide you with enough information to begin sketching this out. Don't worry if you don't know all of the steps, the goal is to get you thinking about the "mile markers" along the way to creating the figure.
3. Add in [code blocks](https://quarto.org/docs/computations/r.html) for each step in your pseudocode. Give each block a name that corresponds to your pseudocode steps.
4. Based on the webpage linked above and the "Execution Options" section linked there, add execution options to each block that ensure that the code block will be printed, but not evaluated.
5. Add a "Results" section and use the markdown command to include an image of the figure from the manuscript you chose. 
