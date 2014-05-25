# 2- Reading Data
# 2.1- Reading ID Values
idtest = IDs from test group 
## idtrain = IDs from train group

#2.2 Reading the feature file
feature = List of all features

# 2.3- Reading Measurements
xtest = Observed measures from test group
xtrain = Observed measures from train group

# 2.4- Reading activity
ytest = Activity_Label for each observed measures for test group
ytrain = Activity_Label for each observed measures for test group

# 2.5- Reading activity Label
activitylabel = Activity_Label

# 3- Reshaping data
# 3.1- Generating Rando ID dataset
idtest1 = Ids from rando test group
idtrain1 = Ids from rando train group
idall = Ids from rando train and test group

#3.2- Merging test and train dataset
testdataset = ID, activity, obserbed measures for test group
traindataset = ID, activity, obserbed measures for train group
alldataset = ID, activity, obserbed measures for test and train group

#4 Calculating descriptive_stat
stat_mean = extract mean
stat_sd = extract sd

#5 Reshaping to get final tidy data
#5.1 calculating meand and sd
stat_meanfinal = adding a column stat with the info mean to dataset
stat_sdfinal = adding a column stat with the info sd to dataset
stat_final = stack stat_meanfinal and stat_sdfinal

#5.2 Droping 2 columns and renaming replacement columns

#5.3 Merging Activity info

#5.4 Merging Rando Info
tidy_data = final dataset 



