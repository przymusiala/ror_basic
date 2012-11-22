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
## Instalacja

    @@@ Ruby

      # Gemfile
      gem 'devise'

      # w konsoli

      $ bundle      
      $ rails generate devise:install
      $ rails generate devise User


<!SLIDE smaller transition=fade>
# Devise
## Konfiguracja

    @@@ Ruby
      # db/migrate/*_devise_create_users.rb

      Odkomentowujemy moduły
      Zapisujemy plik i robimy migrację

      $ rake db:migrate

      # app/models/user.rb   ->   Dołączamy moduły
        :confirmable, :lockable, :timeoutable

<!SLIDE smaller transition=fade>
# Devise
## Widoki i mailery

  [config/locales/devise.pl.yml] (https://gist.github.com/1958933)
    @@@ Ruby
      ściągamy i zapisujemy plik devise.pl.yml


      $ rails generate devise:views users

      # app/views/users/*
      sprawdzamy i edytujemy pliki


<!SLIDE smaller transition=fade>
# Twitter bootstrap

    @@@ Ruby

      # Gemfile
      gem "less-rails"
      gem "twitter-bootstrap-rails"

      $ bundle install

      $ rails g bootstrap:install
      $ rails g bootstrap:layout application fluid

<!SLIDE smaller transition=fade>

    @@@ Ruby
      
      rails g scaffold Post title:string description:text
      rake db:migrate
      rails g bootstrap:themed Posts


