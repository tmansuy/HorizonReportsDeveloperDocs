---
layout: default
title: Self-signed certificate for SSL
nav_order: 1
parent: Configuring IIS
grand_parent: Deploying Horizon Reports
---

Horizon Reports can be run using SSL (Secure Sockets Layer). This is a good idea, because user name and passwords are sent from the browser to the server and SSL ensures this is done securely (not that it's an issue on your own machine but it is when you deploy to a production web server). The internet server requires a trusted certificate in order to access a web site using SSL. Without one (there isn't one by default), you'll get something like this when you launch:

![](/assets/images/certissue.png)

You can click the Proceed Anyway button to continue, but it's a pain to have to do that every time. To install a certificate, do the following:<!-- Taken from http://blogs.msdn.com/b/robert_mcmurray/archive/2013/11/15/how-to-trust-the-iis-express-self-signed-certificate.aspx -->

* Run Microsoft Management Console. The easy way to do that is hold down the Windows key and press R to display the Run dialog, enter "mmc," and click OK.

* Choose Add/Remove Snap-in from the File menu and double-click Certificates. In the Certificates Snap-In dialog, select *Computer account*. Click Next.

    ![](/assets/images/certificate1.png)

* Choose *Local computer*, then click Finish in the Certificates Snap-In dialog and OK in the Add or Remove Snap-in dialog.

    ![](/assets/images/certificate2.png)

* Expand Certificates, then Personal, select the Certificates folder under Personal, and click the localhost certificate.

    ![](/assets/images/certificate3.png)

* Choose All Tasks from the Action menu and select the Export function from the submenu.

    ![](/assets/images/certificate4.png)

* Click Next in the Certificate Export Wizard.

    ![](/assets/images/certificate5.png)

* Choose *No, do not export the private key* and click Next.

    ![](/assets/images/certificate6.png)

* Choose *DER encoded binary X.509 (.CER)* and click Next.

    ![](/assets/images/certificate7.png)

* Enter a path for the exported certificate, such as "C:\Users\<UserName>\Desktop\IISExpress.cer," where <UserName> is your Windows user name (the path and name aren't important since you won't be keeping the file permanently). Click Next and then click Finish.

    ![](/assets/images/certificate8.png)

* Expand Trusted Root Certification Authorities and select Certificates.

    ![](/assets/images/certificate9.png)

* Choose All Tasks from the Action menu and select the Import function from the submenu.

    ![](/assets/images/certificate10.png)

* Click Next in the Certificate Import Wizard.

    ![](/assets/images/certificate11.png)

* Enter the path you specified earlier when exporting the certificate and click Next.

    ![](/assets/images/certificate12.png)

* Choose *Place all certificates in the following store* and ensure the selected Certificate store is "Trusted Root Certification Authorities". Click Next and then Finish.

    ![](/assets/images/certificate13.png)

* You should now see a localhost certificate in Trusted Root Certification Authorities.

    ![](/assets/images/certificate14.png)

* Close MMC. You can choose No when asked to save settings to Console1.
