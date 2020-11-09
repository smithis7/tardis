# tardis_impact.

## DO NOT COMMIT ads.ipynb WITHOUT REMOVING ADS TOKEN!!!

Documenting papers that use TARDIS (Temperature And Radiative Diffusion In Supernova) code.

Use the file ads.ipynb to edit the code that produces the desired list.

### You can type out notes about your progress below:

Isaac: My next step is to edit the format_arxiv_codes to exclude the 'arXiv:' and the final letter. This will allow the creation of a function that will pull up the PDF on arXiv by pulling up the PDF 'https://arxiv.org/pdf/'+arxiv_code+'.pdf'. I'm still working on understanding how the format_arxiv_codes code works so that I don't mess it up when I edit it.

Kevin (2/11/2020): Did work on the requests module, found out that it was not necessary to use after time was put into it. No need for arxiv as we don't need to download the pdf as of right now. Reduced the length of ads.ipynb as a result by A LOT, much shorter now. Changed the authors, now if there are over 3 only first 3 followed by 'et al.' are presented. All data is present, now it must be formatted.

Kevin (3/11/2020): Did the update to the ads.ipynb to make the formatting correct. 

Isaac: The citations are now formatted (I believe) in a string.

Kevin (7/11/2020): I did some research on rst but I wasn't able to download successfully using conda. I tried doing `conda install -c anaconda docutils` and doing just `conda install docutils` and it didn't work so I uninstalled them and will go back. Slight updates to the notebook to have the indent on the first line, and just did some reading about rst. 

Isaac: I am still having trouble with rst documents, but I did manage to create an html file from one-- I just had to copy and paste the citations into it. I also changed the get_journal function so that it returns the full names of the journals instead of the abbreviations.

Kevin (9/11/2020): Not done, but started on my own terrible attempt at the rst file using a few lines of code in ads.ipynb. If you run it, it will make the .rst file but there is still funky formatting that I need to figure out, not finished for today yet.