I also want to create a dashboard using ACLED data to study the political violence and disobedience level in Iran.

**Backgrond**

The ongoing Iran Crisis and the closure of the Strait of Hormuz have created significant uncertainty to global economy and geopolitics. Many commentors now discuss about the possibility of regime change. I want to find some clues by studying the past conflicts in Iran, including demonstrations and riots. I want to study the year-by-year number of demostic volence (including political violence events, demonstration events, events targeting civilians, reported fatalities, reported civilian fatalities from direct targeting) in Iran and trend.

**Political violence events (by year data)**

I have the following data:

* Data\Data_Raw\number_of_demonstration_events_by_country-year_as-of-03Ap.xlsx
* Data\Data_Raw\number_of_events_targeting_civilians_by_country-year_as-o.xlsx
* Data\Data_Raw\number_of_political_violence_events_by_country-month-year.xlsx
* Data\Data_Raw\number_of_political_violence_events_by_country-year_as-of-03Apr2026.xlsx
* Data\Data_Raw\number_of_reported_civilian_fatalities_by_country-year_as.xlsx
* Data\Data_Raw\number_of_reported_fatalities_by_country-year_as-of-03Apr.xlsx

Help me clean the data first. Filter the provided above files where the `Country` column is strictly equal to 'Iran'. Create a new file containing only these rows. The export path is Data\Data_Processed\Iran_violence.csv

Then visualize the yearly number of all the events.

**Disobedience Level (by region)**

I have this dataset: Data\Data_Raw\Middle-East_aggregated_data_up_to_week_of-2026-04-04.xlsx. Load the data and filter it where the `Country` column is strictly equal to 'Iran'. Create a new file containing only these rows. The export path is Data\Data_Processed\Iran_disobedience.csv

List the items under each column: ADMIN1, EVENT_TYPE, SUB_EVENT_TYPE, DISORDER_TYPE

It appears that there are certain categories of events in SUB_EVENT_TYPE are civilian resistance towards the government or regime or events that will encourage disobedience, namely 

- Peaceful protest
- Protest with intervention
- Excessive force against protesters
- Violent demonstration

I want to construct a disobedience level index in Iran, and use an interactive map to show the results. I would like to attach different weight to different sub event types (the greater the number, the greater the disobedience)

* Peaceful protect = 1
* Protest with intervention = 2
* Excessive force against protesters = 3
* Violent demonstration = 4

For a row whose sub_event_type falls within the above four categories, calculate each row's value = weight * EVENTS * FATALITIES / POPULATION_EXPOSURE. Put the result in another column named DISOBEDIENCE. Aggregate all the rows of each region.

Visualize the data in an interactive map. Use the size of bubble to show the level of disobedience of each region. When my mouse touches upon the bubble, please show a 3D accumulated bar chart or pie chart to show the proportion of each sub event type in each region. No latitude data needed.


**Mob violence**
