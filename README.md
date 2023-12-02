# Automated-Backup-Script-for-Important-Documents
creating a script called backup.sh which runs every day and automatically backs up any encrypted password files that have been updated in the past 24 hours.

after creating the script backup.sh file , try following steps to check its working
step1: Save the backup.sh file you're working on and make it executable using command:

       chmod +x backup.sh
       
step2: Download the following .zip file with the wget command:

       wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-LX0117EN-SkillsNetwork/labs/Final%20Project/important-documents.zip
       
step3: Unzip the archive file:

       unzip -DDo important-documents.zip
       
step4: Update the file’s last-modified date to now:

       touch important-documents/*
Test your script using the following command:
       
       ./backup.sh important-documents .
       
This should have created a file called backup-[CURRENT_TIMESTAMP].tar.gz in your current directory.
step5: Copy the backup.sh script into the /usr/local/bin/ directory:

       sudo cp backup.sh /usr/local/bin/
       
step6: Using crontab, schedule your /usr/local/bin/backup.sh script to backup the important-documents folder every 24 hours to the directory /home/project:

       crontab -e
       
       crontab -l
       
Edit this file to introduce tasks to be run by cron.
Each task to run has to be defined through a single line
indicating with different fields when the task will be run
and what command to run for the task
To define the time you can provide concrete values for
minute (m), hour (h), day of month (dom), month (mon),
and day of week (dow) or use '*' in these fields (for 'any').# 
Notice that tasks will be started based on the cron's system
daemon's notion of time and timezones.
Output of the crontab jobs (including errors) is sent through
email to the user the crontab file belongs to (unless redirected).
For example, you can run a backup of all your user accounts
at 5 a.m every week with:
0 5 * * 1 tar -zcf /var/backups/home.tgz /home/

for midnight 12 am use 
       0 0 * * * /usr/local/bin/backup.sh important-documents /home/project
       cntrl + x 
       y + enter
     
step7: explicitly start the cron service using the below command:

      sudo service cron start 
       
Once the cron service is started, check in the directory /home/project to see if the .tar files are being created.
If they are, then stop the cron service using the below command, otherwise it will continue to create .tar files every minute:
        
      command: sudo service cron stop      

