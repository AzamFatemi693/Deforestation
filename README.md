# Deforestation Exploration
This repository contains the code and resources for the Deforestation Exploration project, available on Udacity. The project aims to explore and analyze deforestation patterns using real-world satellite imagery and geospatial data.

# Project Overview
You’re a data analyst for ForestQuery, a non-profit organization, on a mission to reduce deforestation around the world and which raises awareness about this important environmental topic.
Your executive director and her leadership team members are looking to understand which countries and regions around the world seem to have forests that have been shrinking in size, and also which countries and regions have the most significant forest area, both in terms of amount and percent of total area. The hope is that these findings can help inform initiatives, communications, and personnel allocation to achieve the largest impact with the precious few resources that the organization has at its disposal.
You’ve been able to find tables of data online dealing with forestation as well as total land area and region groupings, and you’ve brought these tables together into a database that you’d like to query to answer some of the most important questions in preparation for a meeting with the ForestQuery executive team coming up in a few days. Ahead of the meeting, you’d like to prepare and disseminate a report for the leadership team that uses complete sentences to help them understand the global deforestation overview between 1990 and 2016.

# Getting Started

 To get started with the Deforestation Exploration project, follow these steps:
 https://learn.udacity.com/paid-courses/cd12500/lessons/bf31b778-29ab-4860-adec-153cc6756d45/concepts/3c8a2dab-a727-47be-a27b-30bf6551c272
1. Visit the project page on Udacity at Deforestation Exploration.
1. Enroll in the course if necessary and access the project materials provided by Udacity.
1. Read through the project instructions, requirements, and guidelines to familiarize yourself with the objectives and scope of the project.
4. Download the necessary dataset and resources provided by Udacity.
5. Set up your development environment with the required tools and libraries mentioned in the project instructions.
6. Follow the project instructions and complete the tasks outlined, which may include data preprocessing, exploratory data analysis, visualization, and hypothesis testing.
7. Write code and create visualizations to analyze the deforestation patterns in the dataset.
8. Document your findings, insights, and any conclusions you draw from the analysis.
9. Review and refine your code, analysis, and documentation to ensure clarity and accuracy.
10. Submit your project for evaluation according to the instructions provided by Udacity.

# Steps to Complete

1. Create a View called “forestation” by joining all three tables - forest_area, land_area and regions in the workspace.
2. The forest_area and land_area tables join on both country_code AND year.
3. The regions table joins these based on only country_code.
4. In the ‘forestation’ View, include the following:
  ...All of the columns of the origin tables
  ...A new column that provides the percent of the land area that is designated as forest.
5. Keep in mind that the column forest_area_sqkm in the forest_area table and the land_area_sqmi in the land_area table are in different units (square kilometers and square miles, respectively), so an adjustment will need to be made in the calculation you write (1 sq mi = 2.59 sq km).

# Resources and Dependencies

The project materials provided by Udacity should include all the necessary resources, such as the dataset, code templates, and documentation. The specific dependencies and libraries required for the project will also be mentioned in the project instructions or within the code files.
Make sure to review the project instructions and documentation carefully to ensure you have all the required resources and dependencies to complete the Deforestation Exploration project successfully.


# Copyright
While the data used & tools are free-to-use & open-source, I will appreciate if the below credits are mentioned if you find using my work & time devoted to this project useful, and you intend to share it in full/parts publicly:

Author: Azam Fatemi

LinkedIn: https://www.linkedin.com/in/azam-fatemi

Github: https://github.com/AzamFatemi693/Deforestation
