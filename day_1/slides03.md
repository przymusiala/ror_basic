<!SLIDE title-slide transition=fade>

# Część 3 #

<!SLIDE transition=fade>

# Pierwsza aplikacja w Ruby on Rails. #

<!SLIDE commandline incremental transition=fade>

    $ rails new demo -d mysql
    $ cd demo

<!SLIDE transition=fade>

# Architektura aplikacji w Ruby on Rails. #

<!SLIDE bullets incremental smaller transition=fade>

# Struktua katalogów #

    app/
    config/
    db/
    doc/
    lib/
    log/
    public/
    script/
    test/
    tmp/
    vendor/
    config.ru
    Gemfile
    Gemfile.lock
    Rakefile
    README.rdoc

<!SLIDE transition=fade>

# MVC #

<!SLIDE small transition=fade>

## Model: ##

    @@@ ruby
      def full_name
        "#{self.first_name} #{self.last_name}"
      end

## Kontroler: ##
    
    @@@ ruby
      @user = User.find(params[:id])
      
## Widok: ##
    
    @@@ html
      <h1>Witaj <%= @user.full_name %></h1>

## Routing: ##

    @@@ ruby
        resources :users

<!SLIDE transition=fade>

## YAML - konfiguracja połączenia z bazą danych ##

    @@@ ruby
      development:
        adapter: mysql2
        encoding: utf8
        reconnect: false
        database: demo2_development
        pool: 5
        username: root
        password:
        socket: /tmp/mysql.sock

<!SLIDE commandline incremental transition=fade>

# Tworzymy nową bazę danych #
    $ rake db:create

<!SLIDE transition=fade>

### Dla Ubuntu dodatkowo do Gemfile należy dodać ###
### gem 'therubyracer' ###

    $ rails server
    $ http://localhost:3000

<!SLIDE small transition=fade>

## Wygennerujmy coś na dzień dobry ##
    $ ctrl + c # żeby wyłączyć serwer
### Lub w nowej konsoli: ###
    $ rails generate controller Say hello goodbye

<!SLIDE small transition=fade>
    
    @@@ ruby
      # app/controllers/say_controller.rb

      class SayController < ApplicationController
      
        def hello
        end
      
        def goodbye
        end
      
      end

<!SLIDE incremental transition=fade>

# http://localhost:3000/say/hello #

<!SLIDE transition=fade>

# Trochę dynamiki #

    @@@ html

      # app/views/say/hello.html.erb:
      
      <h1>Hello from Rails!</h1>
      <p> It is now <%= Time.now %> </p>

<!SLIDE transition=fade>
    
# Dobra praktyka #

<!SLIDE small transition=fade>

    @@@ ruby
      # app/controllers/say_controller.rb

      class SayController < ApplicationController
      
        def hello
          @time = Time.now
        end
      
        def goodbye
        end
      
      end

<!SLIDE transition=fade>
    
    @@@ html
      # app/views/say/hello.html.erb:
    
      <h1>Hello from Rails!</h1>
      <p> It is now <%= @time %> </p>

<!SLIDE transition=fade>

# Linkowanie #

<!SLIDE small transition=fade>

## Plik hello.html.erb mógłby zawierać: ##
      
    @@@ html
      # app/views/say/hello.html.erb:
      ...
      <p>
        Say <a href="/say/goodbye">Goodbye</a>!
      </p>
      ...

<!SLIDE small transition=fade>

## A goodbye.html.erb mógłby wyglądać: ##
    
    @@@ html
      # app/views/say/goodbye.html.erb:
      ...
      <p>
        Say <a href="/say/hello">Hello</a>!
      </p>
      ...
## Jednak po przeniesieniu w inne miejsce wszystko mogło by się posypać.. . 

<!SLIDE small transition=fade>

## Prawidłowo wykonane hiperłącze powinno wyglądać następująco: ##

    @@@ html
      # app/views/say/hello.html.erb:
      ...
      <h1>Hello from Rails!</h1>
      <p>
        It is now <%= @time %>
      </p>
      <p>
        Time to say
        <%= link_to "Goodbye", say_goodbye_path %>!
      </p>
      ...

<!SLIDE transition=fade>

# Eksperymenty: #
## Dodawanie: #
    @@@ ruby
      1+2
## Konkatenacja:
    @@@ ruby
      "cow" + "boy"
## Czas: ##
    @@@ ruby
      1.hour.from_now
