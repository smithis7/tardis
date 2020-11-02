# tardis_impact.

## DO NOT COMMIT ads.ipynb WITHOUT REMOVING ADS TOKEN!!!

Documenting papers that use TARDIS (Temperature And Radiative Diffusion In Supernova) code.

Use the file ads.ipynb to edit the code that produces the desired list.

### You can type out notes about your progress below:

Isaac: My next step is to edit the format_arxiv_codes to exclude the 'arXiv:' and the final letter. This will allow the creation of a function that will pull up the PDF on arXiv by pulling up the PDF 'https://arxiv.org/pdf/'+arxiv_code+'.pdf'. I'm still working on understanding how the format_arxiv_codes code works so that I don't mess it up when I edit it.

Kevin (2/11/2020): The above has been done, and there is not a hyperlink for each code that has an arXiv code. Tried to begin opening a pdf but ran into encoding issues. Slight changes to the ads.ipynb and have the sample code to work with to see if we can decode a specific file for now. Changed this, I made a file using just the article names. Unsure what needs to be done now.