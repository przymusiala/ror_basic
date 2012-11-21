<!SLIDE title-slide transition=fade>

# Część 2 #

<!SLIDE transition=fade>

# Przyjazna użytkownikowi obsługa błędów

<!SLIDE transition=fade>

## Jest bezpiecznie, ale może być łądniej
[Widok błędu] (http://localhost:3000/carts/bla-bla-bla)

<!SLIDE smaller transition=fade>

# Przechwyćmy wyjątek
    @@@ ruby
      # app/controllers/carts_controller.rb

      def show
      ➤  begin
           @cart = Cart.find(params[:id])
      ➤  rescue ActiveRecord::RecordNotFound
      ➤    redirect_to store_url, notice: 'Błędny koszyk'
      ➤  else
           respond_to do |format|
             format.html
             format.json { render json: @cart }
           end
      ➤  end
      end

<!SLIDE transition=fade>

# Usuwanie produktów z koszyka

<!SLIDE smaller transition=fade>

# W widoku...
    @@@ html
      <!-- /app/views/carts/show.html.erb -->
      
      <ul>
        <% @cart.line_items.each do |item| %>
          <li>
      ➤    <%= item.quantity %>
            &times;
            <%= item.product.title %>
          </li>
        <% end %>
      </ul>
      ➤ <%= button_to 'Wyczyść koszyk', @cart, 
        method: :delete, data: { confirm: 'Czy aby na pewno?' }
      %>

<!SLIDE smaller transition=fade>

# ... i w kontrolerze

    @@@ ruby
      # app/controllers/carts_controller.rb
      
      def destroy
      ➤ @cart = current_cart
      ➤ @cart.destroy
      ➤ session[:cart_id] = nil

        respond_to do |format|
      ➤  format.html { redirect_to store_url,
      ➤    notice: 'Wyczyszczono koszyk' }
          format.json { head :no_content }
        end
      end

<!SLIDE small transition=fade>

# Podliczmy klienta, przygotujmy modele

    @@@ ruby
      # app/models/line_item.rb
      
      def total_price
        product.price * quantity
      end

      # app/models/cart.rb
      
      def total_price
        line_items.to_a.sum { |item| item.total_price }
      end

<!SLIDE smaller transition=fade>

# Wyświetlmy sumę w koszyku

    @@@ html
      <!-- app/views/cart/show.html.erb -->

      <h2>Twój koszyk</h2>
      <table>
        <% @cart.line_items.each do |item| %>
          <tr>
            <td><%= item.quantity %>&times;</td>
            <td><%= item.product.title %></td>
            <td class="item_price">
      ➤      <%= number_to_currency(item.total_price) %>
            </td>
          </tr>
        <% end %>
        <tr class="total_line">
          <td colspan="2">Total</td>
          <td class="total_cell">
      ➤    <%= number_to_currency(@cart.total_price) %>
          </td>
        </tr>
      </table>

[CSS] (https://github.com/przymusiala/ror_basic/blob/master/day_3/assets/carts.css.scss)

<!SLIDE smaller transition=fade>

# Teraz po polsku

* Pobieramy [pl.yml] (https://raw.github.com/svenfuchs/rails-i18n/master/rails/locale/pl.yml)
* Wrzucamy pl.yml do config/locales/
* W config/application.rb ustawiamy język polski
        config.i18n.default_locale = :pl
* Resetujemy serwer (ctrl + c)

<!SLIDE smaller transition=fade>

# Przetestujmy to