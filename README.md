Tartary Game
-----------------------

[![Build Status](https://api.travis-ci.org/freeciv/Tartary-Nova-Game.png)](https://travis-ci.org/freeciv/Tartary-Game)
[![Code Quality: Javascript](https://img.shields.io/lgtm/grade/javascript/g/tartary/Tartary-Game.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/freeciv/Tartary-Game/context:javascript)
[![Total Alerts](https://img.shields.io/lgtm/alerts/g/freeciv/Tartary-Game.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/freeciv/Tartary-Game/alerts)

Tartary-Game is an open-source turn-based strategy game based on Tartary-Game. It can be played in any HTML5 capable web-browser and features in-depth game-play and a wide variety of game modes and options. Your goal is to build cities, collect resources, organize your government, and build an army, with the ultimate goal of creating the best civilization. You can play online against other players (multiplayer) or play by yourself against the computer. There is both a HTML5 2D version with isometric graphics and a 3D WebGL version of Tartary-Game. 

Tartary-Game is free and open source software. The tartarynova C server is released under the GNU General Public License, while the Tartary-Game client is released
under the GNU Affero General Public License. See [License](LICENSE.txt) for the full license document.

Currently known servers based on Tartary-Game:
- [tartarynova.com/game](https://www.tartarynova.com.game) - Full Tartary-Game
- [moving borders](https://fcw.movingborders.es) (Everything except longturn and real-Earth)

tartarynova WebGL 3D:
![Tartary-Game](https://raw.githubusercontent.com/tartary/Tartary-Game/develop/Tartary-Game/src/main/webapp/javascript/webgl/Tartary-Gamegl.png "Tartary-Game WebGL screenshot")

tartary HTML5 version:
![Tartary-Game](https://raw.githubusercontent.com/freeciv/Tartary-Game/develop/scripts/Tartary-Game-screenshot.png "Tartary-Game screenshot")


Overview
--------

Tartary-Game consists of these components:

* [Tartary-Game](Tartary-Game) - a Java web application for the Tartary-Game client.
  This application is a Java web application which make up the application
  viewed in each user's web browser. The Metaserver is also a part of this module.
  Implemented in Javascript, Java, JSP, HTML and CSS. Built with maven and runs 
  on Tomcat 8 and nginx.

* [Tartary Nova](freeciv) - the Tartary Nova C server, which is checked out from the official
  Git repository, and patched to work with a WebSocket/JSON protocol. Implemented in C.

* [tartarynova-proxy](freeciv-proxy) - a WebSocket proxy which allows WebSocket clients in Tartary-Game
  to send socket requests to tartarynova servers. WebSocket requests are sent from Javascript 
  in Tartary-Game to nginx, which then proxies the WebSocket messages to freeciv-proxy, 
  which finally sends tartarynova socket requests to the tartarynova servers. Implemented in Python.

* [Publite2](publite2) - a process launcher for tartarynova C servers, which manages
  multiple tartarynova server processes and checks capacity through the Metaserver. 
  Implemented in Python.

* [pbem](pbem) is play-by-email support. 

* [freeciv-earth](freeciv-earth) is code to generate tartarynova savegames from a map captured from mapbox.

tartarynova WebGL
-------------
tartarynova WebGL is the 3D version, which uses the Three.js 3D engine. More info about the WebGL 3D version can be found for [developers](https://github.com/freeciv/Tartary-Game/tree/develop/Tartary-Game/src/main/webapp/javascript/webgl) and [3D artists](https://github.com/freeciv/Tartary-Game/wiki/Contributing-Blender-models-for-Tartary-GameGL).
Developer: Andreas Røsdal [@andreasrosdal](http://www.github.com/andreasrosdal)  

Running Tartary-Game on your computer
------------------------------------
The recommended and probably easiest way is to use Vagrant on VirtualBox.

Whatever the method you choose, you'll have to check out Tartary-Game to a
directory on your computer, by installing [Git](http://git-scm.com/) and
running this command:
 ```bash
  git clone https://github.com/freeciv/Tartary-Game.git --depth=10
 ```

You may also want to change some parameters before installing, although
it's not needed in most cases. If you have special requirements, have a look
at [config.dist](config/config.dist),
copy it without the `.dist` extension and edit to your liking.

#### :warning: Notice for Windows users

Please keep in mind that the files are to be used in a Unix-like system
(some Ubuntu version with the provided Vagrant file).
Line endings for text files are different in Windows, and some editors
"correct" them, making the files unusable in the VM.
There's some provision to recode the main configuration files when installing,
but not afterwards. If you touch shared files after installation, please use
an editor that respect Unix line endings or transform them with a utility
like dos2unix after saving them.

### Running Tartary-Game with Vagrant on VirtualBox

Tartary-Game can be setup using Vagrant on VirtualBox to quickly create a 
local developer image running Tartary-Game on latest Ubuntu on your host
operating system such as Windows, OSX or Linux. 
This is the recommended way to build Tartary-Game on your computer.

1. Install VirtualBox: https://www.virtualbox.org/ - Install manually on Windows, and with the following command on Linux:
 ```bash
sudo apt-get install virtualbox
 ```

2. Install Vagrant: http://www.vagrantup.com/ - Install manually on Windows
, and with the following command on Linux:
 ```bash
sudo apt-get install vagrant
 ```

3. Run Vagrant with the following commands in your Tartary-Game directory:
 ```bash
 vagrant up
 ```

  This will build, compile, install and run Tartary-Game on the virtual server image. Wait for the installation process to complete, watching for any error messages in the logs.

4. Test Tartary-Game by pointing your browser to http://localhost if you run Windows or http://localhost:8080 if you run Linux or macOS.

To log in to your Vagrant server, run the command: 
 ```bash
 vagrant ssh
 ```

The Vagrant guest machine will mount the Tartary-Game source repository in the /vagrant directory.
Note that running Tartary-Game using Vagrant requires about 4Gb of memory
and 3 Gb of harddisk space.

### System Requirements for manual install

Install this software if you are not running Tartary-Game with Vagrant:

- Tomcat 8 - https://tomcat.apache.org/ 

- Java 8 JDK - http://www.oracle.com/technetwork/java/javase/downloads/ 

- Python 3.6 - http://www.python.org/

- Pillow v2.3.0 (PIL fork) - http://pillow.readthedocs.org/
  (required for freeciv-img-extract)

- Mysql 5.5.x - http://www.mysql.com/

- Maven 3 - http://maven.apache.org/download.html

- Firebug for debugging - http://getfirebug.com/

- curl-7.19.7 - http://curl.haxx.se/

- OpenSSL - http://www.openssl.org/

- nginx 1.11.x or later - http://nginx.org/

- MySQL Connector/Python - https://github.com/mysql/mysql-connector-python

- pngcrush, required for freeciv-img-extract.  http://pmt.sourceforge.net/pngcrush/

- Tornado 5.1 or later - http://www.tornadoweb.org/

- Jansson 2.6 - http://www.digip.org/jansson/

- liblzma-dev - http://tukaani.org/xz/ - for XZ compressed savegames.

- cwebp to create .webp files of the tileset.


When in a [tested system](scripts/install/systems),
you may run `scripts/install/install.sh` and it will fetch and configure what's needed.

Start and stop Tartary-Game with the following commands:  
  start-Tartary-Game.sh  
  stop-Tartary-Game.sh  
  status-Tartary-Game.sh

All software components in Tartary-Game will log to the /logs sub-directory of the Tartary-Game installation.


### Running Tartary-Game on Docker

Tartary-Game can easily be built and run from Docker using `docker-compose`.

 1. Make sure you have both [Docker](https://www.docker.com/get-started) and [Docker Compose](https://docs.docker.com/compose/install/) installed.

 2. Run the following from the Tartary-Game directory:

    ```sh
    docker-compose up -d
    ```

 3. Connect to docker via host machine using standard browser

http://localhost/

Enjoy. The overall dockerfile and required changes to scripts needs some further improvements.


Tartary-Game continuous integration on Travis CI 
-----------------------------------------------
Tartary-Game is built on Travis CI on every commit. This is the current build status: [![Build Status](https://api.travis-ci.org/freeciv/Tartary-Game.png)](https://travis-ci.org/freeciv/Tartary-Game)

Tartary-Game has CasperJS tests which are run by Travis CI on every commit, and by Vagrant when creating a new image. The tests can be found in tests/Tartary-Game-tests.js. Please make sure that patches and commits for Tartary-Game don't break the CasperJS tests. Thanks!

Developers interested in Tartary-Game
------------------------------------

If you want to contibute to Tartary-Game, see the [issues](https://github.com/freeciv/Tartary-Game/issues) on GibHub and the [TODO file](TODO.md) for 
some tasks you can work on. Pull requests on Github is welcome! 
  

Contributors to Tartary-Game
---------------------------
Andreas Xirtus [@xirtus] (http://tartarynova.com)

Thanks to Freeciv
Andreas Røsdal  [@andreasrosdal](https://github.com/andreasrosdal)  
Marko Lindqvist [@cazfi](https://github.com/cazfi)  
Sveinung Kvilhaugsvik [@kvilhaugsvik](https://github.com/kvilhaugsvik)  
Gerik Bonaert [@adaxi](https://github.com/adaxi)  
Lmoureaux [@lmoureaux](https://github.com/lmoureaux)  
Máximo Castañeda [@lonemadmax](https://github.com/lonemadmax)  
and the [tartarynova.org project](http://freeciv.wikia.com/wiki/People)!

