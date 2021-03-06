install-and-run
===============

Use this repository's issue tracker to post comments, bug reports, and help questions on installing and running NGDS CKAN. Find the formal installation documentation NGDS_Installation_Documentation.docx provided in this repository, which has essential background information and other useful tips for installing a publisher or aggregator node for use in the NGDS system. Below is a quick installation guide (from the same installer script) meant for seasoned Linux users.

### Low Level Installer Script Documentation

### Introduction


[Here's the installer script you'll be running](https://github.com/ngds/install-and-run/blob/master/installation/install-ngds.sh)

[ckanext-ngds](https://github.com/ngds/ckanext-ngds) is in a beta production mode; we're shooting for releasing v1.0 in April 2014.  The installer script will install the latest stable version of ckanext-ngds along with core CKAN and every other software dependency it needs to run in production.  Currently, the stable version of ckanext-ngds is developed to run with core CKAN v2.0.4.  We have development branches in the ckanext-ngds Github repository which we use to keep this software up-to-date with the latest stable releases of core CKAN and these branches follow this naming convention:
`upgrade-ckanvX.X.X` where `X.X.X` refers to a core CKAN release version.  These development branches do not contain stable code and will usually be merged into the master branch once they are stable.

### Installation

Installation with the installer script has only been tested in Ubuntu v12.04 LTS, Xubuntu v12.04, Ubuntu v12.10 and Xubuntu v12.10.  All of this software has been tested on MacOSX as well, but we don't have an installation script for that -- so you'll have to install all of the components manually.  

Setup your environment (assumes starting as user `root`. If you created your system with `ngds` as your main user, you may skip the first 3 steps below.):

    $ adduser ngds
    $ adduser ngds sudo
    $ su -l ngds

Download NGDS:

    $ cd ~
    $ mkdir tmp
    $ cd tmp
    $ git clone https://github.com/ngds/install-and-run.git
    $ cd install-and-run/installation

Set custom parameters in the installer script:

    site_url
    SERVER_NAME
    SMTP_SERVER
    SMTP_STARTTLS
    SMTP_USER
    SMTP_PASSWORD
    SMTP_MAIL_FROM
    GEOSERVER_REST_URL

    # Customize CSW
    IDENTIFICATION_TITLE
    IDENTIFICATION_ABSTRACT
    IDENTIFICATION_KEYWORDS
    IDENTIFICATION_KEYWORDS_TYPE
    IDENTIFICATION_FEES
    IDENTIFICATION_ACCESSCONSTRAINTS
    PROVIDER_NAME
    PROVIDER_URL
    CONTACT_NAME
    CONTACT_POSITION
    CONTACT_ADDRESS
    CONTACT_CITY
    CONTACT_STATEORPROVINCE
    CONTACT_POSTALCODE
    CONTACT_COUNTRY
    CONTACT_PHONE
    CONTACT_FAX
    CONTACT_EMAIL
    CONTACT_URL
    CONTACT_HOURS
    CONTACT_INSTRUCTIONS
    CONTACT_ROLE

Run the installer script:

    $ sudo ./install-ngds.sh (this will take a long time)

Troubleshooting:

If `install_ngds.sh` is not recognized as an executable file, allow the current user to run it as an executable:

    $ sudo chmod u+x install_ngds.sh

NGDS should be being served at http://127.0.0.1/
Login: {username: admin, password: admin}

If you find that upon visiting http://127.0.0.1/ (or http://<SERVER_NAME>) instead of NGDS you get the generic Apache "It's working page", run this command: `sudo a2dissite default`.

Go to http://127.0.0.1/organization and add a new organization named 'public'.

Error Log Locations:

    The log file for CKAN is in: /var/log/apache2/

    Source code is installed in: /opt/ngds/bin/default

    CKAN error log: /var/log/apache2/ckan_default.error.log
    
    CKAN custom log: /var/log/apache2/ckan_default.custom.log
    
    Harvest gather queue log: /var/log/ckan-central-gather.log
    
    Harvest fetch queue log: /var/log/ckan-central-fetch.log
    
    Harvest run log: /var/log/ckan-central-run-harvest.log
    
    Celery log: /var/log/ckan-node-celery.log

    Geoserver and SOLR run on top of Tomcat:
    Tomcat log: /var/log/ckan-tomcat.log

### Changelog
##### v1.0.1 - 2014/04/21
- Fixed map search bug where the user could only perform one search query.
- Make CSV error failure more graceful.
- Added custom NGDS favicon.
- Added search hints link.
- Changed some of the contributor organization info.
- No previews for unsupported data.
- Fixed ratings issue.
- Custom NGDS activity streams.
- Add option for contact email in installation script.
