# Project 2: Ames Housing Data - Linear Regression - README.md
#### Thomas Ludlow, General Assembly NY-DSI-6
#### December 7, 2018

## Problem Statement

**What property features are most important in accurately predicting sale prices of units in Ames, IA?  What modeling approach yields the most accurate sale price predictions?**

## Executive Summary

In Project 2, we worked with Kaggle data on building sales in Ames, IA that occurred during 2006-2010 to better understand the factors influencing sale prices.  We used this understanding to optimize linear regression models, which we then used to make value predictions on Kaggle's test data.  We optimized to return the minimum Root Mean Squared Error (RMSE), which Kaggle calculates.

Through the modeling process, we identified a number of key factors and useful methods to build a high-accuracy linear regression model that Zillow may use to predict housing prices for users searching in Ames.

## Data Dictionary

|Feature|Type|Description|Values|
|---|---|---|---|
|**saleprice**|*int*|The property's sale price in dollars **(Target Value)**|USD|
|**id**|*int*|ID value for sale row|integer|
|**pid**|*int*|ID value for property|integer|
|**ms_subclass**|*int*|The building class|20 - 1-STORY 1946 & NEWER ALL STYLES<br>30 - 1-STORY 1945 & OLDER<br>40 - 1-STORY W/FINISHED ATTIC ALL AGES<br>45 - 1-1/2 STORY - UNFINISHED ALL AGES<br>50 - 1-1/2 STORY FINISHED ALL AGES<br>60 - 2-STORY 1946 & NEWER<br>70 - 2-STORY 1945 & OLDER<br>75 - 2-1/2 STORY ALL AGES<br>80 - SPLIT OR MULTI-LEVEL<br>85 - SPLIT FOYER<br>90 - DUPLEX - ALL STYLES AND AGES<br>120 - 1-STORY PUD (Planned Unit Development) - 1946 & NEWER<br>150 - 1-1/2 STORY PUD - ALL AGES<br>160 - 2-STORY PUD - 1946 & NEWER<br>180 - PUD - MULTILEVEL - INCL SPLIT LEV/FOYER<br>190 - 2 FAMILY CONVERSION - ALL STYLES AND AGES|
|**ms_zoning**|*object*|Identifies the general zoning classification of the sale|A - Agriculture<br>C - Commercial<br>FV - Floating Village Residential<br>I - Industrial<br>RH - Residential High Density<br>RL - Residential Low Density<br>RP - Residential Low Density Park<br>RM - Residential Medium Density|
|**bldg_type**|*object*|Type of dwelling|1Fam - Single-family Detached<br>2FmCon - Two-family Conversion; originally built as one-family dwelling<br>Duplx - Duplex<br>TwnhsE - Townhouse End Unit<br>TwnhsI - Townhouse Inside Unit|
|**house_style**|*object*|Style of dwelling|1Story - One story<br>1.5Fin - One and one-half story: 2nd level finished<br>1.5Unf - One and one-half story: 2nd level unfinished<br>2Story - Two story<br>2.5Fin - Two and one-half story: 2nd level finished<br>2.5Unf - Two and one-half story: 2nd level unfinished<br>SFoyer - Split Foyer<br>SLvl - Split Level|
|**lot_frontage**|*float*|Linear feet of street connected to property|ft|
|**lot_area**|*int*|Lot size in square feet|sq ft|
|**street**|*int*|Type of road access to property|Grvl - Gravel<br>Pave - Paved<br>|
|**alley**|*object*|Type of alley access to property|Grvl - Gravel<br>Pave - Paved<br>NA - No alley access|
|**lot_shape**|*int*|General shape of property|Reg - Regular<br>IR1 - Slightly irregular<br>IR2 - Moderately Irregular<br>IR3 - Irregular|
|**land_contour**|*int*|Flatness of the property|Lvl - Near Flat/Level<br>Bnk - Banked - Quick and significant rise from street grade to building<br>HLS - Hillside - Significant slope from side to side<br>Low - Depression|
|**utilities**|*int*|Type of utilities available|AllPub - All public Utilities (E,G,W,& S)<br>NoSewr - Electricity, Gas, and Water (Septic Tank)<br>NoSeWa - Electricity and Gas Only<br>ELO - Electricity only|
|**lot_config**|*object*|Lot configuration|Inside - Inside lot<br>Corner - Corner lot<br>CulDSac - Cul-de-sac<br>FR2 - Frontage on 2 sides of property<br>FR3 - Frontage on 3 sides of property|
|**land_slope**|*int*|Slope of property|Gtl - Gentle slope<br>Mod - Moderate Slope<br>Sev - Severe Slope|
|**neighborhood**|*object*|Physical locations within Ames city limits|Blmngtn - Bloomington Heights<br>Blueste - Bluestem<br>BrDale - Briardale<br>BrkSide - Brookside<br>ClearCr - Clear Creek<br>CollgCr - College Creek<br>Crawfor - Crawford<br>Edwards - Edwards<br>Gilbert - Gilbert<br>IDOTRR - Iowa DOT and Rail Road<br>MeadowV - Meadow Village<br>Mitchel - Mitchell<br>Names - North Ames<br>NoRidge - Northridge<br>NPkVill - Northpark Villa<br>NridgHt - Northridge Heights<br>NWAmes - Northwest Ames<br>OldTown - Old Town<br>SWISU - South & West of Iowa State University<br>Sawyer - Sawyer<br>SawyerW - Sawyer West<br>Somerst - Somerset<br>StoneBr - Stone Brook<br>Timber - Timberland<br>Veenker - Veenker|
|**condition_1**|*object*|Proximity to main road or railroad|Artery - Adjacent to arterial street<br>Feedr - Adjacent to feeder street<br>Norm - Normal<br>RRNn - Within 200' of North-South Railroad<br>RRAn - Adjacent to North-South Railroad<br>PosN - Near positive off-site feature--park, greenbelt, etc.<br>PosA - Adjacent to postive off-site feature<br>RRNe - Within 200' of East-West Railroad<br>RRAe - Adjacent to East-West Railroad|
|**condition_2**|*object*|Proximity to main road or railroad (if a second is present)|Proximity to main road or railroad|Artery - Adjacent to arterial street<br>Feedr - Adjacent to feeder street<br>Norm - Normal<br>RRNn - Within 200' of North-South Railroad<br>RRAn - Adjacent to North-South Railroad<br>PosN - Near positive off-site feature--park, greenbelt, etc.<br>PosA - Adjacent to postive off-site feature<br>RRNe - Within 200' of East-West Railroad<br>RRAe - Adjacent to East-West Railroad|
|**overall_qual**|*int*|Overall material and finish quality|1 - Very Poor <-> 10 - Very Excellent|
|**overall_cond**|*int*|Overall condition rating|1 - Very Poor <-> 10 - Very Excellent|
|**year_built**|*int*|Original construction date|year|
|**year_remod/add**|*int*|Remodel date (same as construction date if no remodeling or additions)|year|
|**roof_style**|*object*|Type of roof|Flat - Flat<br>Gable - Gable<br>Gambrel - Gabrel (Barn)<br>Hip - Hip<br>Mansard - Mansard<br>Shed - Shed|
|**roof_matl**|*object*|Roof material|ClyTile - Clay or Tile<br>CompShg - Standard (Composite) Shingle<br>Membran - Membrane<br>Metal - Metal<br>Roll - Roll<br>Tar&Grv - Gravel & Tar<br>WdShake - Wood Shakes<br>WdShngl - Wood Shingles|
|**exterior_1st**|*object*|Exterior covering on house|AsbShng - Asbestos Shingles<br>AsphShn - Asphalt Shingles<br>BrkComm - Brick Common<br>BrkFace - Brick Face<br>CBlock - Cinder Block<br>CemntBd - Cement Board<br>HdBoard - Hard Board<br>ImStucc - Imitation Stucco<br>MetalSd - Metal Siding<br>Other - Other<br>Plywood - Plywood<br>PreCast - PreCast<br>Stone - Stone<br>Stucco - Stucco<br>VinylSd - Vinyl Siding<br>WdSdng - Wood Siding<br>WdShing - Wood Shingles|
|**exterior_2nd**|*object*|Exterior covering on house (if more than one material)|AsbShng - Asbestos Shingles<br>AsphShn - Asphalt Shingles<br>BrkComm - Brick Common<br>BrkFace - Brick Face<br>CBlock - Cinder Block<br>CemntBd - Cement Board<br>HdBoard - Hard Board<br>ImStucc - Imitation Stucco<br>MetalSd - Metal Siding<br>Other - Other<br>Plywood - Plywood<br>PreCast - PreCast<br>Stone - Stone<br>Stucco - Stucco<br>VinylSd - Vinyl Siding<br>WdSdng - Wood Siding<br>WdShing - Wood Shingles|
|**mas_vnr_type**|*object*|Masonry veneer type|BrkCmn - Brick Common<br>BrkFace - Brick Face<br>CBlock - Cinder Block<br>None - None<br>Stone - Stone|
|**mas_vnr_area**|*float*|Masonry veneer area in square feet|sq ft|
|**exter_qual**|*int*|Exterior material quality|Ex - Excellent<br>Gd - Good<br>TA - Average/Typical<br>Fa - Fair<br>Po - Poor|
|**exter_cond**|*int*|Present condition of the material on the exterior|Ex - Excellent<br>Gd - Good<br>TA - Average/Typical<br>Fa - Fair<br>Po - Poor|
|**foundation**|*object*|Type of foundation|BrkTil - Brick & Tile<br>CBlock - Cinder Block<br>PConc - Poured Contrete<br>Slab - Slab<br>Stone - Stone<br>Wood - Wood|
|**bsmt_qual**|*int*|Height of the basement|Ex - Excellent (100+ inches)<br>Gd - Good (90-99 inches)<br>TA - Typical (80-89 inches)<br>Fa - Fair (70-79 inches)<br>Po - Poor (<70 inches)<br>NA - No Basement|
|**bsmt_cond**|*object*|General condition of the basement|Ex - Excellent<br>Gd - Good<br>TA - Typical - slight dampness allowed<br>Fa - Fair - dampness or some cracking or settling<br>Po - Poor - Severe cracking, settling, or wetness<br>NA - No Basement|
|**bsmt_exposure**|*int*|Walkout or garden level basement walls|Gd - Good Exposure<br>Av - Average Exposure (split levels or foyers typically score average or above)<br>Mn - Mimimum Exposure<br>No - No Exposure<br>NA - No Basement|
|**bsmtfin_type_1**|*object*|Quality of basement finished area|GLQ - Good Living Quarters<br>ALQ - Average Living Quarters<br>BLQ - Below Average Living Quarters<br>Rec - Average Rec Room<br>LwQ - Low Quality<br>Unf - Unfinshed<br>NA - No Basement|
|**bsmtfin_sf_1**|*float*|Type 1 finished square feet|sq ft|
|**bsmtfin_type_2**|*object*|Quality of second finished area (if present)|GLQ - Good Living Quarters<br>ALQ - Average Living Quarters<br>BLQ - Below Average Living Quarters<br>Rec - Average Rec Room<br>LwQ - Low Quality<br>Unf - Unfinshed<br>NA - No Basement|
|**bsmtfin_sf_2**|*float*|Type 2 finished square feet|sq ft|
|**bsmt_unf_sf**|*float*|Unfinished square feet of basement area|sq ft|
|**total_bsmt_sf**|*float*|Total square feet of basement area|sq ft|
|**heating**|*object*|Type of heating|Floor - Floor Furnace<br>GasA - Gas forced warm air furnace<br>GasW - Gas hot water or steam heat<br>Grav - Gravity furnace<br>OthW - Hot water or steam heat other than gas<br>Wall - Wall furnace|
|**heating_qc**|*int*|Heating quality and condition|Ex - Excellent<br>Gd - Good<br>TA - Average/Typical<br>Fa - Fair<br>Po - Poor|
|**electrical**|*object*|Electrical system|SBrkr - Standard Circuit Breakers & Romex<br>FuseA - Fuse Box over 60 AMP and all Romex wiring (Average)<br>FuseF - 60 AMP Fuse Box and mostly Romex wiring (Fair)<br>FuseP - 60 AMP Fuse Box and mostly knob & tube wiring (poor)<br>Mix - Mixed|
|**central_air**|*int*|Central air conditioning|Y/N|
|**first_flr_sf**|*int*|First Floor square feet|sq ft|
|**second_fl_sf**|*int*|Second floor square feet|sq ft|
|**low_qual_fin_sf**|*int*|Low quality finished square feet (all floors)|sq ft|
|**gr_liv_area**|*int*|Above grade (ground) living area square feet|sq ft|
|**bsmt_full_bath**|*float*|Basement full bathrooms|number|
|**bsmt_half_bath**|*float*|Basement half bathrooms|number|
|**full_bath**|*int*|Full bathrooms above grade|integer|
|**half_bath**|*int*|Half baths above grade|integer|
|**bedroom_abvgr**|*int*|Number of bedrooms above basement level|integer|
|**kitchen_abvgr**|*int*|Number of kitchens|integer|
|**kitchen_qual**|*int*|Kitchen quality|Ex - Excellent<br>Gd - Good<br>TA - Typical/Average<br>Fa - Fair<br>Po - Poor|
|**totrms_abvgrd**|*int*|Total rooms above grade (does not include bathrooms)|integer|
|**functional**|*object*|Home functionality rating|Typ - Typical Functionality<br>Min1 - Minor Deductions 1<br>Min2 - Minor Deductions 2<br>Mod - Moderate Deductions<br>Maj1 - Major Deductions 1<br>Maj2 - Major Deductions 2<br>Sev - Severely Damaged<br>Sal - Salvage only|
|**fireplaces**|*int*|Number of fireplaces|integer|
|**fireplace_qu**|*int*|Fireplace quality|Ex - Excellent - Exceptional Masonry Fireplace<br>Gd - Good - Masonry Fireplace in main level<br>TA - Average - Prefabricated Fireplace in main living area or Masonry Fireplace in basement<br>Fa - Fair - Prefabricated Fireplace in basement<br>Po - Poor - Ben Franklin Stove<br>NA - No Fireplace|
|**garage_type**|*object*|Garage location|2Types - More than one type of garage<br>Attchd - Attached to home<br>Basment - Basement Garage<br>BuiltIn - Built-In (Garage part of house - typically has room above garage)<br>CarPort - Car Port<br>Detchd - Detached from home<br>NA - No Garage|
|**garage_yr_blt**|*object*|Year garage was built|year|
|**garage_finish**|*int*|Interior finish of the garage|Fin - Finished<br>RFn - Rough Finished<br>Unf - Unfinished<br>NA - No Garage|
|**garage_cars**|*float*|Size of garage in car capacity|number|
|**garage_area**|*float*|Size of garage in square feet|sq ft|
|**garage_qual**|*int*|Garage quality|Ex - Excellent<br>Gd - Good<br>TA - Typical/Average<br>Fa - Fair<br>Po - Poor<br>NA - No Garage|
|**garage_cond**|*int*|Garage condition|Ex - Excellent<br>Gd - Good<br>TA - Typical/Average<br>Fa - Fair<br>Po - Poor<br>NA - No Garage|
|**paved_drive**|*int*|Paved driveway|Y - Paved<br>P - Partial Pavement<br>N - Dirt/Gravel|
|**wood_deck_sf**|*int*|Wood deck area in square feet|sq ft|
|**open_porch_sf**|*int*|Open porch area in square feet|sq ft|
|**enclosed_porch**|*int*|Enclosed porch area in square feet|sq ft|
|**three_ssn_porch**|*int*|Three season porch area in square feet|sq ft|
|**screen_porch**|*int*|Screen porch area in square feet|sq ft|
|**pool_area**|*int*|Pool area in square feet|sq ft|
|**pool_qc**|*int*|Pool quality|Ex - Excellent<br>Gd - Good<br>TA - Average/Typical<br>Fa - Fair<br>NA - No Pool|
|**fence**|*int*|Fence quality|GdPrv - Good Privacy<br>MnPrv - Minimum Privacy<br>GdWo - Good Wood<br>MnWw - Minimum Wood/Wire<br>NA - No Fence|
|**misc_feature**|*object*|Miscellaneous feature not covered in other categories|Elev - Elevator<br>Gar2 - 2nd Garage (if not described in garage section)<br>Othr - Other<br>Shed - Shed (over 100 SF)<br>TenC - Tennis Court<br>NA - None|
|**misc_val**|*int*|Value of miscellaneous feature|USD|
|**mo_sold**|*int*|Month sold|1 - January <-> 12 - December|
|**yr_sold**|*int*|Year sold|year|
|**sale_type**|*object*|Type of sale|WD - Warranty Deed - Conventional<br>CWD - Warranty Deed - Cash<br>VWD - Warranty Deed - VA Loan<br>New - Home just constructed and sold<br>COD - Court Officer Deed/Estate<br>Con - Contract 15% Down payment regular terms<br>ConLw - Contract Low Down payment and low interest<br>ConLI - Contract Low Interest<br>ConLD - Contract Low Down<br>Oth - Other|

