# EmailAutomate
Print to Email to Bot to cycle to Print

<Mail Setup Raspberry Pi /w Repetier-Server on Linux>

sudo apt-get install ssmtp mailutils

{See App Password on Google after Setting up 2FA and allow less secure apps}

{https://myaccount.google.com/lesssecureapps}

sudo nano /etc/ssmtp/ssmtp.conf

#Edit

"mailhub=smtp.gmail.com:587"

#Add these to .conf

AuthUser=youraddress@gmail.com

AuthPass=AppPassword

UseSTARTTLS=YES

USETLS=YES

//

nano EmailScript.py

import smtplib

smtpUser='youraddress@gmail.com'

smtpPass='AppPassword'

toAdd='youraddressorwhereever@gmail.com'

fromAdd='smtpUser'

subject='Printer Update'

header='To: ' + toAdd + '\n' + 'From: ' + fromAdd + '\n' + 'Subject: ' + subject

body='Printer Completed'

print header + '\n' + body

s=smtplib.SMTP('smtp.gmail.com',587)

s.starttls()

s.login (smtpUser, smtpPass)

//

sudo nano /var/lib/Repetier-Server/database/extcommands.xml

<config>

//<execute name = "emailjob" allowParams = "true" >/usr/bin/python /home/pi/EmailScript.py </execute>

</config>

//

#End G-Code

@execute emailjob
