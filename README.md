Getting-and-Cleaning-Data
=========================

The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. The goal is to prepare tidy data that can be used for later analysis. You will be graded by your peers on a series of yes/no questions related to the project. You will be required to submit: 1) a tidy data set as described below, 2) a link to a Github repository with your script for performing the analysis, and 3) a code book that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md. You should also include a README.md in the repo with your scripts. This repo explains how all of the scripts work and how they are connected.


You should create one R script called run_analysis.R that does the following.
Merges the training and the test sets to create one data set.
Extracts only the measurements on the mean and standard deviation for each measurement. 
Uses descriptive activity names to name the activities in the data set
Appropriately labels the data set with descriptive activity names. 
Creates a second, independent tidy data set with the average of each variable for each activity and each subject. 


# 1- Setting working directory
setwd("C:/Users/almenard/Desktop/Coursera - Data Science/Getting and Cleaning the Data/programming assignment/UCI HAR Dataset")




# 2- Reading Data
# 2.1- Reading ID Values
idtest <- read.table("./test/subject_test.txt", header=F, as.is=T, col.names=c("ID"))
idtrain<- read.table("./train/subject_train.txt", header=F, as.is=T, col.names=c("ID"))

#2.2 Reading the feature file
feature <- read.table("./features.txt", header=F, as.is=T, col.names=c("number", "feature"))

# 2.3- Reading Measurements
xtest <- read.table("./test/x_test.txt", header=F, as.is=T, col.names=c(feature$feature))
xtrain<- read.table("./train/x_train.txt", header=F, as.is=T, col.names=c(feature$feature))

# 2.4- Reading activity
ytest <- read.table("./test/y_test.txt", header=F, as.is=T, col.names=c("Activity_Label"))
ytrain<- read.table("./train/y_train.txt", header=F, as.is=T, col.names=c("Activity_Label"))

# 2.5- Reading activity Label
activitylabel <- read.table("./activity_labels.txt", header=F, as.is=T, col.names=c("Activity_Label", "Activity"))


# 3- Reshaping data
# 3.1- Generating Rando ID dataset
idtest1 <- data.frame(rando = "test", ID = c(2,4,9,10,12,13,18,20,24))
idtrain1 <- data.frame(rando = "train", ID = c(1,3,5,6,7,8,11,14,15,16,17,19,21,22,23,25,26,27,28,29,30))
idall <- rbind(idtest1, idtrain1)

#3.2- Merging test and train dataset
testdataset <- cbind(idtest, ytest, xtest)
traindataset <- cbind(idtrain, ytrain, xtrain)
alldataset <- rbind(testdataset, traindataset)

#4 Calculating descriptive_stat
stat_mean <- aggregate(x = alldataset, by = list(alldataset$ID, alldataset$Activity_Label), FUN = "mean")
stat_sd <- aggregate(x = alldataset, by = list(alldataset$ID, alldataset$Activity_Label), FUN = "sd")

#5 Reshaping to get final tidy data
#5.1 calculating meand and sd
stat_meanfinal <- data.frame(stat = "mean", stat_mean)
stat_sdfinal <- data.frame(stat = "sd", stat_sd)
stat_final <- rbind(stat_meanfinal, stat_sdfinal)

#5.2 Droping 2 columns and renaming replacement columns
drops <- c("ID","Activity_Label") 
stat_final_clean <- stat_final[,!(names(stat_final) %in% drops)]
library(plyr)
stat_final_cleanrenamed <- rename(stat_final_clean, c("Group.1"="ID", "Group.2"="Activity_Label"))

#5.3 Merging Activity info
final_dataset <- merge(activitylabel,stat_final_cleanrenamed)

#5.4 Merging Rando Info
tidy_data <- merge(idall, final_dataset)


#6 Saving to file original tidy dataset with train and test info
write.csv(tidy_data, "tidy_data.csv")
write.table(tidy_data, "tidy_data.txt")

