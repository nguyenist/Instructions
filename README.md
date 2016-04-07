# Project Sidewalk - Instructions
This repository contains onboarding instructions for start contributing to
projects under Project Sidewalk. For example, it contains instructions on
how to install softwares and libraries that the multiple projects rely on
(e.g., PostgreSQL, PostGIS).

## Getting Started

### Java & Scala
Install
[Java Development Kit version 7 (JDK 7)](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html).
JDK 8 is backward compatible and our code should work on it too. To build a Scala project, you should also install [`sbt`](http://www.scala-sbt.org/) or [`activator`](https://www.lightbend.com/activator/download).

### JavaScript
Install [`npm`](https://www.npmjs.com/), a package manager for JavaScript. Then install [`Grunt`](http://gruntjs.com/getting-started), a task runner for JavaScript.

### Python
Install Python. I recommend installing [Anaconda](https://www.continuum.io/downloads), a Python distribution with all the scientific packages (e.g., numpy) bundled by default.

### PostgreSQL
We use Postgres (or PostgreSQL) for persistent data storage of user data and GIS data. We choose
PostgreSQL over other databases (e.g., MySQL) primarily because of its geographical data support.
You can either install Postgres and plug-ins them on top of a virtual machine (recommended; easier to install) or
directly into your computer.

#### Installation
* **(Recommended) If you installing them using a virtual machine, see [Virtual Box and Vagrant](### Virtual Box and Vagrant (Optional)).**
* I you are installing Postgres directly into your computer, see the following pages:
  * Windows:
    * [PostGIS](http://postgis.net/windows_downloads) : PostGIS's official web page. Follow the instruction to install PostgreSQL as well as PostGIS (> 2.0.0).
  * OS X:
    * [Kyng Chaos](http://www.kyngchaos.com/software/postgres) : Kyng Chao offers a PostgreSQL 9.4 binary for OS X that include PostgreSQL, PostGIS, and pgRouting. This would be the easiest way to go for the OS X user. Once installed, start the database with the following command. `/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data/`. To start the postgres, run `/usr/local/pgsql/bin/postgres -D /usr/local/pgsql/data/`

Once you got the database set up, send an email to Kotaro (kotaro@cs.umd.edu) so he can send you the data to be dumped into the database.

#### Accessing the Database
Whether you are accessing the database on your local machine or on the virtual machine, you can also access you can access it by the either command line tool or a Postgres client (e.g., Postico) using the following credential information:

```
Host: localhost:5432
User: sidewalk
Password: sidewalk
Database: sidewalk
```

If you cannot login, check if the user name exists by running the following:

```
psql -d sidewalk
\du
```

To import data, you should run the following command (you may need to run it as sudo. Run: `sudo su - postgres`):

```
psql -d sidewalk -a -f sidewalk.sql
```

### Virtual Box and Vagrant (Optional)
Start by installing VirtualBox (www.virtualbox.org/wiki/Downloads) and Vagrant (www.vagrantup.com).
Windows users should also install an SSH client as well (or the chance is you already have it if you are using git.
Add `C:\Program Files (x86)\Git\bin` to the PATH.
See [here](http://stackoverflow.com/questions/27768821/ssh-executable-not-found-in-any-directories-in-the-path)
and [here](https://gist.github.com/haf/2843680) for more information.)
Spend some time setting up and familiarizing yourself with vagrant. To run Vagrant, type the following command in the directory where the `Vagrantfile` is located:

```
vagrant init hashicorp/precise64
```

This should place a vagrant file in this directory. You should receive 
```
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
```

Then

```
vagrant up
```

This will create a new Ubuntu Trusty 64 Bit virtual machine and configure it for this project. This step will take a while. When it completes, you can log into a terminal of your new virtual machine by using:

```
vagrant ssh
```

When you are done working be sure the suspend (or halt/destroy) your vagrant virtual machine:
```
vagrant suspend
```

When you are ready to start working again just use:
```
vagrant up
vagrant ssh
```

## Development Environment

### IDE
Effectively using an IDE for development is an important skill you need.
When you are working on this project, I highly recommend you to use IDE.
My favorites are those offered by [JetBrains](https://www.jetbrains.com/)
(e.g., [IntelliJ](https://www.jetbrains.com/idea/) for Scala and Java, [PyCharm](https://www.jetbrains.com/pycharm/) for Python).
They also have [student license](https://www.jetbrains.com/student/) which gives
a free access to a set of their products.

#### Hint: Debugging Play applications on IntelliJ
This is based on [this stackoverflow post](http://stackoverflow.com/questions/19473941/how-to-debug-play-application-using-activator).
1. In a terminal, go to the root directory of your Play project. Then run: `activator -jvm-debug 9999`
2. Start the play application by entering `run` in the activator console.
3. Set up IntelliJ's debug setting. Go to Run > Edit Configureations...
4. Add a new configuration; click "+" and select "Remote".
5. Choose Transport: Socket, Debugger mode: Attach, Host: localhost, Port: 9999, and select the appropriate module's classpath. Click "Ok."
6. Run a debugger and set break points. Then you should be good to go!

### Git and GitHub
As you can see, we use Git and GitHub for version control and collaboration. See below for the list of concepts you should know:

* Branching:
  1. Create a branch to work on your task. You can create a branch by "git checkout -b <branch-name>"
  2. Make changes to the code in your branch
  3. Once you are done with editing the code, issue a "pull request"
  4. Wait for a code to be reviewed. (You can work on other stuff by branching )
  5. Merge the code once reviewed. If there are conflicts, resolve it. (http://stackoverflow.com/questions/161813/fix-merge-conflicts-in-git)
* Pull Request:
  * [Using pull requests](https://help.github.com/articles/using-pull-requests/)
* For more information, see:
  * [GitHub Training & Guides](https://www.youtube.com/watch?v=U8GBXvdmHT4): A YouTube channel for learning Git and GitHub.
  * [Git tutorial by RyPress](http://rypress.com/tutorials/git/index) : This is a short and concise tutorial of GIT. I find it more approachable than the official Git documentation.
  * [Pro Git](http://git-scm.com/doc) : The official git documentation.

## Utilities/Tutorials/Datasets
This section introduces various tools that may become handy while working on
the projects.

### PostgreSQL Clients
Database client programs make it easier to interact with tables.
The following PostgreSQL clients provides GUI to view and manipulate the database.
* [Postico](https://eggerapps.at/postico/): A free Postgres client for OS X.
* [Valentina Studio](https://www.valentina-db.com/en/valentina-studio-overview): A cross-platform database client.

### GIS Data Viewer
When you are working with GIS dataset, you have to visualize it at many stages of your research & development cycle (e.g., debugging, analysis). Following tools are what I have found handy
while working with GIS dataset.
* [QGIS](http://www.qgis.org/en/site/) : A comprehensive open source GIS tool. I recommend to install [OpenLayers plug-in](https://plugins.qgis.org/plugins/openlayers_plugin/) and [Quick OSM](https://plugins.qgis.org/plugins/QuickOSM/).
* [geojson.io](http://workshops.boundlessgeo.com/postgis-intro/) : A browser based geojson data viewer.

### GIS Data Manipulation
* [ogr2ogr](http://www.gdal.org/ogr2ogr.html) : ogr2ogr allows you to convert different file formats
* [osm2pgrouting](http://pgrouting.org/docs/tools/osm2pgrouting.html) : The application allows you to convert data from the OSM format into the pgRouting format and populate a database. If you are on OS X, you can install it via homebrew (`brew install osm2pgrouting`).
* [pgShapeloader](http://suite.opengeo.org/4.1/dataadmin/pgGettingStarted/pgshapeloader.html): The tool allows you to load a shapefile into PostgreSQL.

### PostGIS and pgRouting
* FOSS4G routing with pgRouting: http://workshop.pgrouting.org/index.html
* [Introduction to PostGIS](http://workshops.boundlessgeo.com/postgis-intro/) : A comprehensive tutorial for using PostGIS.

### GIS Datasets
#### Washington, D.C.
1. Download OSM file using wget: http://workshop.pgrouting.org/chapters/installation.html (Use the following bounding box parameter for downloading the Washington DC dataset: -76.9,39.0,-77.1,38.8)
Or simply download the data from http://download.bbbike.org/osm/bbbike/WashingtonDC/
2. Follow the steps to import the OSM data into the PostGIS-enabled database (or use a python script with Imposm ) http://workshop.pgrouting.org/chapters/osm2pgrouting.html
