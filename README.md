Tidy-Data-for-Samsung-Data
==========================

Script and Code Book

X_train<-read.table("./UCI HAR Dataset/train/X_train.txt")
y_train<-read.table("./UCI HAR Dataset/train/y_train.txt")
subject_train<-read.table("./UCI HAR Dataset/train/subject_train.txt")
X_test<-read.table("./UCI HAR Dataset/test/X_test.txt")
y_test<-read.table("./UCI HAR Dataset/test/y_test.txt")
subject_test<-read.table("./UCI HAR Dataset/test/subject_test.txt")
X<-rbind(X_test, X_train)
X_sub<-X[,c(1:6,41:46,81:86,121:126,161:166,201:202,214:215, 227:228,240:241,253:254,266:271,345:350,424:429,503:504,516:517,529:530,542:543)]
y<-rbind(y_test,y_train)
subject<-rbind(subject_test,subject_train)
i<-0
for(i in 1:nrow(y)){
	if(y[i,1]==1){y[i,1]<-"WALKING"}
	if(y[i,1]==2){y[i,1]<-"WALKING_UPSTAIRS"}
	if(y[i,1]==3){y[i,1]<-"WALKING_DOWNSTAIRS"}
	if(y[i,1]==4){y[i,1]<-"SITTING"}
	if(y[i,1]==5){y[i,1]<-"STANDING"}
	if(y[i,1]==6){y[i,1]<-"LAYING"}
}
data<-cbind(X_sub,y,subject)
features<-read.table("./UCI HAR Dataset/features.txt")
f<-features$V2[c(1:6,41:46,81:86,121:126,161:166,201:202,214:215, 227:228,240:241,253:254,266:271,345:350,424:429,503:504,516:517,529:530,542:543)]
f<-as.character(f)
f<-c(f,"activity","subject")
names(data)<-f
splited<-split(data,list(data$subject,data$activity))
data2<-sapply(splited,function(x) colMeans(x[,1:66]))
write.table(data,"./UCI HAR Dataset/tidydata.txt")
write.table(data2,"./UCI HAR Dataset/tidydata2.txt")
