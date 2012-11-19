<!SLIDE title-slide transition=fade>

# Dzień pierwszy #

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

<!SLIDE title-slide transition=fade>

# Część 2 #

<!SLIDE title-slide transition=fade>

# Wprowadzenie do języka programowania Ruby #

<!SLIDE small transition=fade>

# Konwencje ponad konfiguracje #

    @@@ ruby
      # Nazwy klas:

        ToJestKlasa

      # Nazwy metod:

        to_jest_metoda

      # Zmienne:

        @zmienna
        to_tez_jest_zmienna

      # Stałe:

        TO_JEST_STALA

<!SLIDE transition=fade>

# Typy danych #

<!SLIDE bullets transition=fade>

  * string
  * array
  * hash
  * ...

<!SLIDE transition=fade>

# Konsola - irb #

<!SLIDE transition=fade>

# Instrukcje warunkowe #

<!SLIDE code transition=fade>

# if #

    @@@ ruby
      if coś
        # ..
      elsif coś_innego
        # ..
      else
        # ..
      end

      # Wersja skrócona
      jedz_prosto if zielone_swiatlo

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby


<!SLIDE code transition=fade>

# unless #
    
    @@@ ruby
      jedz_peosto unless czerwone_swiatlo

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE code transition=fade>
  
# while #

    @@@ ruby
      while true
        # ..
      end

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE code transition=fade>

# each #

    @@@ ruby
      [1,2,3,4,5].each do |value|
        puts value
      end

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE code transition=fade>

# for #

    @@@ ruby
      for i in 1..10 do
        puts i
      end

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE code transition=fade>

# Wyjątki #

    @@@ ruby
      begin
        dziwna_funkcja
      rescue => e
        puts "Wszystko się posypało"
      end

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE code transition=fade>

# Użycie klasy #

    @@@ ruby
      class OwczarekNiemiecki
        def daj_głos
          "Hau, hau!"
        end
      end

      fokus = OwczarekNiemiecki.new
      fokus.daj_głos

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania (jedna funkcja wywołuje drugą, trzy sposoby ustawienia zmiennej instancji, attr_accesory, inicjalizery) ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE transition=fade>

# Popularne idiomy #

<!SLIDE transition=fade>

    @@@ ruby
      a || b

Wyrażenie najpier sprawdza wartość a, jeśli nie różni się ona od fałszu lub nila proces się kończy i zwraca a. W przeciwnym przypadku zwraca b. Popularny sposób zwracania domyślnej wartości jeśli pierwsze wyrażenie nie zostało ustawione.

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE transition=fade>

    @@@ ruby
      a ||= b

Przypisanie, jeśli a jest fałszem lub nilem, ustaw a na b

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE transition=fade>

    @@@ ruby
      count += 1

Zwiększanie o daną wartość

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE transition=fade>

    @@@ ruby
      price *= discount

      # price = price * discount

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE transition=fade>
    
    @@@ ruby
      count ||= 0 

      # count = count || 0

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

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

<!SLIDE title-slide transition=fade>

# Część 4 #

<!SLIDE smaller incremental transition=fade>

# Tworzenie aplikacji bazodanowej. #
## ORM? ##
      
      Tabela: users
      Model: User

## Dzięki ORMowi mamy automatyczny dostęp do wszystkich pól w tabeli ##
## Są one zmapowane na metody obiektu ##

    @@@ ruby
      user = User.first
      user.email

<!SLIDE transition=fade>

# Operacje na ActiveRecord #

<!SLIDE smaller transition=fade>

# find #

    @@@ ruby
      User.find(1)
      User.find_by_email('adam@google.com')
      User.find_all_by_email('adam@google.com')

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE smaller transition=fade>

# where #

    @@@ ruby
      User.where(:email => 'adam@google.com')

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE smaller transition=fade>

# conditions #

    @@@ ruby
      # parametry z sieci są eskejpowane

      User.find(:first, 
        :conditions => ['email = ?', params[:email]]
      ) 

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE smaller transition=fade>

# select #
    
    @@@ ruby
      User.find(:first,
        :conditions => ['email = ?', params[:email]], 
        :select => [:first_name, :email]
      )          

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE smaller transition=fade>

# Operacja na bazie #
    
    @@@ ruby
      Order.where(name: 'dave').each do |order|
        order.pay_type = "Purchase order"
        order.save
      end

<!SLIDE transition=fade>

# Relacje: #
    @@@ ruby
      has_many
      has_one
      belongs_to

<!SLIDE transition=fade>

    @@@ ruby
      # app/models/post.rb
      has_many :comments

      # app/models/comment.rb
      belongs_to :post

<!SLIDE transition=fade>

# Zadanie #
## Stworzyć post i dodać do niego komentarz przez konsolę ##
