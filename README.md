# School District Broad Analysis
In this training project, school board data is analysis based on math & reading score. 
 There are two data resources csv formats; school data & student data. First of all, we made pandas DataFrame of each resources by the below code;

		 - school_data_df = pd.read_csv(school_data_to_load)
student_data_df = pd.read_csv(student_data_to_load)

Then they were merged together to make one complete data resource.

	 - school_data_complete_df = pd.merge(student_data_df, school_data_df, how="left", on=["school_name", "school_name"])

Second, Before starting our analysis, if it might need, we should consider our data based and clean. In this project student name column had to cleaned (there are some prefixes and suffixes for some students name, they were omitted from student's name column). The below codes helped us in this stage;

	 - prefixes_suffixes = ["Dr. ", "Mr. ","Ms. ", "Mrs. ", "Miss ", " MD", " DDS", " DVM", " PhD"]
	 -  student_data_df["student_name"] = student_data_df["student_name"].str.replace(word,"")

Then, we understood that Thomas High School ninth graders are not correct and we shall omit their data from our analysis. Therefore; we replace them with NaNs. The below codes were used;

	 - student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th"),["reading_score"]]=np.nan

	 - student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & (student_data_df["grade"] == "9th"),["math_score"]]=np.nan

##  School Summary
Overall schools performance was calculated based on the below factors;
			-	Total Schools
			-	Total Students
			-	Total Budget
			-	Average Math Score
			-	Average Reading Score
			-	% Passing Math
			-	% Passing Reading
			-	% Overall Passing
passing math & reading score is math score equal or greater than 70. 
In School summery, all above factors were calculated for each school and because Thomas school ninth graders were replaced with NaNs, therefore this school data had to updated.  The below code was used to make this school data frame based on  grades 10, 11 & 12.

	 - thomas_student = school_data_complete_df.loc[(school_data_complete_df["grade"]!="9th") & (school_data_complete_df["school_name"] == "Thomas High School")]

## High and Low Performing Schools 
In this part, high & low performing schools were displayed based on % Overall Passing score.
Five high performing schools are;

	 - Cabrera High School 
	 - Thomas High School 
	 - Griffin High School
	 - Wilson High School
	 - Pena High School
Five high performing schools are;

	 - Rodriguez High School
	 - Figueroa High School
	 - Huang High School
	 - Hernandez High School 
	 - Johnson High School
Moreover, each school performance was calculated based on math & reading scores and grades.

	 1. Prepare series of each grade.
	 2. In each grade series, grouped school name and average of math/reading score(groupby code was used in this part)
 For example, below codes were used for grade 9th:
 

	 - ninth_graders = school_data_complete_df[(school_data_complete_df["grade"] == "9th")]
	-	ninth_graders_math = ninth_graders.groupby(["school_name"]).mean()["math_score"].map("{:,.1f}".format)
	-	ninth_graders_reading = ninth_graders.groupby(["school_name"]).mean()["reading_score"].map("{:,.1f}".format)

## Scores by School Spending
In this part,  math score and reading score were categorized based on spending budget per student. we used bins forms for this part. First of all, we calculated some statistics data by .describe( ). We used Max & Min and Std  to define our bins.

	 - group_names = ["<$584", "$585-629", "$630-644", "$645-675"]
	 - 
Then, average of  metrics were calculated as follows;

	 - spending_math_scores = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["Average Math Score"].map("{:,.1f}".format)
	 - spending_reading_scores = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["Average Reading Score"].map("{:,.1f}".format)
	 - spending_passing_math = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["% Passing Math"].map("{:,.0f}".format)
	 - spending_passing_reading = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["% Passing Reading"].map("{:,.0f}".format)
	 - overall_passing_spending = per_school_summary_df.groupby(["Spending Ranges (Per Student)"]).mean()["% Overall Passing"].map("{:,.0f}".format)List item

## Scores by School Size
In this part, schools performance were analyzed based on school size (number of student in each schools). First of all, we calculated some statistics data by .describe( ). We used Max & Min and Std  to define our bins.

	 - group_names = ["Small (<1000)", "Medium (1000-2000)", "Large (2000-5000)"]

Then, average of  metrics were calculated as follows;

	 - spending_math_scores = per_school_summary_df.groupby(["Spending Ranges (Per size)"]).mean()["Average Math Score"].map("{:,.1f}".format)
	 - spending_reading_scores = per_school_summary_df.groupby(["Spending Ranges (Per size)"]).mean()["Average Reading Score"].map("{:,.1f}".format)
	 - spending_passing_math = per_school_summary_df.groupby(["Spending Ranges (Per size)"]).mean()["% Passing Math"].map("{:,.0f}".format)
	 - spending_passing_reading = per_school_summary_df.groupby(["Spending Ranges (Per size)"]).mean()["% Passing Reading"].map("{:,.0f}".format)
	 - overall_passing_spending = per_school_summary_df.groupby(["Spending Ranges (Per size)"]).mean()["% Overall Passing"].map("{:,.0f}".format)

## Scores by School Type
There are two kinds of school in this project; 

 - Charter
 - District
 
 The metrics were calculated in above categories, .groupby() used for this part.
		
	 - type_math_scores = per_school_summary_df.groupby(["School Type"]).mean()["Average Math Score"].map("{:,.1f}".format)
	 - type_reading_scores = per_school_summary_df.groupby(["School Type"]).mean()["Average Reading Score"].map("{:,.1f}".format)
	 - type_passing_math = per_school_summary_df.groupby(["School Type"]).mean()["% Passing Math"].map("{:,.0f}".format)
	 - type_passing_reading = per_school_summary_df.groupby(["School Type"]).mean()["% Passing Reading"].map("{:,.0f}".format)
	 - type_overall_passing = per_school_summary_df.groupby(["School Type"]).mean()["% Overall Passing"].map("{:,.0f}".format)