## Conclusions & Recommendations

**Source Data**
Records from 2,050 home/building sales in Ames, IA from 2006 - 2010
80 pieces of building details including:
 - Years of construction, sale, and remodel
 - Neighborhood, proximity to transportation/parks & recreation
 - Building type and municipal subclass
 - Building materials for exterior, roofing, masonry
 - Number of rooms, area in sq. ft.
 - Utility details
 - Lot details such as size, shape, incline
 - Details on sale execution
 - Quality and condition ratings 

**Exploratory Data Analysis**
Look at data for completeness
 - Fix missing data if possible
 - Remove corrupted rows
Reshape for usability / accuracy
 - Convert years into ages
 - Turn Y/N into 1/0
Standardize category names/spellings
 - Identify outliers
 - Determine whether to keep or remove, and for which categories

**Feature Exploration**
Heat mapping - color-coded graphing of correlations between variables 
 - Variables with high positive and negative correlations have the biggest impact on modeling for target values

Pair plotting - scatter plots between variables and histograms of variable distributions
 - Visualize the nature of correlations between variables, identify non-normal distributions across variables

### Which features most affect sales prices?
_Feature_						_Corr._
 - Overall Quality 				(0.81)
 - Exterior Quality				(0.71)
 - Above-Grade Living Area  	(0.71)
 - Kitchen Quality				(0.69)
 - Garage Number of Cars		(0.66)
 - Garage Area					(0.65)
 - Total Basement Square Ft		(0.65)
 - First Floor Square Ft		(0.63)
 - Basement Quality				(0.62)
 - Age at Sale			       (-0.59)

