# GCR-Google-Calendar-RAT
Google Calendar RAT is a PoC of Command&amp;Control over Google Calendar Events
The script creates a 'Covert Channel' by exploiting the event descriptions in Google Calendar. The target will connect directly to Google."
It could be considered as a layer 7 application Covert Channel (but some friends would say it cannot be :) very thanks to my mates "Tortellini" https://aptw.tf )

![image](https://github.com/MrSaighnal/GCR-Google-Calendar-RAT/assets/47419260/8e4e1f83-8141-408d-8910-e8e92896b8e4)

# How it works
GCR attempt to connect to a valid shared Google Calendar link and after generating a unique ID check for any yet-to-be-executed commands.
If it is not able to find any command, it creates a new one (fixed to "whoami") as a proof of connection.
Every event is composed by two part:
1. The Title, which contains the unique ID, it means you can schedule multiple commands creating events having the same unique ID as name
2. The Description, which contains the command to execute and the base64 encoded output using the pipe symbol as separator "|"

# What a SOC analyst/Blue Teamer will see?
This:
![image](https://github.com/MrSaighnal/GCR-Google-Calendar-RAT/assets/47419260/a2bf1f24-90a6-49ab-9a12-bcc7c999e2b3)
![image](https://github.com/MrSaighnal/GCR-Google-Calendar-RAT/assets/47419260/66dbd7b5-4060-4829-9229-99bb0c5a19e5)


which results in this
![image](https://github.com/MrSaighnal/GCR-Google-Calendar-RAT/assets/47419260/244e9acf-44a9-45b7-92f5-f61d911446a3)
![image](https://github.com/MrSaighnal/GCR-Google-Calendar-RAT/assets/47419260/14c875fc-c28f-45d6-94c1-64e3dd02606b)



# How to use it
- Setup a Google service account and obtain the credentials.json file, place the file in the same directory of the script
- Create a new Google calendar and share it with the new created service account
- Edit the script to point your calendar address
- Once executed on the target machine an event with a unique target ID is automatically created autoexecuting the "whoami" command
- Use the following syntax in the event description for the communication =>   CLEAR_COMMAND|BASE64_OUTPUT
  ### Examples:
  - "whoami|"
  - "net users|"
- The date is fixed on May 30th, 2023. You can create unlimited events using the unique ID as the event name.

# POC
![poc](https://github.com/MrSaighnal/GCR-Google-Calendar-RAT/assets/47419260/b83e6f28-36bd-454d-9c04-87095a280b1a)



# Notes
I prefer to consider this project as a game rather than an experiment :)
Please do not use it for illegal purpose.
I take no responsibility for the use that will be made of it

IT IS JUST A POC IN PYTHON, PLEASE DO NOT ASK ME HOW TO WEAPONIZE IT!
