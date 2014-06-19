#Code Book For The Tiddy Data#

The second Tiddy data set includes 180 columns and 66 rows. The column names stand for 180 combinations of 6 activities and 30 subjects. The row names stand for 66 variables include mean or std. All the data in the tidy data set is the average of each variable for each activity and each subject. 

The following transforming steps were taken to get the tidy data sets:

1. The original data were transformed to combinations of the training and the test data set for X, y and subject. 
2. In the X data set, the measurements on the mean and standard deviation for each measurement were extracted to form a sub data set with 66 variables (columns). 
3. The integral acitivity names in the activity (y) data set were transformed to descriptive activity name. 
4. The sub data set with 66 variables, the activity data set, the subject data set were combined into a single data set. 
5. Descriptive names of the 66 variables were read from the feature data set and asigned to each column of the data set got in the last step as column names. The last two columns were named "activity" and "subject". The result data set was saved in file "tidydata.txt".
6. The tidydata set was splited according to activity and subject.
7. Column means were calculated for each variable in each of the elements in the splited data set.
8. The resulting second tidy data set was saved in file "tidydata2.txt".
