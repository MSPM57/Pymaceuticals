# Unit 5 Homework: The Power of Plots

What good is data without a good plot to tell the story?

In this homework assignment, you’ll apply what you've learned about Matplotlib and to a real-world situation and dataset.
## Background

You've just  joined Pymaceuticals Inc., a new pharmaceutical company that specializes in anti-cancer pharmaceuticals. Recently, it began screening for potential treatments for squamous cell carcinoma (SCC), a commonly occurring form of skin cancer.

As a senior data analyst at the company, you've been given access to the complete data from their most recent animal study. In this study, 249 mice identified with SCC tumor growth were treated with a variety of drug regimens. Over the course of 45 days, tumor development was observed and measured. The purpose of this study was to compare the performance of Pymaceuticals' drug of interest, Capomulin, versus the other treatment regimens. 

The executive team has tasked you with generating all of the tables and figures needed for the technical report of the study. They have also asked for a top-level summary of the study results.

## Instructions

Your tasks are to do the following:

* Prepare the data.

* Generate summary statistics.

* Create bar charts and pie charts.

* Calculate quartiles, find outliers, and create a box plot.

* Create a line plot and a scatter plot.

* Calculate correlation and regression. 

* Submit your final analysis. 

### Prepare the Data

1. Run the provided package dependency and data imports, and then merge the `mouse_metadata` and `study_results` DataFrames into a single DataFrame.
  record from mouse_metadata
	Mouse ID	Drug Regimen	Sex	Age_months	Weight (g)
    	k403	Ramicane	    Male	21	      16    

  record from study_results file
  Mouse ID	Timepoint	Tumor Volume (mm3)	Metastatic Sites
  	b128	    0	      45.0	              0

Sample of 5 records from mouse_metadata file merged with study_results file.

Mouse ID	Drug Regimen	Sex	Age_months	Weight (g)	Timepoint	Tumor Volume (mm3)	Metastatic Sites
0	k403	Ramicane	Male	21	16	0	45.000000	0
1	k403	Ramicane	Male	21	16	5	38.825898	0
2	k403	Ramicane	Male	21	16	10	35.014271	1
3	k403	Ramicane	Male	21	16	15	34.223992	1
4	k403	Ramicane	Male	21	16	20	32.997729	1

2. Display the number of unique mice IDs in the data, and then check for any mouse ID with duplicate time points. Display the data associated with that mouse ID, and then create a new DataFrame where this data is removed. Use this cleaned DataFrame for the remaining step.

number of duplicated records for a mouse

Mouse ID	Drug Regimen	Sex	Age_months	Weight (g)	Timepoint	Tumor Volume (mm3)	Metastatic Sites
909	g989	Propriva	Female	21	26	0	45.000000	0
911	g989	Propriva	Female	21	26	5	47.570392	0
913	g989	Propriva	Female	21	26	10	49.880528	0
915	g989	Propriva	Female	21	26	15	53.442020	0
917	g989	Propriva	Female	21	26	20	54.657650	1

clean dataframe

Mouse ID              1888
Drug Regimen          1888
Sex                   1888
Age_months            1888
Weight (g)            1888
Timepoint             1888
Tumor Volume (mm3)    1888
Metastatic Sites      1888

3. Display the updated number of unique mice IDs.
Mouse ID               249
Drug Regimen            10
Sex                      2
Age_months              24
Weight (g)              16
Timepoint               10
Tumor Volume (mm3)    1640
Metastatic Sites         5
dtype: int64



### Generate Summary Statistics


	        mean	    median    var	      std     	sem
