This is a part of my Capstone project for a Coursera Specialization on Python. I discussed in [this thread](https://www.coursera.org/learn/python-data-visualization/discussions/all/threads/pJouE2SSEeeoNBLy-QPjJA/replies/dNK5JpYBEeePthLOl8mzhA?page=4) about the initial idea for my project. I then went ahead with a data-set that interested me from http://data.gov.in. The [data set](https://data.gov.in/catalog/road-accidents-india-classified-according-various-parameters) provided data related to Road Accidents in India classified according to various parameters. I picked up the data provided on the total number of road accidents in various Indian states and Union territories (UT) along with the educational qualification of the Drivers responsible for the accidents. The website provided data in separate JSON files (one each for each type of educational qualification) for the period of 2009-2015. The education qualification was divided in categories “Below 8th Standard” (primary school education only), “From 8 to 9 Standard” (secondary school educated) and “Above 10 Standard” (Senior secondary or Graduate/Post Graduate etc.). I discarded the data where educational qualification was not available (unknown) or accidents were not reported (zero).

The data provided was 4 dimensional (Year of Accident, Number of Accidents, Name of State/UT where accident took place, Education Qualification of the driver). I chose to use the [Google Bubble chart](https://developers.google.com/chart/interactive/docs/gallery/bubblechart) for visualization.

I wrote a Python script [AccidentsJsonImporter.py](https://github.com/dchucks/coursera-python-course/blob/master/capstone/accidents-analysis/AccidentsJsonImporter.py) that picks up all JSON files from a given directory containing accident data and then inserted in to the local SQLLite Database accidentsdb.sqlite. I had to cleanse the data at places where state names were spelled differently (example: “Andaman and Nicobar Islands” and “Andaman & Nicobar Islands”). Another Python script [AccidentsChartGenerator.py](https://github.com/dchucks/coursera-python-course/blob/master/capstone/accidents-analysis/AccidentsChartGenerator.py) then queried the database and created the bubblechart.html file with required JavaScript needed to display the [bubble chart](https://github.com/dchucks/coursera-python-course/blob/master/capstone/accidents-analysis/bubblechart-top3-states.html).

Initially, I selected data for all 36 States/UTs and the Bubble chart (except for looking colorful) really came out too crowded to decipher anything.

![Alt text](https://github.com/dchucks/coursera-python-course/blob/master/capstone/accidents-analysis/bubblechart-all-states.JPG "Accident data for all Indian States/Union Territories - 2009 to 2015")

I then changed the query to display data for the top 10 States/UTs that had maximum number of accidents during this 7-year period. The resulting chart (see below) was better but still crowded.

![Alt text](https://github.com/dchucks/coursera-python-course/blob/master/capstone/accidents-analysis/bubblechart-top10-states.JPG "Accident data for top 10 Indian States/Union Territories - 2009 to 2015")

Finally, I created the chart with just the top 3 culprit states. The chart now looked much better (see below).

![Alt text](https://github.com/dchucks/coursera-python-course/blob/master/capstone/accidents-analysis/bubblechart-top3-states.JPG "Accident data for top 3 Indian States/Union Territories - 2009 to 2015")

The Chart displays the year on x-axis and number of accidents on y-axis. The bubbles are colored according to the Indian State they represent. The size of the bubble represents the educational qualification of the driver, larger the bubble size more educated was the driver.

The results of the analysis were quite interesting and in fact changed my own prejudice on the subject. A common perception (perhaps) is that more educated drivers are likely to cause fewer accidents (as they might be more aware of traffic rules, would be more mature etc.). The chart shows that the reality is actually the very reverse. The data shows that people who just received primary education (educated less than Standard 8) had caused lesser accidents than those educated higher than them. In fact, the clear pattern is that “Higher the educational qualification of the driver, more likely s/he is to cause an accident”.

A formal account was also [published at LinkedIn](https://www.linkedin.com/pulse/so-less-educated-drivers-cause-more-road-accidents-chakrabarty).
