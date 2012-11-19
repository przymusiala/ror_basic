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
