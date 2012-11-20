<!SLIDE title-slide transition=fade>

# Część 2 #

<!SLIDE transition=fade>

## Początek prac nad księgarnią, tworzenie panelu do zarządzania produktami, HTML i kaskadowe arkusze stylów ##

<!SLIDE bullets incremental transition=fade>
# Budowa aplikacji Depot

* programowanie przyrostowe: krok po kroku
* krótkie i szybkie iteracje
* częste commity
* projektowanie aplikacji

<!SLIDE  bullets incremental transition=fade>
# Projektowanie aplikacji Depot

* widok kupujacego
* widok sprzedajacego
* struktura danych


<!SLIDE  commandline incremental transition=fade>
# No to startujemy !
## generujemy projekt Rails

    $ rails new depot -d mysql2
    $ cd depot

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

    @@@ Ruby
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


<!SLIDE small transition=fade>
# Załadowanie migracji
$ rake db:migrate
$ rails server