# DataCleansing
Data Cleansing

x_train <- read.table("./X_train.txt")
y_train <- read.table("./y_train.txt")
subject_train <- read.table("./subject_train.txt")
x_train <- read.table("./X_train.txt")
y_train <- read.table("./y_train.txt")
subject_train <- read.table("./subject_train.txt")
x_test <- read.table("./X_test.txt")
y_test <- read.table("./y_test.txt")
subject_test <- read.table("./subject_test.txt")
features <- read.table("./features.txt", header = FALSE)
activity_labels = read.table("./activity_labels.txt", header = FALSE)
subject_data <- rbind(subject_train, subject_test)
activity_data <- rbind(y_train, y_test)
features_data <- rbind(x_train, x_test)
names(subject_data)<-c("subject")
names(activity_data)<- c("activity")
names(features_data)<- features$V2
data <- cbind(subject_data, activity_data)
all_data <- cbind(features_data, data)
subset_feature <-features$V2[grep("mean\\(\\)|std\\(\\)", features$V2)]
subset_all_data <-c(as.character(subset_feature), "subject", "activity" )
all_data<-subset(all_data, select = subset_all_data)
all_data
all_data$activity<-factor(all_data$activity,labels=activity_labels[,2])
head(all_data$activity,10)
names(all_data)<-gsub("^t", "time", names(all_data))
names(all_data)<-gsub("^f", "frequency", names(all_data))
names(all_data)<-gsub("^f", "frequency", names(all_data))
names(all_data)<-gsub("Acc", "Accelerometer", names(all_data))
names(all_data)<-gsub("Gyro", "Gyroscope", names(all_data))
names(all_data)<-gsub("Mag", "Magnitude", names(all_data))
names(all_data)<-gsub("BodyBody", "Body", names(all_data))
all_data2<- aggregate(. ~subject + activity, all_data, mean)
all_data2<- all_data2[order(all_data2$subject,all_data2$activity),]
write.table(all_data2, file = "tidydata.txt",row.name=FALSE)
savehistory("C:/Users/donye/Desktop/test4.Rhistory")

