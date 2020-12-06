# Mapping Tesla Superchargers in the U.S.

## Project Overviews

This repository was created for the DSCI 511 course at Drexel University. The overall scope of this project is to scrape Tesla’s website for Supercharger locations in the U.S. and create a `.csv` file of these data points. Considering Tesla is the leader in the field of electric cars, we will be focusing on data collection of only Tesla Superchargers by using BeautifulSoup to scrape their supercharger location pages. After running our code, the results can be verified with the U.S. government dataset of every charging station in the U.S. 
 
## File Manifest: 

- `final_project.ipynb` - Main code that scrapes the Tesla website
- `Database_Checker.ipynb` -  Main code used for Tesla and Federal comparison
- `Folder /data` - Contains all data files 
  - `tesla_superchargers.csv` - Tesla dataset created after running code
  - `alt_fuel_stations (Oct 4 2020).csv` [Federal dataset](https://afdc.energy.gov/stations/#/analyze?country=US&fuel=ELEC&ev_levels=all&access=public&access=private) copy
  - `output.json` Initial JSON output for proof of concept, final version will *not* output this file.
- `Folder /drafts` - Contains code versions used to scrape Tesla website
  - `10-11-2020.ipynb` - First version of code used for scraping
  - `Project 11-16-2020.ipynb` - Second version
  - `Project 11-23-2020.ipynb` - Third version 
- `Tesla Data Project Presentation.pptx` - PowerPoint slides for final presentation
 
## Reason for Project:
The topic of interest arose from recent years, electric cars have been gaining 
popularity. There are multiple reasons why people opt for a hybrid or an entirely electric vehicle. One reason is the individual’s ability to save money in the long-term due to the longevity and low maintenance required for electric vehicles in comparison to fuel vehicles. Another reason is the growing concern for the environment.  Many individuals that are concerned about the harmful emissions released into the environment have opted for a vehicle with a lesser carbon footprint.

Having a collection of Tesla Supercharger locations can provide benefits for personal and commercial usage. Those that are interested in purchasing a Tesla can use this project to get the most up-to-date information regarding Superchargers. Businesses can consider using this data to figure out the closest charging locations and help with other analytic decision making for investment opportunities.

## Team Members

Our team consists of the following individuals: 

- Ashley Ziur, anz27@drexel.edu
- Shoshone Smith, sys39@drexel.edu
- Wesley Marshall, wm374@drexel.edu
- Zach Carlson, zc378@drexel.edu

## Design
- This project was developed using Python 3.8 and using Jupyter Notebooks. 
- Python modules, packages, and methods required: 
    - `from bs4 import BeautifulSoup`
    - `import urllib`
    - `from pprint import pprint`
    - `import csv`
    - `import re`
- Our code will scrape Tesla’s website for Supercharger locations and then export those locations to a `.csv` file.
    - _**NOTE: Make sure to place this `.csv` file into the data folder of the project for the verifier function to work.**_ 
    - By default, the Federal Dataset `.csv` file needs to be located in the data folder. It should be there already.

## Results of Code:

After running the code, the resulting dataset is found in two main formats. In Python, the data structure of the results is a nested dictionary file type that is written out to a `.csv` file. In addition, outside of Python, a local `.csv` file is created after code execution. 

## How to Execute Code: 

All of the code in this project needs to be opened with the Jupyter notebook environment. We recommend using [Anaconda](https://www.anaconda.com/products/individual) to help with Jupyter notebook.

### _**Tesla Scraping Section**_

To view and run the project, open the `final_project.ipynb` file to see all of the final code for the project. 

Run each cell from top to bottom. 


### _**Checking between Datasets Section**_

To compare Tesla supercharger locations between the Tesla dataset and Federal dataset, open the `Database_Checker.ipynb. `

Run each cell from top to bottom

The last cell will ask for multiple user inputs. Follow these inputs based on the options that output. The program will not stop till the stop input is provided based on the output options.


## Explanation of Code: 

### _**Tesla Scraping Section**_

In this section, we explain how our code works from beginning to end of capturing the website to pulling elements with BeautifulSoup and building our dataset. 

By using `URLOpen`, we were able to request the Tesla page of all of the Supercharger locations in the United States. We saved this full markdown webpage into a variable. After saving this data into a variable, we used `BeautifulSoup` to have an `HTML.parsed` version of the data.  

Once we had this information, we looked for specific data of interest, including the street address and locality (city, state, and zip code). 

Next, we went through both street address and locality and cleaned the data to remove any whitespace and pull in text from the `<span>` and `<a>` tags from the `HTML` and saved these to their own list in Python, `street_address_list` and `city_list`. 

We also created a `title_list` variable that holds all of the names of the charging stations. We used BeautifulSoup to find all of the URL links that are a part of the class `fn org url`. When following these URL links will take one to each individual Tesla Supercharger detail page. Since we are creating a nested dictionary, we used a `for` loop that creates unique keys based on the titles. For any title that is duplicated, it will appear with a “#2” at the end. 

After creating all three variables of data - `street_address_list`, `city_list`, and `title_list` - we zipped each together to create our nested dictionary for our final output. 

Once creating the nested dictionary variable, we use the `DictWriter` method to create the final `.csv` file, `tesla_superchargers.csv`. We created this file by iterating over the keys of the nested dictionary whose values were dictionaries themselves.  These values were saved into a list of five elements which were then saved to the `.csv` file using the `writerow` method.

### _**Checking between Datasets Section**_

By running the cell that includes the verifier code will load in both `.csv` files. The Federal dataset `.csv` file and the newly created Tesla Supercharger `.csv` file. After loading these two `.csv` files a menu will print to ask for user input and display the options. 
A user can enter their desired input to check for superchargers via either the Federal or Tesla dataset. By selecting either option, the user is able to enter either a state, city, or zipcode to search a dataset.

We use a loop that will look through the selected dataset and will match the user input and saves any matches to a list to later be printed out after the loop. After printing the list, the list is reset. 

The verifier will continue to loop, asking the user for an option and input, until the user enters the quit command.


## Known Limitations of Project:

- The project is limited to the collection of data only from Tesla’s website, not including any other electric vehicle. 
- Consumers cannot use our project to check for locations of other types of electric vehicles, only Tesla Supercharger locations.
- The federal dataset information used is time dated to the time of download. The last download of the dataset was: October 4th 2020
- The `Database_Checker` is limited to user input of: State, City, and Zip Code - between the datasets.


## Potential Future Development: 

- Allowing for more potential user inputs to allow for more filtering of results.
- Expanding the scope to include other locations besides the United States.
- Expanding the scope of the project to account for non-Tesla vehicles. When one is entered, our program would pull addresses from the Federal dataset.
- Embed the HTML link into the output result to take the user to the Tesla supercharger page
- Adding a GUI for the project


## Sharing Permissions:

- Content is free to share and copy for own use
 


