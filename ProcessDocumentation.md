Bellabeat products:
- **Bellabeat App:** Provides user health data related to activity, sleep, stress, menstrual cycle, and mindfulness habits. Connects to their line of smart products
- **Leaf:** wellness tracker that can be worn as a bracelet, necklace, or clip. Connects to the app to track activity, sleep, and stress.
- **Time:** a smartwatch to track activity, sleep, and stress
- **Spring:** A smart water bottle to track hydration levels
- **Bellabeat membership:** Membership program that gives users 24/7 access to fully personalized guidance on nutrition, activity, sleep, health and beauty, and mindfulness

Bellabeat Marketing/Sales Strategy
- Products available through growing amounts of online retailers and Bellabeat’s website
- Traditional advertising media: radio, out-of-home billboards. print, and television
- Heavier focus and investment in digital marketing: 
- Google Search, 
- Facebook and Instagram pages, 
- active twitter engagement.
- Youtube ads
- Ads through Google Display Network to support marketing campaigns around key dates

Questions:
- What are some trends in smart device usage?
- How could these trends apply to Bellabeat customers?
- How could these trends help influence Bellabeat’s marketing strategy?

Report deliverable components:
1. A clear summary of the business task 
2. A description of all data sources used 
3. Documentation of any cleaning or manipulation of data 
4. A summary of your analysis 
5. Supporting visualizations and key findings 
6. Your top high-level content recommendations based on your analysis 

## Ask
### Guideline:
- What is the problem you are trying to solve?
- Focusing on Bellabeat’s Time smartwatch; how can the company increase its smartwatch marketing strategy to increase consumer reach, competitiveness, and sales?

### How can your insights drive business decisions?
- Insights from the data analysis can provide a view into how the smartwatch is primarily being used. 
- Gain an understanding of the primary target base; whether there is any room for expansion or downscaling (more specific targets). 
- How well is Bellabeat’s Time performing against competitors (Apple Watch, Samsung watch, Fitbit)

### Key tasks:
- Identify the business task
- Consider key stakeholders
- Deliverable:
- A clear statement of the business task
## Prepare
### Guideline:
- Where is your data stored? <br />
Google Drive
- How is the data organized? Is it in a long or wide format? <br />
A majority of the data is organized by the date-time variable. The dataset is wide or long depending on the timeframe that the data is organized; a data table organized by minute is longer (narrow) than by the hour, which is wider

- Are there issues with bias or credibility in this data? <br />
A bias was discovered after the analysis was conducted. The data collect information on a rather short time period, this would skew the data away from meaningful discoveries about user’s usage to track weight. Biologically, a person’s weight and health does not change significantly in a month, it would be hard to tell from the data if user's intentions are to improve health/weight conditions.
- Does the data ROCCC (reliable, original, comprehensive, current, cited)? <br />
The data does follow ROCCC. 
- How are you addressing licensing, privacy, security, and accessibility? <br />
The data is publicly available data provided by fitbit, obtained from Kaggle. The data is under CC0: Public Domain license.
- How did you verify the data’s integrity? <br />
The data’s integrity was verified through Google Big Query’s SQL functions. The raw datasets were imported, reviewed, cleaned, and saved into new datasets as to not damage the original source.
- How does it help you answer your question? <br />
The data provides a lot of fitness and health information on fitbit users, a major competitor of Bellabeat. Generally, user behavior will not differ when using different products, thus we can use the data to identify patterns in user behavior. 

- Are there any problems with the data? <br />
Many of the datasets have problems with timestamp formatting when uploading to BigQuery. This was discovered while in the process of uploading. For future improvement, perform preliminary data cleaning on a copy of the CSV itself. 


### Key tasks:
- Download data and store it appropriately
- Identify how it's organized
- Sort and filter the data
- Determine the credibility of the data
### Deliverable:
- A description of all data sources used
## Process
### Guideline:
- What tools are you choosing and why? <br />
The tools chosen are BigQuery for SQL manipulation and Tableau for visualization
- Have you ensured your data’s integrity? <br />
- What steps have you taken to ensure that your data is clean? <br />
Change, format, and separate date-time <br />
Conduct exploratory analysis to view information
- How can you verify that your data is clean and ready to analyze? <br />
Verification was performed through manual checking between BigQuery and Excel, as well as performing elementary queries 
- Have you documented your cleaning process so you can review and share those results? <br />

### Key tasks:
- Check the data for errors
- Choose your tools
- Transform the data 
- Document the cleaning process
### Deliverable:
- Documentation of any cleaning or manipulation of data
## Analyze
Daily Activity: <br />
Summarize average daily activity distance and minutes by day of week <br />

Sleep: <br />

&emsp; Avg sleep and bed time by day of week: <br />
&emsp; Day		avg_time_asleep	avg_time_in_bed <br />
&emsp; Monday	394.0			430.0 <br /> 
&emsp; Tuesday	410.0			449.0 <br />
&emsp; Wednesday	421.0			461.0 <br />
&emsp; Thursday	385.0			418.0 <br />
&emsp; Friday		395.0			431.0 <br />
&emsp; Saturday	414.0			456.0 <br />
&emsp; Sunday	458.0			500.0 <br />



In tableau, display pie chart for daily activity - minute breakdown <br /> 
Need to write sql to group such as: <br />
Datetime | Activity_Level_Minutes <br />
…..	    | very_active <br />
…..	    | Lightly Active <br />

### Guideline:
- How should you organize your data to perform analysis on it? <br />
The datasets were organized and aggregate into 5 major categories: <br />
Daily activity <br />
Sleep records <br />
Activity on an hourly time scale <br />
Activity on a minute timescale <br />
Weight <br />
- Has your data been properly formatted? <br />
As the data was imported from CSV into BigQuery, all timestamps were converted from a STRING format into BigQuery DATETIME format
- What surprises did you discover in the data? <br />
A majority of the data logs were imputed when users were at rest. This is inferred by the number of logs when user steps equated to zero
- What trends or relationships did you find in the data? <br />

- How will these insights help answer your business questions? <br />
These insights will help Bellabeat understand which situations a smart watch is primarily being used

### Key tasks:
- Aggregate your data so it's useful and accessible
- Organize and format your data
- Perform calculations
- Identify trends and relationships
### Deliverable:
- A summary of your analysis
## Share
### Guideline:
- Were you able to answer the business questions? <br />
Yes, given the limitations of the data
- What story does your data tell? <br />
Fitbit usage preferences
- How do your findings relate to your original question? <br />
The findings will help answer what direction the marketing team of Bellabeat should head to increase its customer base.
- Who is your audience? What is the best way to communicate with them? <br />
The audience will be the marketing team and senior leadership. Communication involving direct results and trends will be the most useful
- Can data visualization help you share your findings? <br />
yes
- Is your presentation accessible to your audience? <br />
yes

### Key tasks:
1. Determine the best way to share your findings.
2. Create effective data visualizations.
3. Present your findings.
4. Ensure your work is accessible.
## Act
### Guideline:
- What is your final conclusion based on your analysis? <br />
Sleep and fitness activity are the most prominent usage
- How could your team and business apply your insights? <br />
Decide on direction for marketing campaigns
- What next steps would you or your stakeholders take based on your findings? <br />
Create marketing campaigns and focus operations on the Bellabeat Time product to increase customers
- Is there additional data you could use to expand on your findings? <br />
Datasets from other smartwatch companies

### Key tasks:
- Create your portfolio.
- Add your case study.
- Practice presenting your case study to a friend or family member.

