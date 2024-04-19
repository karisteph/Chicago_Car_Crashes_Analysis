# Chicago Car Crashes Analysis
## Introduction
It comes as no surprise that the largest contributors to car accidents are neglecting safety measures and driving while incapacitated. Night-time driving and crashes in disadvantaged areas also significantly increase accident risks. Night driving raises fatality or serious injury chances by 90%, while disadvantaged areas add another 28%!

This project analyzes reported vehicle accidents in Chicago from the previous 9 years. We processed data from the city's data portal to provide insights for the city's current mayor.


<img width="828" alt="Screenshot 2024-04-18 at 4 41 49 PM" src="https://github.com/karisteph/Chicago_Car_Crashes_Analysis/assets/157851606/b149da8e-9bac-426e-af88-a51681b83004">

## Business Problem
Mayor Brandon Johnson is interested in reducing the deadliness of car crashes in Chicago. Our team was tasked with reviewing and analyzing the data from 2015 to the present to enhance road safety. 

The mayor wants to know:

  - Which factors have the greatest influence on fatal or serious injury car accidents?
  - Are there any factors unrelated to driving behavior that contribute to serious car accidents?
  - What measures can be implemented to decrease the likelihood of serious crashes occurring in the first place?

## Data and Resources Used
![image](https://data.cityofchicago.org/api/assets/73F1665C-0FE6-4183-8AD1-E91DB8EFAFA4?7CB02402-8E06-48B0-8C9A-3890182D58C7.png)

For this project, we obtained a [dataset](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if/about_data) from the Chicago Data Portal, encompassing data from 2015 up to April 2024. It includes:

  - Car crashes
  - People in crashes
  - Socially disadvantaged areas geographies

<img width="497" alt="Screenshot 2024-04-18 at 6 14 19 PM" src="https://github.com/karisteph/Chicago_Car_Crashes_Analysis/assets/157851606/c89f9f29-580f-4dae-a280-94411af1bd4d">


## Methods
We address our business problem by employing data science techniques, beginning with data cleaning. 

  - The initial data exploration included: 48 columns in the Crashes dataset and 29 columns in the People dataset
  - Most columns were not useful
  - Other columns have substantial gaps in the data
  - We decided to keep 13 columns from Crashes and 3 columns from People

After cleaning the data we generated the master dataset and conducted an analysis using Python. 

Further exploration of the data led to the application of more advanced modeling techniques to determine the likelihood of a crash resulting in a fatality or incapacitating injury.

The target variable is severely imbalanced, with only 1.8% of accidents involving severe consequences. As a result, accuracy of any model is likely to be naturally high, and also a bad metric. Instead, recall more closely fits the City's goals. At the expense of some false predictions, models targeting an improved recall score will provide actionable insights to the City to minimize these types of accidents.

Socially Disadvantaged Districts Map: the parts of Chicago that have been deemed 'Socially Disadvantaged'
![Untitled](https://github.com/karisteph/Chicago_Car_Crashes_Analysis/assets/157851606/e62fd914-7efe-47cf-b440-e55abad3732d)

Steps Completed Before Modeling Data:
- Geographic analysis
- Prepared datetime data for analysis
- Merged the DataFrames for modeling purposes

Modeling Progression:
- Created a baseline model >> Due to the severe imbalance, a dummy model that optimizes using majority class results in 98.2% accuracy, but 0% recall and an AUC score of 50% that is no better than random guessing.
- Created a first simple model - logistic regression with three predictors >> This model does not successfully predict any positive cases, although the higher AUC suggests setting a lower probability threshold might lead to better predictions.
- Created a logistic regression model with many predictors which must be encoded >> This improved the ROC-AUC marginally, but the recall is still 0. The class imbalance is too great.
- Created a logistic regression model with SMOTE >> The final complex model is a very good model which finally captures 73% of true positives. There are many more false positives as well, which is a predicted effect of improving recall. In this case, it is an acceptable trade-off. 


![Untitled](https://github.com/karisteph/Chicago_Car_Crashes_Analysis/assets/157851606/0473a9e7-533e-4040-8a7c-9f898ae22dca)


## Data Analysis Results
Our analysis shows that the following factors seem to have the largest effect on fatal or serious injury car accidents:

- The use of safety features
- The driver's condition
- Whether the crash happened during the night 
- Whether the crash happened in a socioeconomically disadvantaged area (SDA)

Below, the coefficients are shown and calculated odds increase of each factor: 


![Untitled](https://github.com/karisteph/Chicago_Car_Crashes_Analysis/assets/157851606/ead3288e-a1c6-4280-8fd7-995c94aa96e8)

The effect on the odds of a severe accident is plotted below:

![Untitled](https://github.com/karisteph/Chicago_Car_Crashes_Analysis/assets/157851606/89c1831c-5a97-4132-8c3f-0e6ee5a3542d)

## Recommendations

1. Neglecting safety measures, driving while incapacitated, night-time driving, and crashes in disadvantaged areas all significantly influence fatal or serious injury car accidents in Chicago. The data showed that incapacitated drivers, remain one of the leading factors contributing to car crash fatalities or serious injuries.

- "Every day, about 37 people in the United States die in drunk-driving crashes — that's one person every 39 minutes." - [How Alcohol Affects Driving Ability](https://www.nhtsa.gov/risky-driving/drunk-driving#:~:text=Every%20day%2C%20about%2037%20people,These%20deaths%20were%20all%20preventable.)

- #### We propose investing in tech. With the financial resources invested, you could incentivize drivers to use devices that detect for distracted driving and other dangerous driving behaviors like speeding. 

2. We discovered a non-driving-related factor contributing to severe car accidents: being in a Socioeconomically Disadvantaged Area at the time of the accident. The diminished quality of services, including limited EMS accessibility and lower-quality hospital care in these areas, may lead to increased fatalities or serious injuries.

- #### We recommend prioritizing these areas when it comes to the maintenance of traffic lights, visible crosswalks and other street design safety features. 

3. Certain measures can be implemented to decrease the likelihood of serious crashes at night. We know that a driver's vision is severely limited at that time of day more than any other time.
    
- #### We recommend ensuring that street lamps and reflective tapes are regularly maintained to increase visibility when it is at an all time low.

## Future Investigations

- Age of the driver
- Proximity of the crash to major holidays
- Geographic proximity of the crash to a hospital
- Whether the make/model of the car leads to differential outcomes (i.e. for EVs, pickups)
- Whether severe outcomes have different predictors for pedestrians, bicyclists and drivers

## For More Information
Please review our full analysis in the jupyter notebook [Chicago Car Crashes Analysis](https://github.com/karisteph/Chicago_Car_Crashes_Analysis/blob/main/Chicago_Car_Crashes_Analysis.ipynb)

Refer to our [Presentation](https://docs.google.com/presentation/d/1ckk2djo9aRBG1i314E5EMvmnY5OmWTe6D2UCEkn9pOk/edit#slide=id.p)

Note: The complete dataset used for this project is available upon request. Due to its large size our team decided to exclude the entire dataset from this repository. To enhance efficiency, specifying specific columns for importation for each dataset reduces processing time and minimizes the use of computational resources.


## Contributors
-[Karina Baculima](https://github.com/karisteph)
-[Rick Lataille](https://github.com/rjlatail)
-[Daniel Fox](https://github.com/DBAfox)


## Repository Structure
```
|— README.md                                                 <- The top-level README for reviewers of this project
|— Car_Crashes_Analysis_Repo.pdf                             <- PDF version of repository
|— Car_Crashes_Analysis_Presentation.pdf                     <- PDF version of project presentation
|— Car_Crashes_Analysis.ipynb                                <- Interactive computing environment including analysis in Jupyter                                                                     notebook
|— Chicago_Car_Crashes_Analysis - Jupyter Notebook.ipynb     <- PDF version of jupyter notebook
|— .gitignore                                                <- Exclude listed files, mainly '.csv'
|— Data                                                      <- Geometry files
    |— Beat.cpg
    |— Beat.dbf
    |— Beat.prj
    |— Beat.shp
    |— Beat.shx
    |— Images.xlsx
    |— SD_geo.cpg
    |— SD_geo.dbf
    |— SD_geo.prj
    |— SD_geo.shp
    |— SD_geo.shx                                    
