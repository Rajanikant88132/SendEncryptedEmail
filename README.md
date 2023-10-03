# SendEncryptedEmail
This utility sends signed or encryted email .
<br>
Its a spring boot application required java 14 .
<br>
Its uses javaMail and Spring Mail to send email based on SMTP protocal.
<br>
Its configuration based tool. Below are configuration of tool maintain in externalize application.properties file.
There are OOB/Spring provided properties for mail which start with spring.mail*
<br>
custom.mail.* properties are added for utility support .

<br>
####### MAIL ##############
<br>spring.mail.host=smtp.gmail.com
<br>spring.mail.port=587
<br>spring.mail.username=XXXXX@gmail.com
<br>spring.mail.password=XXXXXX
<br>spring.mail.properties.mail.smtp.auth=true
<br>spring.mail.properties.mail.smtp.starttls.enable=true
<br>spring.mail.protocol=smtp
<br>spring.mail.defaultEncoding=UTF-8
<br>custom.mail.subject=Your mainframe password has been reset
<br>custom.mail.template.format=html
<br>custom.mail.template.html.userid=email-templates/email_template_userid.html
<br>custom.mail.template.plain.userid=email-templates/email_template_userid_plain.txt
<br>custom.mail.template.html.passwd=email-templates/email_template_password.html
<br>custom.mail.template.plain.passwd=email-templates/email_template_password_plain.txt
<br>custom.mail.template.format.fromuser=rXXXXXX@gmail.com
<br>custom.mail.template.passwordfile=email-templates/password_File.txt
<br>custom.mail.signing.signoption=sign
<br>custom.mail.signing.singlecertificate=false
<br>custom.mail.signing.certificate.extention=.cer
<br>custom.mail.signing.certificate.directory=src/main/resources/email-templates/certificates

<br>custom.mail.signing.jks.file=src/main/resources/email-templates/rajanikantjks.jks
<br>custom.mail.signing.jks.password=rajani.test
<br>custom.mail.encrypting.jks.file=src/main/resources/email-templates/Rajanikant.cer
####### SPRING ##############
<br>spring.main.banner-mode=off


<br>1. Spring inbuilt properties : 
<br>This is self explanatory  or details can be found over internet .

<br>2.Custom properties :

<br>
1. custom.mail.template.format=html
    Email can be html format or plain text format . based on this value accordingly template will be picked up.
<br>
2. Below are template file location should be relative to current directory of jar
   template details can be refered in this git repo.
custom.mail.template.html.userid=email-templates/email_template_userid.html
<br>
custom.mail.template.plain.userid=email-templates/email_template_userid_plain.txt
<br>
custom.mail.template.html.passwd=email-templates/email_template_password.html
<br>
custom.mail.template.plain.passwd=email-templates/email_template_password_plain.txt
<br>
4. fromuser is used from which email id ,emails will be sent to reciepient .<br>
custom.mail.template.format.fromuser=rXXXXXX@gmail.com
<br>
5. This file will be used for list of users details like userid ,password ,emailid ,user name<br>
custom.mail.template.passwordfile=email-templates/password_File.txt
<br>
6. This value will be used for informing tool whether email should be signed email or encrypted email<br>
custom.mail.signing.signoption=sign
<br>
7. This property will be used to inform utility whether single certificate will be used or per reciepient different certificate will be provided .<br>
custom.mail.signing.singlecertificate=false
<br>
8. this is used what is extention of certificate for dynamically loading certificate.<br>
custom.mail.signing.certificate.extention=.cer
<br>
9. This will be used to store list of certificates if  per reciepient different certificate issued .
  <br> 
custom.mail.signing.certificate.directory=email-templates/certificates
<br>
<br>
<br>
9. This will be used for signing the email <br>
custom.mail.signing.jks.file=email-templates/rajanikantjks.jks
<br>
10. This will be used for signing the email <br>
custom.mail.signing.jks.password=rajani.test
<br>


<br>
10. This will be used for encryoting the email with single certificates <br>
custom.mail.encrypting.jks.file=email-templates/Rajanikant.cer
<br>
<br>
<b> ###################Generating certificate - Start ###############################</b>
<b> Generating certificate with java keytool</b>
<br>
<br>
1. keytool -genkey -alias rajanikanttest -keyalg RSA -validity 1825 -keystore "rajanikantjks.jks" -storetype JKS -dname "CN=www.ibm.com,OU=IBM,O=IBM,L=Helsinki,ST=Uusima,C=FI"  -ext san=dns:ibm.com,dns:IBM.COM -keypass rajani.test -storepass rajani.test
<br>
Output :
</br>
Generating 2 048 bit RSA key pair and self-signed certificate (SHA256withRSA) with a validity of 1 825 days
	for: CN=www.ibm.com, OU=IBM, O=IBM, L=Helsinki, ST=Uusima, C=FI
<br>
Warning:
The JKS keystore uses a proprietary format. It is recommended to migrate to PKCS12 which is an industry standard format using "keytool -importkeystore -srckeystore rajanikantjks.jks -destkeystore rajanikantjks.jks -deststoretype pkcs12".
<br>
(base) rajanikantyadav@Rajanikants-MacBook-Pro-180 TEST_CERTIFICATES % ls
rajanikantjks.jks
<br>
<br>
<b> Generating certificate with openssl </b>
<br>
<br>
<br>
openssl req -x509 -newkey rsa:4096 -keyout publickeytest.pem -out privaatekeyTest.pem -days 365 
<br>
<br>
openssl pkcs12 -export -out publickeytest.p12 -inkey publickeytest.pem -in privaatekeyTest.pem
<br>
<b> ###################Generating certificate - End###############################</b>
<br>
<br>
<br>
<b> ############ Steps to run the utility ##################</b>
<br>
<br>
1. Clone the repository
<br>
<br>
git clone https://github.com/Rajanikant88132/SendEncryptedEmail.git

<br>
<br>
2. Update properties value as per env and requirement 
br>
<br>
3. Run below command 

<br>
    §JAVA_HOME/bin/java -jar MailUtilityForCAReplacement.jar  --spring.config.location=email-templates/application.properties
<br>
<br>
<br>
4. Output looks like something this .
<br>
<br>
<img width="1430" alt="Screenshot 2023-08-04 at 12 21 49" src="https://github.com/Rajanikant88132/SendEncryptedEmail/assets/17102344/2867c522-4b13-4950-b350-a64275d422b3">

<br>
<br>
5. Email will be recieved  looks like something this .
<br>
<br>
<img width="1188" alt="Screenshot 2023-08-04 at 12 40 14" src="https://github.com/Rajanikant88132/SendEncryptedEmail/assets/17102344/3b9b40d7-31da-4431-8fb0-bc97c8013784">
