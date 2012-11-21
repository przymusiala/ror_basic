<!SLIDE title-slide transition=fade>

# Część 1 #

<!SLIDE smaller bullets incremental transition=fade>

# Nowe CSSy do pobrania:

  * [application.css.scss] (https://github.com/przymusiala/ror_basic/blob/master/day_4/assets/application.css.scss) do app/assets/stylesheets/application.css.scss
  * [store.css.scss] (https://github.com/przymusiala/ror_basic/blob/master/day_4/assets/store.css.scss) do app/assets/stylesheets/store.css.scss

<!SLIDE commandline incremental transition=fade>

# Obsługa zamówienia - przyśpieszamy :)

    $ rails generate scaffold order name:string address:text \
      email:string pay_type:string

    $ rails generate migration add_order_id_to_line_item \
      order_id:integer

    $ rake db:migrate

<!SLIDE smaller transition=fade>

# Dodajmy przycisk złożnia zamówienia

    @@@ html
      <!-- app/views/carts/_cart.html.erb -->

      <%= button_to "Zamawiam!", new_order_path, method: :get %>

<!SLIDE smaller transition=fade>

# Zabezpieczmy się na pusty koszyk

    @@@ ruby
      # app/controllers/orders_controller.rb
      
      def new
        @cart = current_cart
        if @cart.line_items.empty?
          redirect_to store_url, notice: "Koszyk jest pusty"
      ➤   return
        end
      end

<!SLIDE smaller transition=fade>

# Stałe w modelu Order...

    @@@ ruby
      # /app/models/order.rb
      
      class Order < ActiveRecord::Base
      ➤ PAYMENT_TYPES = [ "Przelew", "Odbiór własny" ]
      end

<!SLIDE smaller transition=fade>

# ...i ich użycie:

    @@@ html
      <!-- app/views/orders/_form.html.erb -->
      
      <div class="field">
        <%= f.label :pay_type %><br />
      ➤ <%= f.select :pay_type, Order::PAYMENT_TYPES,
      ➤   prompt: 'Wybierz metodę płatności' %>
      </div>

<!SLIDE smaller transition=fade>

# Walidacje w zamówieniu
    
    @@@ ruby
      validates :name, :address, :email, presence: true
      validates :pay_type, inclusion: PAYMENT_TYPES

<!SLIDE smaller bullets incremental transition=fade>

# Uzupełnijmy metodę create kontrolera zamówień

  * Przechwycamy wartości wysłane formularzem aby uzupełnić wartości obiektu klasy Order
  * Dodajemy pozycje z koszyka do zamówienia
  * Walidujemy i zapisujemy zamówienie. Jeśli są błędy dajemy odpowieni komunikat aby użytkownik poprawił dane
  * Po zapisaniu zamówienia kasujemy koszyk i wyświetlamy odpowiedni komunikat na stronie głównej

<!SLIDE smaller transition=fade>

# Dodajemy odpowiednią relację

    @@@ ruby
      # app/models/line_item.rb
      
      class LineItem < ActiveRecord::Base
      ➤  belongs_to :order

        # ...

      end

      # app/models/order.rb
      
      class Order < ActiveRecord::Base
      ➤  has_many :line_items, dependent: :destroy
      
        # ...

      end

<!SLIDE smaller transition=fade>

# Dodajemy pozycje koszyka do zamówienia
  
    @@@ ruby
      # app/controllers/orders_controller.rb
      
      def create
        @order = Order.new(params[:order])
      ➤ @order.add_line_items_from_cart(current_cart)
        
        respond_to do |format|
          if @order.save
      ➤    Cart.destroy(session[:cart_id])
            session[:cart_id] = nil
            format.html { redirect_to store_url,
              notice: 'Dziękujemy.' }
            format.json { render json: @order, 
              status: :created, location: @order }
          else
            @cart = current_cart
            format.html { render action: "new" }
            format.json { render json: @order.errors,
              status: :unprocessable_entity }
          end
        end
      end

<!SLIDE smaller transition=fade>

# Tajemnicza metoda
## add\_line\_items\_from\_cart
    
    @@@ ruby
      # app/models/order.rb
      
      class Order < ActiveRecord::Base

        # ...
        
      ➤  def add_line_items_from_cart(cart)
      ➤    cart.line_items.each do |item|
      ➤      item.cart_id = nil
      ➤      line_items << item
      ➤    end
      ➤  end
      end