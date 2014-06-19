Tidy-Data-for-Samsung-Data
==========================
# read the training and test files from the "UCI HAR Dataset" folder into separate objects 
X_train<-read.table("./UCI HAR Dataset/train/X_train.txt")	
y_train<-read.table("./UCI HAR Dataset/train/y_train.txt")	
subject_train<-read.table("./UCI HAR Dataset/train/subject_train.txt")	
X_test<-read.table("./UCI HAR Dataset/test/X_test.txt")			
y_test<-read.table("./UCI HAR Dataset/test/y_test.txt")		
subject_test<-read.table("./UCI HAR Dataset/test/subject_test.txt")

# combind the test and training data sets into one data set by combining the rows #
X<-rbind(X_test, X_train)

# Extracts only the measurements on the mean and standard deviation for each measurement #
X_sub<-X[,c(1:6,41:46,81:86,121:126,161:166,201:202,214:215, 227:228,240:241,253:254,266:271,345:350,424:429,503:504,516:517,529:530,542:543)]

# combind the test and training labels into one label data set by combining the rows #
y<-rbind(y_test,y_train)

# combind the test and training subject data sets into a single subject data set by combining the rows #
subject<-rbind(subject_test,subject_train)

# Uses descriptive activity names to name the activities in the label data set #
i<-0	
for(i in 1:nrow(y)){	
	if(y[i,1]==1){y[i,1]<-"WALKING"}	
	if(y[i,1]==2){y[i,1]<-"WALKING_UPSTAIRS"}	
	if(y[i,1]==3){y[i,1]<-"WALKING_DOWNSTAIRS"}	
	if(y[i,1]==4){y[i,1]<-"SITTING"}	
	if(y[i,1]==5){y[i,1]<-"STANDING"}	
	if(y[i,1]==6){y[i,1]<-"LAYING"}		
}

# combind the data set with the label set and suject set by combining the columns #
data<-cbind(X_sub,y,subject)

# read the features file to a object called "features" #
features<-read.table("./UCI HAR Dataset/features.txt")

# Extracts only the features for each measurement that has been extracted and put in the "data" objective #
f<-features$V2[c(1:6,41:46,81:86,121:126,161:166,201:202,214:215, 227:228,240:241,253:254,266:271,345:350,424:429,503:504,516:517,529:530,542:543)]

# change the class of all the feature names into "character" and stored in the "f" object #
f<-as.character(f)

# add "activity" and "subject" m into the object f as characters #
f<-c(f,"activity","subject")

# Appropriately labels the data set with descriptive variable names #
names(data)<-f

# Write the subseted, combined and labled data set "data" into a txt file #
write.table(data,"./UCI HAR Dataset/tidydata.txt")

# split the "data" data set by suject and activity name #
splited<-split(data,list(data$subject,data$activity))

# Creates a second, independent tidy data set with the average of each variable for each activity and each subject #
data2<-sapply(splited,function(x) colMeans(x[,1:66]))

# Write the second independent tidy data set "data2" into another txt file #
write.table(data2,"./UCI HAR Dataset/tidydata2.txt")
