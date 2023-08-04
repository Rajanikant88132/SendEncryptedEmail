# SendEncryptedEmail
This utility sends signed or encryted email .
Its a spring boot application required java 14 .
Its uses javaMail and Spring Mail to send email based on SMTP protocal.

Its configuration based tool. Below are configuration of tool maintain in externalize application.properties file.
There are OOB/Spring provided properties for mail which start with spring.mail*
custom.mail.* properties are added for utility support .


####### MAIL ##############
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=XXXXX@gmail.com
spring.mail.password=XXXXXX
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
spring.mail.protocol=smtp
spring.mail.defaultEncoding=UTF-8
custom.mail.subject=Your mainframe password has been reset
custom.mail.template.format=html
custom.mail.template.html.userid=src/main/resources/email-templates/email_template_userid.html
custom.mail.template.plain.userid=src/main/resources/email-templates/email_template_userid_plain.txt
custom.mail.template.html.passwd=src/main/resources/email-templates/email_template_password.html
custom.mail.template.plain.passwd=src/main/resources/email-templates/email_template_password_plain.txt
custom.mail.template.format.fromuser=rXXXXXX@gmail.com
custom.mail.template.passwordfile=src/main/resources/email-templates/password_File.txt
custom.mail.signing.signoption=sign
custom.mail.signing.singlecertificate=false
custom.mail.signing.certificate.extention=.cer
custom.mail.signing.certificate.directory=src/main/resources/email-templates/certificates

custom.mail.signing.jks.file=src/main/resources/email-templates/rajanikantjks.jks
custom.mail.signing.jks.password=rajani.test
custom.mail.encrypting.jks.file=src/main/resources/email-templates/Rajanikant.cer
####### SPRING ##############
spring.main.banner-mode=off


1. Spring inbuilt properties : 
This is self explanatory  or details can be found over internet .

2.Custom properties :


1. custom.mail.template.format=html
    Email can be html format or plain text format . based on this value accordingly template will be picked up.
2. Below are template file location should be relative to current directory of jar
   template details can be refered in this git repo.
custom.mail.template.html.userid=email-templates/email_template_userid.html
custom.mail.template.plain.userid=email-templates/email_template_userid_plain.txt
custom.mail.template.html.passwd=email-templates/email_template_password.html
custom.mail.template.plain.passwd=email-templates/email_template_password_plain.txt

3. fromuser is used from which email id ,emails will be sent to reciepient .
custom.mail.template.format.fromuser=rXXXXXX@gmail.com

4. This file will be used for list of users details like userid ,password ,emailid ,user name
custom.mail.template.passwordfile=email-templates/password_File.txt

5. This value will be used for informing tool whether email should be signed email or encrypted email
custom.mail.signing.signoption=sign

6. This property will be used to inform utility whether single certificate will be used or per reciepient different certificate will be provided .
custom.mail.signing.singlecertificate=false

7. this is used what is extention of certificate for dynamically loading certificate.
custom.mail.signing.certificate.extention=.cer

8. This will be used to store list of certificates if  per reciepient different certificate issued .
   
custom.mail.signing.certificate.directory=email-templates/certificates

9. This will be used for signing the email 
custom.mail.signing.jks.file=email-templates/rajanikantjks.jks

10. This will be used for signing the email 
custom.mail.signing.jks.password=rajani.test

10. This will be used for encryoting the email with single certificates 
custom.mail.encrypting.jks.file=email-templates/Rajanikant.cer
