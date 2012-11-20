<!SLIDE title-slide transition=fade>

# Część 2 #

<!SLIDE transition=fade>

## Początek prac nad księgarnią, tworzenie panelu do zarządzania produktami, HTML i kaskadowe arkusze stylów ##

<!SLIDE bullets incremental transition=fade>

# Budowa aplikacji Księgarnia

* Programowanie przyrostowe: krok po kroku
* Krótkie i szybkie iteracje
* Częste commity
* Projektowanie aplikacji

<!SLIDE  bullets incremental transition=fade>

# Projektowanie aplikacji Księgarnia

* Widok kupujacego
* Widok sprzedajacego
* Struktura danych


<!SLIDE  commandline incremental transition=fade>

# No to startujemy !
## generujemy projekt Rails

    $ rails new ksiegarnia -d mysql2
    $ cd ksiegarnia

    a następnie....
    ustawiamy bazę danych w pliku config/database.yml

<!SLIDE transition=fade>

# Generujemy scaffold

<!SLIDE commandline incremental transition=fade>

    $ rails generate scaffold Product \
        title:string description:text image_url:string \
        price:decimal

<!SLIDE small transition=fade>

# Edycja migracji 

    @@@ ruby
      # app/models/product.rb

      class CreateProducts < ActiveRecord::Migration 
        def change
          create_table :products do |t| 
            t.string :title
            t.text :description 
            t.string :image_url
          ➤ t.decimal :price, precision: 8, scale: 2
            t.timestamps
          end 
        end
      end


<!SLIDE commandline incremental transition=fade>

# Załadowanie migracji
  
    $ rake db:migrate
    $ rails server

<!SLIDE small transition=fade>

# Stylowanie widoków

<!SLIDE bullets incremental transition=fade>


* [Formularz] (assets/_form.html.erb) umieszczamy w app/views/products
* [Style] (assets/products.css.scss) umieszczamy w app/assets/stylesheets
* [Listing] (assets/index.html.erb) umieszczamy w app/views/products

<!SLIDE bullets incremental small transition=fade>

# Zadania

* [Gitignore] (http://media.pragprog.com/titles/rails4/code/rails32/depot_a/.gitignore) 
* [Data Seed] (http://media.pragprog.com/titles/rails4/code/rails32/depot_a/db/seeds.rb)