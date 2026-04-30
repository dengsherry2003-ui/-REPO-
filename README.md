# Mapping Dissent: A Temporal and Spatial Analysis of Civil Disobedience in Iran

## Project Overview
This project investigates the spatial and temporal dynamics of civil unrest, political violence, and state repression in Iran over the past decade. By processing and visualizing types of protests and demonstrations, coupled with their frequency and intensity changes over time and across regions, this repository provides an analytical framework to understand how Iranian civil disobedience and resistance evolved in the past decade.

The project culminates in an interactive **Civil Disobedience Dashboard** (`Dashboard.html`), featuring bivariate geographical mapping and year-by-year trend analysis to highlight the patterns in Iranian people's resistance.

---

## Data Sources
All data for this analysis is sourced from the **[Armed Conflict Location & Event Data Project (ACLED)](https://acleddata.com/conflict-data/download-data-files)**. 

Specific aggregated datasets utilized include:
* [Number of Political Violence Events by Country-Year](https://acleddata.com/aggregated/number-political-violence-events-country-year)
* [Number of Demonstration Events by Country-Year](https://acleddata.com/aggregated/number-demonstration-events-country-year)
* [Number of Events Targeting Civilians by Country-Year](https://acleddata.com/aggregated/number-events-targeting-civilians-country-year)
* [Number of Reported Fatalities by Country-Year](https://acleddata.com/aggregated/number-reported-fatalities-country-year)
* [Number of Reported Civilian Fatalities (Direct Targeting) by Country-Year](https://acleddata.com/aggregated/number-reported-civilian-fatalities-direct-targeting-country-year)
* [Aggregated Data for the Middle East](https://acleddata.com/aggregated/aggregated-data-middle-east)

*Note: Access to ACLED data requires registration and adherence to their terms of use.*

---

## Methodology

### 1. Temporal Analysis of Iranian Dissent (2016–2026)
To capture the longitudinal evolution of civil unrest and state repression, the project conducts a detailed time-series analysis spanning a decade. The temporal pipeline involves isolating and aggregating data specifically for Iran (2016–2026) across several macro-level ACLED datasets.

**A. Event & Fatality Metrics:** To map the volume, trajectory, and lethality of unrest over time, Iranian records are filtered and merged from the following datasets:
* *Number of Political Violence Events by Country-Year*
* *Number of Demonstration Events by Country-Year*
* *Number of Events Targeting Civilians by Country-Year*
* *Number of Reported Fatalities by Country-Year*
* *Number of Reported Civilian Fatalities (Direct Targeting) by Country-Year*

**B. Strategic Context Filtering:** To contextualize the raw violence and protest metrics, data from the *Aggregated Data for the Middle East* is specifically filtered for `EVENT_TYPE == "Strategic development"`. This isolates crucial non-violent or preparatory state actions—such as mass arrests, policy shifts, security force deployments, and changes in the regime's riot-control posture.

By tracking these filtered metrics chronologically, the dashboard's Plotly time-series charts reveal the cyclical waves of national protests (e.g., the 2019 fuel protests, the 2022 "Woman, Life, Freedom" movement) alongside the state's corresponding mobilization of violence and strategic suppression.

### 2. Spatial Analysis: The Disobedience Index
To prevent simple event counts from masking the true severity of localized conflicts, this project calculates a custom **Disobedience Severity Index (DSI)** for each province. 

* **Event Weighting:** Sub-event types are assigned severity weights ($w$):
   * Peaceful protest: 1
   * Protest with intervention: 2
   * Excessive force against protesters: 3
   * Violent demonstration: 4
* **Base Calculation:** $$Score = \frac{w^2 \times Events \times (Fatalities + 1)}{Population Exposure}$$
   *(A baseline of +1 is added to fatalities to ensure non-lethal, high-frequency events retain their fundamental weight, while events with casualties are heavily amplified.)*
* **Logarithmic Transformation & Normalization:** To prevent extreme outliers (such as highly lethal military crackdowns in specific provinces) from visually suppressing variance across the rest of the country, a logarithmic transformation `[ln(1 + x)]` is applied. Finally, scores are normalized to a 0.0 – 1.0 scale.

---

## Key Findings: The Geometry of Unrest
The interactive map reveals a stark geographical divergence in state repression strategies across Iran:
* **The Core (High Frequency, Low Lethality):** Major metropolitan areas like Tehran and Isfahan record the highest absolute number of protest events. However, due to political risk and international visibility, state suppression typically relies on non-lethal crowd control tactics (tear gas, mass arrests).
* **The Periphery (Low Frequency, High Lethality):** Marginalized border regions, most notably **Sistan and Baluchestan**, exhibit the highest Disobedience Index. The regime consistently frames dissent in these Sunni-majority areas through a securitized lens, justifying highly militarized and lethal force. This indicates that the friction between the state and the local population has reached a critical threshold in the periphery.

---

## Repository Structure

* `Code/Violence.ipynb`: The core Jupyter Notebook containing the data pipeline. It reads the raw ACLED data, calculates the Disobedience Scores, performs regional aggregations, formats the data into JSON, and generates the final HTML dashboard using Python string formatting.
* `Report/Dashboard.html`: The fully interactive, standalone web dashboard generated by the notebook. It utilizes **Leaflet.js** for the interactive bubble map and **Plotly.js** for the time-series charts.
* `Data/Data_Raw`: The folder containing all raw downloaded ACLED CSV files 
* `Data/Data_Processed/Iran_disobedience.csv`: The processed dataset containing all the Iran-related events, fatality, and exposure counts from [Middle East aggregated data](https://acleddata.com/aggregated/aggregated-data-middle-east).

---

## How to Use

### 1. View the Dashboard
No installation is required to view the final output. Simply clone the repository and open `Report/Dashboard.html` in any modern web browser (Chrome, Safari, Firefox, Edge).

### 2. Adjust for Local Environment
The `Violence.ipynb` notebook was originally written in Google Colab. To run it locally, open the notebook and delete (or comment out) the Colab-specific mounting code in the first cell:
```python
# from google.colab import drive
# drive.mount('/content/drive')
```

### 3. Update the Project Path
In the first cell, update the project_path variable to point to the absolute or relative path where you saved this repository on your local machine:
```python
project_path = "./" # Use relative path if the notebook is in the main folder
```

### 4: Verify Folder Structure
Ensure your local directory matches the script's expected architecture:
* Place the downloaded ACLED Excel files inside Data/Data_Raw/.
* Ensure Data/Data_Processed/ exists (the script will export Iran_violence.csv and read Iran_disobedience.csv here).
* Ensure the Report/ folder exists for the final HTML export.

### 5. Run the Notebook
To replicate the data processing and regenerate the dashboard:
1. Ensure you have Python installed along with the following libraries:
* `pandas` (for data manipulation and cleaning)
* `numpy` (for numerical operations and logarithmic transformations)
* `plotly` (for generating the interactive time-series charts)

You can install all the required dependencies quickly via your terminal or command prompt:

```python
pip install pandas numpy plotly
```

## Limitations

While the data provides a compelling look at Iranian civil unrest, the following limitations should be considered when interpreting the results:

* **Reporting Bias & Censorship:** The data relies heavily on ACLED’s collection methods, which aggregate media reports and NGO statements. In highly restrictive environments like Iran, state-led internet shutdowns and the suppression of journalists can lead to an undercounting of events, particularly in remote rural provinces.
* **Lag in Fatality Verification:** Fatality figures in conflict zones are often subject to revision. While ACLED is rigorous in its verification, the figures for very recent events (Q1 2026) should be viewed as conservative estimates that may rise as more information becomes available.
* **Population Exposure Proxy:** The *Disobedience Severity Index* uses population exposure as a denominator. While this helps normalize the data, it does not account for the varying demographic density or the specific "tactical value" of certain locations (e.g., a small protest at a major oil refinery may be more significant than a larger one in a residential square).

---

## Author Information

**[Your Name]** *Undergraduate Student, University of Hong Kong (HKU)* **Academic Background:** Statistics & Political Science  
**Research Interests:** Data Science in Public Policy, Middle Eastern Geopolitics, and Quantitative Conflict Analysis.

This project was developed as part of **POLI3148: Data Science in Politics and Public Administration**.

* **GitHub:** [Your GitHub Profile Link]
* **Contact:** [Your Email Address]
* **Date:** April 2026