### What modeling approaches yield the most accurate predictions?

**Dummy Variables**
Replacing categorical variables Each value gets its own binary 1/0 variable
Using dummy variable “has_garage” retains important detail
For “ms_subclass”, dummies can represent shared qualities (e.g., “is_post_war”, “is_two_story”, etc.)

**Ordinal Values**
Assign ordinal values to “quality” and other scaled variables
Change from text categories into numerical values for model processing
“Ex”, “Gd”, “Av”, “Fr”, “Po” become 5, 4, 3, 2, 1
Mapped in addition to creating dummy categories, and estimated values based on materials

**Polynomials**
Linear regression models can be enhanced with interactions and polynomial variables
Added interaction and polynomial variables for the top-14 correlated categories against all categories
Added two cubic values by top-14 correlations
 - Overall_qual Gr_liv_area
 - Exter_qual Gr_liv_area

**Model Execution**
Train / Test Split
 - Separate portion of data as control group to assess model performance before submitting
Scaling
 - Using tools in Python library SciKit-Learn, convert numeric values to standard deviation of all values for a variable
Power Transform
 - Tools convert variables logarithmically to even out skewed distributions
Regularization
 - While modeling, we used two types of regularizing models: Ridge and Lasso
 - Models impose costs on using too many variables to improve accuracy
 - Lasso reduces predictive coefficients to zero quickly, helping to identify unneeded variables
