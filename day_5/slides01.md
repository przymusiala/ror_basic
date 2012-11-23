<!SLIDE title-slide transition=fade>

# Część 1 #

<!SLIDE small bullets incremental transition=fade>

# Konto użytkownika

  * Instalacja i konfiguracja Devise
  * Stylowanie widoków i maili
  * Ciekawe moduły
  * Twitter bootstrap

<!SLIDE smaller transition=fade>

# Devise
## Konfiguracja

    @@@ ruby

      # Gemfile
      gem 'devise'

      # terminalu

<!SLIDE commandline incremental transition=fade>

# Devise
## Instalacja
    $ bundle      
    $ rails generate devise:install
    $ rails generate devise User

<!SLIDE smaller transition=fade>

# Devise
## Konfiguracja

    @@@ ruby
      # db/migrate/*_devise_create_users.rb
      # Odkomentowujemy moduły
      # Zapisujemy plik i robimy migrację

      $ rake db:migrate

      # app/models/user.rb   ->   Dołączamy moduły
        :confirmable, :lockable, :timeoutable

<!SLIDE smaller transition=fade>
# Devise
## Widoki i mailery

  [config/locales/devise.pl.yml] (https://gist.github.com/1958933)

<!SLIDE commandline incremental transition=fade>

## Ściągamy i zapisujemy plik devise.pl.yml

    $ rails generate devise:views users

<!SLIDE smaller transition=fade>

    @@@ ruby
      # app/views/users/*
      # ....sprawdzamy i edytujemy pliki

<!SLIDE smaller transition=fade>

# Twitter bootstrap - konfiguracja

    @@@ ruby

      # Gemfile
      gem "less-rails"
      gem "twitter-bootstrap-rails"

<!SLIDE commandline incremental transition=fade>

# Twitter bootstrap - instalacja

    $ bundle install
    $ rails g bootstrap:install
    $ rails g bootstrap:layout application fluid

<!SLIDE small  transition=fade>

    @@@ ruby
      rails g scaffold Post title:string description:text
      rake db:migrate
      rails g bootstrap:themed Posts
