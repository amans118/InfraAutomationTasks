AMI Backup code has been refered with a small enhancement from: https://gist.github.com/bkozora/724e01903a9ad481d21e
AMI Cleanup code has been refered with a small enhancement from: https://gist.github.com/bkozora/d4f1cf0e5cf26acdd377

Automated AMI Backups
•	This script will first search for all ec2 instances having a tag with "Backup” on it and are in "Running" state.
•	After generating the instances list, it loops through each instance and then creates an AMI of it.
•	Also, it will look for a "Retention" tag key which will be used as a retention policy number in days. If there is no tag with that name, it will use a 7 days default value for each AMI.
•	After creating the AMI it creates a "DeleteOn" tag on the AMI indicating when it will be deleted using the Retention value and another Lambda function.

Automated AMI and Snapshot Deletion
•	This script first searches for all ec2 instances having a tag with "Backup” on it and are in "Running" state.
•	After generating the instances list, it loops through each instance and reference the AMIs of that instance.
•	It checks whether the latest daily backup succeeded then it stores every image that reached its "DeleteOn" tag's date for deletion.
•	It then loops through the AMIs, de-registers them and removes all the snapshots associated with that AMI.
