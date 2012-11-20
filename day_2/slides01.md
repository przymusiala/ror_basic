<!SLIDE title-slide transition=fade>

# Część 1 #

<!SLIDE transition=fade>

# Podstawy systemu kontroli wersji GIT

<!SLIDE bullets incremental smaller transition=fade>

# Git

  * GIT to rozproszony system kontroli wersji
  * Repozytorium lokalne i zdalne
  * Zalety GITa
  * Kto używa GITa ?
  * [Instalacja GITa] (https://help.github.com/articles/set-up-git)
  * Konfiguracja profilu w repozytorium
  * [Film] (http://railscasts.com/episodes/96-git-on-rails)


<!SLIDE transition=fade>
[github.com] (http://github.com)
![github.com] (gfx/github.png)

<!SLIDE bullets incremental smaller transition=fade>

# [github.com] (http://github.com)

  * Czym jest github ?
  * Kto korzysta z githuba
  * Konto w github
  * Zarządzanie projektami
  * Tricki w github


<!SLIDE bullets incremental transition=fade>

# Zadanie

* Zakładamy konto w [github.com] (http://github.com)
* Klonujemy projekt z githuba
* Tworzymy swój projekt w githubie


<!SLIDE commandline incremental small transition=fade>

# Klonujemy projekt z githuba

    $ git clone https://github.com/thoughtbot/cocaine

<!SLIDE bullets incremental small transition=fade>

# Uruchamiamy gitg #

* Otwieramy projekt cocaine
* Czytamy commity

<!SLIDE commandline incremental transition=fade>

# Klucz ssh #

    $ ssh-keygen
    $ cd ~/.ssh/
    $ cat id_rsa.pub

[ssh w github] (https://github.com/settings/ssh)

<!SLIDE commandline incremental transition=fade>

# [Nowy projekt na githubie] (https://github.com/new)

    $ rails new ksiegarnia -d mysql
    $ cd ksiegarnia
    $ git init
    $ git add .
    $ git remote add origin git@github.com  -> Twój projekt
    $ git push -u origin master

<!SLIDE bullets incremental transition=fade>

# Zadanie

  * wejdz na githuba kolegi
  * sklonuj jego repozytorium
  * otwórz repozytorium w gitg
