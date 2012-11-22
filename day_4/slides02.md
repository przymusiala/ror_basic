<!SLIDE title-slide transition=fade>

# Część 2 #


<!SLIDE transition=fade>

# Strumienie danych

<!SLIDE bullets incremental transition=fade>

# Udostępniamy publiczne API swojej aplikacji.

  * XML
  * JSON
  * ATOM

<!SLIDE smaller transition=fade>
# Relacja has_many :through
    @@@ Ruby
    # app/models/product.rb

    class Product < ActiveRecord::Base 
      has_many :line_items
      ➤ has_many :orders, through: :line_items 
      #...
    end

<!SLIDE smaller transition=fade>
# JSON & XML
[json_builder] (https://github.com/dewski/json_builder)

    @@@ Ruby
      # config/routes.rb
      
      resources :products do
        get 'who_bought', on: :member
      end

      # app/controllers/products_controller.rb
      # na końcu:
      
      def who_bought
        @product = Product.find(params[:id])
        respond_to do |format|
          format.atom
          format.xml { render xml: @product.to_xml 
             (include: :orders) }
          format.json { render json: @product.to_json
             (include: :orders) }
        end
      end
    $ rake routes

<!SLIDE transition=fade>

# http://localhost:3000/
# products/1/who_bought.json



<!SLIDE transition=fade>

# Paginacja

<!SLIDE bullets incremental transition=fade>

# Od przybytku głowa nie boli?!
## ... Czyli jak ogarnąć dużo obiektów

  * konfiguracja środowiska
  * jak rails wysyła maile ? 
  * szablony html

<!SLIDE bullets incremental transition=fade>

# 
## 


<!SLIDE transition=fade>

    @@@ Ruby
      # Gemfile

      gem 'will_paginate', '~> 3.0'

      $ bundle install

<!SLIDE smaller transition=fade>
# Skrypt ładujący dane

    @@@ Ruby
    # script/load_orders.rb

    Order.transaction do 
      (1..100).each do |i|
        Order.create(name: "Klient #{i}", 
        address: "Ulica Dluga #{i} ", 
        email: "klient-#{i}@example.com", pay_type: "Check")
      end 
    end


    $ rails runner script/load_orders.rb


<!SLIDE smaller transition=fade>
# Paginacja w kontrolerze

    @@@ Ruby
    # app/controllers/orders_controller.rb

    def index
      ➤ @orders = Order.paginate page: params[:page], 
      ➤  order: 'created_at desc', per_page: 10

<!SLIDE smaller transition=fade>
# Paginacja na widoku

    @@@ Ruby
    # app/views/orders/index.html.erb

    <%= link_to 'Nowe Zamówienie', new_order_path %> 
    ➤ <p><%= will_paginate @orders %></p>
