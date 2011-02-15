# Publication
-----------------
* Gollapudi, R., Revanna, K.V., Hemmerich, C., Schaack, S. & Dong, Q. (2008) BOV- A Web-based BLAST Output Visualization Tool. BMC Genomics 9, 414. This little toy was ranked as a "Highly accessed" paper by BioMed Central.
* PUBMED link: http://www.ncbi.nlm.nih.gov/pubmed/18793422

# Setup
-----------------

## Supported Operating Systems
* Linux, Solaris (untested on other Unix flavors)

## Supported Browsers
* Mozilla Firefox 2 or higher
* Internet Explorer 6 or higher
* Safari
* Opera

## Prequisites
* Apache 1.3 or 2.0 ( http://www.apache.org )
* MySQL Database ( http://dev.mysql.com/ )
* BioPerl 1.5.2 or higher ( http://www.bioperl.org/ )

## CPAN Perl Modules
The following perl modules can be downloaded from the CPAN archive at http://www.cpan.org.
* DBI
* DBD::mysql
* HTML::Template
* GD
* CGI::Ajax

## Core Perl Modules
The following perl modules are part of a default perl installation. If they are not available on your system, you can download them from CPAN.
* CGI
* CGI::Carp
* Data::Dumper
* Digest::MD5
* Math::Round
* File::stat
* POSIX
* Storable

## Database Setup 
BOV requires a MySQL database to store data and generate results. By default, BOV will connect to MySQL installed on the local machine, using the username bov, and the database name microbial. To setup BOV with these default settings, issue the following commands from the unix command prompt.

* To create the username bov, without password
    mysql -uroot -p password -e 'create user bov@localhost'
* With password
    mysql -uroot -p password -e 'create user bov@localhost identified by password'

* To create the database and give permissions to your user
    mysql -uroot -p password -e 'create database microbial'
    mysql -uroot -p password -e 'grant select,insert,create,drop on microbial.* to bov@localhost'

If you want to use different database settings, reference the MySQL
documentation for instructions on how to configure the database.


## Installation
------------

1. Download BOV from http://cgb.indiana.edu/files/downloads/Blast_Output_Viewer.tar.gz

2. Uncompress BOV using the command 
    tar -zxvf Blast_Output_Viewer.tar.gz

3. Edit the setup.sh to customize BOV for your location. You must set the parameters under "REQUIRED PARAMETERS". If you did not use the default database settings, you must also define the connection information under "OPTIONAL PARAMETERS".


5. Execute the setup command to configure BOV, this creates two folders in the same 
directory called 'cgi-bin' and 'htdocs'
    setup.sh

6. If you have set the 'lifetime' value in setup.sh for automatic expiration of results, a shell script will be created in
    bin/clean_database.sh

To have this command executed automatically, you need to add the following entry to your crontab.

    * 0 * * * sh /PATH/TO/clean_database.sh
       
7. Rename the htdocs directory to BOV and copy it to the directory your apache installation uses for html files. This directory is defined in your apache configuration file as 'DocumentRoot'. So if your apache configuration includes

    DocumentRoot "/var/www/htdocs"

you would execute

    cp -rp htdocs /var/www/htdocs/BOV

8. Rename the cgi-bin directory to BOV and copy it to the directory your apache installation uses for cgi-bin executables. This may be defined as 'ScriptAlias' in your apache configuration.

    ScriptAlias /cgi-bin/ "/var/www/cgi-bin"

in which case you would execute

    cp -rp cgi-bin /var/www/cgi-bin/BOV

If your apache configuration does not include ScriptAlias, then append cgi-bin to th
e DocumentRoot, e.g.

    cp -rp cgi-bin /var/www/htdocs/cgi-bin/BOV