Drug Regimen					
Capomulin	40.675741	41.557809	24.947764	4.994774	0.329346
Ceftamin	52.591172	51.776157	39.290177	6.268188	0.469821
Infubinol	52.884795	51.820584	43.128684	6.567243	0.492236
Ketapril	55.235638	53.698743	68.553577	8.279709	0.603860
Naftisol	54.331565	52.509285	66.173479	8.134708	0.596466
Placebo	54.033581	52.288934	61.168083	7.821003	0.581331
Propriva	52.320930	50.446266	43.852013	6.622085	0.544332
Ramicane	40.216745	40.673236	23.486704	4.846308	0.320955
Stelasyn	54.233149	52.431737	59.450562	7.710419	0.573111
Zoniferol	53.236507	51.818479	48.533355	6.966589	0.516398

Create two summary statistics DataFrames:

    * For the first table, use the `groupby` method to generate the mean, median, variance, standard deviation, and SEM of the tumor volume for each drug regimen. This should result in five unique series objects. Combine these objects into a single summary statistics DataFrames.

    * For the second table, use the `agg` method to produce the same summary statistics table by using a single line of code.

### Create Bar Charts and a Pie Charts

1. Generate two bar plots. Both plots should be identical and show the total number of timepoints for all mice tested for each drug regimen throughout the course of the study.

    * Create the first bar plot by using Pandas's `DataFrame.plot()` method.
#see png file ==> Bar Chart Using Pandas

 

# Generate a bar plot showing the total number of timepoints for all mice tested for each drug regimen using Pandas.

#see png file ==> Bar Chart Using Matplotlib



# Generate a pie plot showing the distribution of female versus male mice using Pandas

#see png file ==> Pie Chart Showing Female vs Male Using Pandas

 # Generate a pie plot showing the distribution of female versus male mice using pyplot

#see png file ==> PIe Chart Showing Female vs Male Using pyplot

### Calculate Quartiles, Find Outliers, and Create a Box Plot 

1. Calculate the final tumor volume of each mouse across four of the most promising treatment regimens: Capomulin, Ramicane, Infubinol, and Ceftamin. Then, calculate the quartiles and IQR and determine if there are any potential outliers across all four treatment regimens. Follow these substeps:

    * Create a grouped DataFrame that shows the last (greatest) time point for each mouse. Merge this grouped DataFrame with the original cleaned DataFrame.

    * Create a list that holds the treatment names, as well as a second, empty list to hold the tumor volume data.

    * Loop through each drug in the treatment list, locating the rows in the merged DataFrame that correspond to each treatment. Append the resulting final tumor volumes for each drug to the empty list. 

    * Determine outliers by using the upper and lower bounds, and then print the results.

#Start by getting the last (greatest) timepoint for each mouse
# 	Mouse ID	Drug Regimen	Sex	Age_months	Weight (g)	Timepoint	Tumor Volume (mm3)	Metastatic Sites
0	k403	    Ramicane	    Male	21	      16	        0	        45.000000	          0
1	k403	    Ramicane	    Male	21	      16	        5	        38.825898	          0
2	k403	    Ramicane	    Male	21	      16	        10	      35.014271	          1
3	k403	    Ramicane	    Male	21	      16	        15	      34.223992         	1

4	k403	    Ramicane	    Male	21	      16	        20	      32.997729         	1
...	...	...	...	...	...	...	...	...
1888	z969	Naftisol	    Male	9	        30	        25	      63.145652         	2
1889	z969	Naftisol	    Male	9	        30	        30	      65.841013	          3
1890	z969	Naftisol	    Male	9	        30	        35	      69.176246	          4
1891	z969	Naftisol	    Male	9	        30	        40	      70.314904	          4
1892	z969	Naftisol	    Male	9	        30	        45	      73.867845	          4

1888 rows × 8 columns
 #Merge this group df with the original dataframe to get the tumor volume at the last timepoin##
	Mouse ID	Timepoint	Drug Regimen	Sex	Age_months	Weight (g)	Tumor Volume (mm3)	Metastatic Sites