Assessment
 - Test models using Cross-Validation Scoring to determine R^2 score
 - Comparing R^2 scores of training and test data tells modeler about fit and predictive accuracy

### What values did the model find most important?

Final Ridge model used 111 variables.
The variables with the largest coefficients had the biggest impact on the model’s predictions.

**Top 10 Model Coefficients**
1. Total Basement SqFt x Basement Quality
2. Overall Quality^2
3. Above Grade Living Area x Fireplace Quality
4. Above Grade Living Area x Basement Quality
5. Kitchen Quality x Garage Area
6. Overall Quality x Exterior Quality
7. Overall Quality x Kitchen Quality
8. Kitchen Quality x Garage Cars
9. Overall Quality x Garage Area
10. Overall Condition

**Final Model Details**
Regularization: Ridge
Scaling: StandardScaler
Power: PowerTransformer on variables between 1 and 30 absolute skewness
Approach: Initially built “kitchen sink” model and used Lasso with manual alpha to manage Convergence Errors
Removed zero-coefficient values from LassoCV to create Ridge model

Cross-Validation R^2 Score 
 - 0.9107
R^2 Score on Test Prediction 
 - 0.9214

**Engineered Features**

Custom Garage Dummies by Percentile Group
 - Created a loop that when given a percent number, automatically broke all garages into categories based on age, and assigned descriptive title to DataFrame

