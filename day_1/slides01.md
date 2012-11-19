<!SLIDE title-slide transition=fade>

# Część 1 #

<!SLIDE transition=fade>

# Instalacja RoR na różnych systemach operacyjnych #

<!SLIDE title-slide transition=fade>

# Windows #

<!SLIDE bullets incremental transition=fade>

  * RailsInstaller (Ruby 1.9.3, Rails 3.2.1)
  * "Next", "I accept all of the Licenses", "Next", "Install", "Finish" :)

<!SLIDE title-slide transition=fade>

# Linux (Ubuntu) #

<!SLIDE commandline incremental transition=fade>

    $ sudo apt-get install apache2 curl git nodejs
    $ sudo apt-get install libmysqlclient-dev mysql-server 
    $ curl -L https://get.rvm.io | bash -s stable
    $ rvm requirements
    $ rvm install 1.9.3
    $ rvm use 1.9.3
    $ gem install rails
    $ rvm --default 1.9.3
    $ rails -v

<!SLIDE title-slide transition=fade>

# OSX #

<!SLIDE bullets incremental transition=fade>

  * Xcode a w nim "command line tools"
  * git
  * Następnie przechodzimy do instalacji RVM

<!SLIDE commandline incremental transition=fade>

    $ curl -L https://get.rvm.io | bash -s stable
    $ rvm requirements
    $ rvm install 1.9.3
    $ rvm use 1.9.3
    $ gem install rails
    $ rvm --default 1.9.3
    $ rails -v

<!SLIDE title-slide transition=fade>

# Konfigurowanie środowiska deweloperskiego i narzędzi (Windows, Linux, Mac OS X). #

<!SLIDE bullets transition=fade>

  * Baza danych:
    * MySQL / PostgreSQL
    * MongoDB
    * SQLite (domyślna baza RoR)
  * Edytory / IDE:
    * Sublime Text 2
    * Vim
    * RubyMine
    * TextMate (1|2)
  * Przeglądarka:
    * Google Chrome
    * Safari
    * Firefox

<!SLIDE bullets transition=fade>

# Inne #

  * Sequel Pro (Tylko na OSX)
  * iTerm2 (Tylko na OSX)
  * Terminator (Tylko Linux)
