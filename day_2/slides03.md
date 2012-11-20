<!SLIDE title-slide transition=fade>

# Część 3 #

<!SLIDE transition=fade>

## Walidacja danych wejściowych, testy jednostkowe ##

<!SLIDE smaller transition=fade>

## Paleta możliwości ##
    @@@ ruby
      validates :terms, :acceptance => true
      validates :password, :confirmation => true
      validates :username, :exclusion => { 
        :in => %w(admin superuser)
      }
      validates :email, :format => { 
        :with => /\A([^@\s]+)@((?:[-a-z0-9]+\.)+[a-z]{2,})\Z/i, 
        :on => :create 
      }
      validates :age, :inclusion => {
        :in => 0..9
      }
      validates :first_name, :length => {
        :maximum => 30
      }
      validates :age, :numericality => true
      validates :username, :presence => true
      validates :username, :uniqueness => true

<!SLIDE transition=fade>

# Trochę zabawy #

<!SLIDE transition=fade>

# Stan obecny - wolna amerykanka #
    @@@ ruby
      # app/models/product.rb

      class Product < ActiveRecord::Base
        attr_accessible :description,
          :image_url,
          :price,
          :title
      end

<!SLIDE bullets incremental transition=fade>

# Wymagania klienta #

  * Nie można dodać produktu z pustym tytułem, opisem i bez url'a obrazka
  * Tytuły muszą być unikalne
  * Cena musi być większa od zera ;)
  * Obrazki mogą być tylko w formacie gif|jpg|png

<!SLIDE code smaller transition=fade>

    @@@ ruby
      # app/models/product.rb

      class Product < ActiveRecord::Base
        attr_accessible :description, 
          :image_url, 
          :price, 
          :title 
        validates :title,
          :description,
          :image_url,
          presence: true
        validates :price, 
          numericality: {
            greater_than_or_equal_to: 0.01
          }
        validates :title, uniqueness: true
        validates :image_url,
          allow_blank: true,
          format: {
            with:    %r{\.(gif|jpg|png)\Z}i,
            message: 'must be a URL for GIF, JPG or PNG image.'
          }
      end

<!SLIDE title-slide transition=fade>

# Testy#
### Ale o co chodzi??? ###

<!SLIDE title-slide transition=fade>

# Lepiej to przetestujmy... #

<!SLIDE transition=fade>

# Atrybuty produktu nie mogą być puste #

<!SLIDE small transition=fade>

    @@@ ruby
      # test/unit/product_test.rb
      
      test "Atrybuty produktu nie mogą być puste" do
        product = Product.new
        assert product.invalid?
        assert product.errors[:title].any?
        assert product.errors[:description].any?
        assert product.errors[:price].any?
        assert product.errors[:image_url].any?
      end
    
    $ rake test

<!SLIDE transition=fade>

# Cena musi być #
# większa od zera #

<!SLIDE smaller transition=fade>

    @@@ ruby
      # test/unit/product_test.rb

      test "Cena musi być większa od zera" do
        product = Product.new(title:       "Moja książka",
                              description: "Lorem ipsum dolor",
                              image_url:   "zzz.jpg")
        product.price = -1
        assert product.invalid?
        assert_equal ["must be greater than or equal to 0.01"],
          product.errors[:price]

        product.price = 0
        assert product.invalid?
        assert_equal ["must be greater than or equal to 0.01"], 
          product.errors[:price]

        product.price = 1
        assert product.valid?
      end

    $ rake test

<!SLIDE transition=fade>

# URLem mogą prowadzić tylko do obrazków #

<!SLIDE small transition=fade>

## Oszczędźmy torchę czasu ##

    @@@ ruby
      # test/unit/product_test.rb

      def new_product(image_url)
        Product.new(title:       "Moja książka",
                    description: "Lorem ipsum dolor",
                    price:       1,
                    image_url:   image_url)
      end

<!SLIDE smaller transition=fade>

    @@@ ruby
      # test/unit/product_test.rb

      test "URLem mogą prowadzić tylko do obrazków" do
        ok = %w{ obr.gif obr.jpg obr.png obr.JPG obr.Jpg
                 http://a.b.c/x/y/z/obr.gif }
        bad = %w{ obr.doc obr.gif/more obr.gif.more }
        
        ok.each do |name|
          assert new_product(name).valid?, 
            "#{name} shouldn't be invalid"
        end

        bad.each do |name|
          assert new_product(name).invalid?,
            "#{name} shouldn't be valid"
        end
      end

    $ rake test

<!SLIDE transition=fade>

# Nie marnujmy czasu na ciągłe #
# uzupełnianie bazy testowej danymi #

<!SLIDE smaller transition=fade>
      
      @@@ ruby
        # test/fixtures/products.yml

        one:
          title: MyString
          .....

        two:
          title: MyString
          .....

        moja_ksiazka: 
          title: Moja ksiazka
          description: 
            Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
            tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam
          price: 49.50
          image_url: moja.png 

<!SLIDE transition=fade>

# Produkt musi mieć #
# unikalny tytuł #

<!SLIDE smaller transition=fade>

    @@@ ruby
      # test/unit/product_test.rb
      
      test "Produkt musi mieć unikalny tytuł" do
        prod = Product.new(title: products(:moja_ksiazka).title,
                              description: "yyy", 
                              price: 1, 
                              image_url: "obr.gif")

        assert prod.invalid?
        assert_equal ["has already been taken"], 
          prod.errors[:title]
      end

    $ rake test
