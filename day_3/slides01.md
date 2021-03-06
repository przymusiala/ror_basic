<!SLIDE title-slide transition=fade>

# Część 1 #

<!SLIDE transition=fade>

# Tworzenie koszyka produktów
  
<!SLIDE commandline incremental transition=fade>
  
# Stary, dobry scaffold

    $ rails generate scaffold cart
    $ rake db:migrate

<!SLIDE smaller transition=fade>

# Koszyk dostępny
# we wszystkich kontrolerach

    @@@ ruby
      # app/controllers/application_controller.rb

      class ApplicationController < ActionController::Base

        protect_from_forgery

        # Dajmy dostęp w widoku
        helper_method :current_cart
        
        private

          def current_cart
            Cart.find(session[:cart_id])
          rescue ActiveRecord::RecordNotFound
            cart = Cart.create
            session[:cart_id] = cart.id
            cart
          end
      end

<!SLIDE commandline incremental small transition=fade>
  
# Pozycja w koszyku

    $ rails generate scaffold line_item product_id:integer cart_id:integer
    $ rake db:migrate

<!SLIDE small transition=fade>

# Połączenie koszyka z pozycjami koszyka

    @@@ ruby
      # app/models/cart.rb

      class Cart < ActiveRecord::Base
        has_many :line_items, dependent: :destroy
      end
      
      # app/models/line_item.rb
      
      class LineItem < ActiveRecord::Base
        attr_accessible :cart_id, :product_id

        belongs_to :product
        belongs_to :cart
      end

<!SLIDE smaller transition=fade>

## Zabezpieczenie przed usunięciem
## produktu podłączonego do jakiegoś koszyka

    @@@ ruby
      # app/models/product.rb

      class Product < ActiveRecord::Base
        before_destroy :check_if_referenced_by_line_item

        private

          def check_if_referenced_by_line_item
            if line_items.empty?
              return true
            else
              errors.add(:base, 'Podłączone pozycje koszyka')
              return false
            end
          end
      end

<!SLIDE smaller transition=fade>

# Dodajmy przycisk dodania do koszyka
    @@@ html
      <!-- app/views/store/index.html.erb -->

      <% @products.each do |product| %>
        <div class="entry">
          <%= image_tag(product.image_url) %>
          <h3><%= product.title %></h3>
          <p><%= sanitize(product.description) %></p>
          <div class="price_line">
            <span class="price">
              <%= number_to_currency(product.price) %>
            </span>
      ➤     <%= button_to 'Dodaj do koszyka',
              line_items_path(product_id: product) %>
          </div>
        </div>
      <% end %>
### [Arkusz css] (https://github.com/przymusiala/ror_basic/blob/master/day_3/assets/store.css.scss)
<!SLIDE smaller transition=fade>

# Wrzucamy produkt do koszyka
    @@@ ruby
      def create
        # app/controllers/line_items_controller.rb

        ➤ @cart = current_cart
        ➤ product = Product.find(params[:product_id])
        ➤ @line_item = @cart.line_items.build
        ➤ @line_item.product = product

        respond_to do |format|
          if @line_item.save
            ➤ format.html { redirect_to @line_item.cart,
              notice: 'Dodano poprawnie.' }
            format.json { render json: @line_item,
              status: :created, location: @line_item }
          else
            format.html { render action: "new" }
            format.json { render json: @line_item.errors,
              status: :unprocessable_entity }
          end
        end

      end

<!SLIDE smaller transition=fade>

# Widok koszyka
    
    @@@ html
      <!-- app/views/carts/show.html.erb -->

      <% if notice %>
        <p id="notice"><%= notice %></p>
      <% end %>

      <h2>Twoja księgarnia</h2>
      <ul>    
        <% @cart.line_items.each do |item| %>
          <li><%= item.product.title %></li>
        <% end %>
      </ul>

<!SLIDE transition=fade>

# Grupowanie produktów

<!SLIDE commandline incremental small transition=fade>

# Dodajmy liczebność do pozycji koszyka
    
    $ rails generate migration add_quantity_to_line_items quantity:integer

<!SLIDE smaller transition=fade>

# Zmiana migracji

    @@@ ruby
      # db/migrate/........rb

      class AddQuantityToLineItems < ActiveRecord::Migration
        def change
          add_column :line_items,
            :quantity,
            :integer,
            default: 1
        end
      end

    $ rake db:migrate

<!SLIDE smaller transition=fade>

# Zliczmy to teraz w modelu...
    
    @@@ ruby
      # app/models/cart.rb
      
      def add_product(p_id)

        current_item = line_items.find_by_product_id(p_id)
      
        if current_item
          current_item.quantity += 1
        else
          current_item = line_items.build(product_id: p_id)
        end
        
        # return current_item
        current_item
      end

<!SLIDE smaller transition=fade>

# ... i poprawmy kontroler

    @@@ ruby
      # app/controllers/line_items_controller.rb
      
      def create
        @cart = current_cart
        product = Product.find(params[:product_id])
      ➤ @line_item = @cart.add_product(product.id)
        @line_item.product = product

        #.....
      end

<!SLIDE commandline incremental transition=fade>

# Czas na reset :)

    $ rake db:migrate:reset
    $ rake db:fixtures:load