0	a203	    45	      Infubinol	    Female	20	    23	        67.973419	          2
1	a251	    45	      Infubinol	    Female	21	    25	        65.525743	          1
2	a262	    45	      Placebo	      Female	17	    29	        70.717621         	4
3	a275	    45	      Ceftamin	    Female	20	    28	        62.999356	          3
4	a366	    30	      Stelasyn	    Female	16	    29	        63.440686	          1
...	...	...	...	...	...	...	...	...
243	z435	  10	      Propriva	    Female	12	    26	        48.710661	          0
244	z578	  45	      Ramicane	    Male	  11	    16	        30.638696	          0
245	z581	  45	      Infubinol	    Female	24	    25	        62.754451	          3
246	z795	  45	      Naftisol	    Female	13	    29	        65.741070	          3
247	z969	  45	      Naftisol	    Male	  9	      30	        73.867845	          4
248 rows × 8 columns



    
2. Using Matplotlib, generate a box plot of the final tumor volume for all four treatment regimens. Highlight any potential outliers in the plot by changing their color and style.

  **Hint**: All four box plots should be within the same figure. Use this [Matplotlib documentation page](https://matplotlib.org/gallery/pyplots/boxplot_demo_pyplot.html#sphx-glr-gallery-pyplots-boxplot-demo-pyplot-py) for help with changing the style of the outliers.


# Generate a box plot of the final tumor volume of each mouse across four regimens of interest   


  see file ==> Box Plot of Final Tumor Volumne for Four Treatment Regimens.png
### Create a Line Plot and a Scatter Plot


1. Select a mouse that was treated with Capomulin and generate a line plot of tumor volume vs. time point for that mouse.

see file ==> Line Plot for Mouse Treated with Capomulin Drug Regimen.png

2. Generate a scatter plot of tumor volume versus mouse weight for the Capomulin treatment regimen.

see file ==> Scatter Plot of Tumor Volume for Mouse Weight with Capomulin Treament Regimen.png

### Calculate Correlation and Regression

1. Calculate the correlation coefficient and linear regression model between mouse weight and average tumor volume for the Capomulin treatment. 

2. Plot the linear regression model on top of the previous scatter plot.

# see  file ==> Regression Model of Averae Tumor Volume Comparted to Weight of the Mouse.png

### Submit Your Final Analysis

Review all the figures and tables that you generated in this assignment. Write at least three observations or inferences that can be made from the data. Include these observations at the top of your notebook.

## Hints and Considerations

* Use the code comments in the provided starter file to guide you through this assignment. 

* Use proper labeling for your plots, that is, include plot titles, axis labels, legend labels, _x_-axis and _y_-axis limits, etc.

* While working on this assignment, refer to Stack Overflow and the Matplotlib documentation as needed. These are essential tools in every data analyst's tool belt.

* Remember that there are many ways to approach a data problem. One way to break up your task into micro tasks. For example, ask yourself questions like the following:

  * How does my DataFrame need to be structured in order to have the right _x_-axis and _y_-axis?

  * How do I build a basic scatter plot?

  * How do I add a label to a scatter plot?

  * Where in the DataFrame can I find the names that will go into the labels?

 
* Get help when you need it! Your instructional team is here to help.
## Rubric

[Unit 5 Homework Rubric](https://docs.google.com/document/d/1ZZ0lFGHqKwVdqjTCfynY2FSiswuOMBVi9An7oWeg344/edit?usp=sharing)

- - -

## References

Mockaroo, LLC. (2021). Realistic Data Generator. [https://www.mockaroo.com/](https://www.mockaroo.com/)

- - -

© 2022 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.

My analysis:

1. Out of 10 Drug Regimens the 4 focused on were regimens: Capomulin, Ramicane  Infubinol and Ceftamin  in studying tumors in mice over a 45 day treament period
2. The best of the four regimens was Capomulin; a line chart showed tumor size decreased over the study and the sex of them mice was split almost in half so as not to sway the study
3. The worse drug was Propriva was worst then the Placebo
3. The correlation of the size of the tumor compared to the weight of the mouse using Capomulin was 84%;  suggesting the use of the Capomulin regimen showed a relationship that the tumor size was lower as the mouse weighed less.  
   