Custom Neighborhood Dummies by Percentile Group
 - Created a loop to group neighborhoods by median sale price by percentile, and assigned value ranges in DataFrame column names

Dictionary Ordinal Assignment
 - Used two dictionaries to allow adjustment of ordinal values and mass application to DataFrame

Partial Heatmap Loop
 - Configured Seaborn heatmap to show variables correlation 12 at a time against 6 key variables

Partial PowerTransform
 - Created separate DataFrame to limit PowerTransform to necessary distributions (resolved divide-by-zero errors)

### Recommendations
**What does this mean for Zillow?**
 - The Ames, IA model can serve as a starting point for similar markets
 - This model can be further optimized using GridSearch hyperparameter techniques
 - An iterative modeling approach will continue to improve predictive results in all markets
 - Additional research should be done into quantifying materials categories


## Data Sources

Kaggle Project 2 Ames, IA Data: https://www.kaggle.com/c/dsi-us-6-project-2-regression-challenge/data
 - train.csv
 - test.csv

Ames, IA Wikipedia: https://en.wikipedia.org/wiki/Ames,_Iowa
Roofing Styles: https://www.roofcostestimator.com/top-15-roof-types-and-their-pros-cons/
Siding Material Prices: http://www.sidingpriceguides.com/siding-comparison.html
Stucco Price Guide: https://www.homeadvisor.com/cost/siding/stucco-siding/