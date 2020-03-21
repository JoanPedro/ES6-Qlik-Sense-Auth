# Qlik-Sense-Auth
An example of using NodeJs backend integrated with Qlik Sense.

Prerequisites:

- Node.js
- Qlik Sense Server

Configuration:

- Node.js

    1. Open cmd;
    2. Access the project's qliksense-nodejs-example directory;
    3. Install package by running "npm install" in that directory;
        - This solution uses the qlik-auth package, which is configured as a project dependency;
    4. Open the index.html file and update the hostname and port in the script tags on line 6 to point to your qlik server;
    5. Open script.js and configure the appId and objectId variables to access your development environment;
        - In the link below see how to get appId and objectId;
        - [Getting appId and objectId] (https://help.qlik.com/en-US/sense-developer/February2020/Subsystems/Mashups/Content/Sense_Mashups/Howtos/mashups-obtain-app-object-id.htm)

- Qlik Sense Server

    1. Open QMC (Qlik Management Console) and navigate to the CONFIGURE SYSTEM> Virtual proxies area;
    2. Create a new virtual proxy with a prefix of your choice (you will need this prefix when configuring Node.js)
    3. When editing a virtual proxy, in Properties> Authentication, fill in the "Authentication module redirect URI" with http: // node_server: 3000 / authenticate
        - Port 3000 is configured in server.js and can be changed as desired
    4. In the virtual proxy edition, in Properties> Advanced, add this in the "Additional response header" section: Access-Control-Allow-Origin: *
    5. Again in QMC go to CONFIGURE SYSTEM> Certficates
    6. Export the certificate, giving it the name on the Node.js machine. By default it will be saved in C: \ ProgramData \ Qlik \ Sense \ Repository \ Exported Certificates
    7. Copy the client certificate to the root of the Node.js project
        - In the link below tutorial on how to export certificates
        - [Exporting Certificates] (https://support.qlik.com/articles/000005433)

How it works:

1. The script.js file attempts to load the configured Qlik Sense Server qlik.js;
2. At this point the 'Authentication module redirect URI' in the virtual proxy is called;
3. This is solved by the server.js file and creates a hardcode user called "sample";
4. The qlik-auth module is called to send a ticket request with the specified configuration;
5. A ticketId is returned and the session established;
6. No user input is required.

OBS: Note that, at the time of this tutorial, Qlik made an update that disabled the use of this method on a machine that does not have Qlik Sense (Server) installed. That is, you will need to run Node and Qlik Sense on the same machine, whether virtual or not.
