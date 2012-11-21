<!SLIDE title-slide transition=fade>

# Część 3 #

<!SLIDE transition=fade>
# Modyfikacja interfejsu użytkownika


<!SLIDE bullets incremental transition=fade>
## Tworzymy widok podglądu koszyka

  * partiale
  * renderowanie partiali
  * zasada DRY

<!SLIDE smaller transition=fade>
    
    @@@ html
      <!--app/views/carts/show.html.erb -->

      <% if notice %>
        <p id="notice"><%= notice %></p>
      <% end %>

      <h2>Twój Koszyk</h2>
      <table>
        <%= render(@cart.line_items) %>
        <tr class="total_line">
          <td colspan="2">Razem</td>
          <td class="total_cell">
            <%= number_to_currency(@cart.total_price) %>
          </td>
        </tr>
      </table>

      <%= button_to 'Opróżnij', @cart, method: :delete,
          data: { confirm: 'Czy aby na pewno?' } %>


<!SLIDE smaller transition=fade>
## Tworzymy partial z elementami koszyka

    @@@ html
      <!-- app/views/line_items/_line_item.html.erb -->
      <tr>
        <td><%= line_item.quantity %>&times;</td>
        <td><%= line_item.product.title %></td>
        <td class="item_price">
          <%= number_to_currency(line_item.total_price) %>
        </td>
      </tr>

<!SLIDE bullets incremental smaller transition=fade>
## Renderowanie z bliska

    @@@ html 
      wystarzczy poprzedni partial oraz wywołanie render

     ➤ <%= render(@cart.line_items) %>



      Zamiast pisac tyle kodu :

      <% @cart.line_items.each do |item| %> 
        <tr>
          <td><%= item.quantity %>&times;</td>
          <td><%= item.product.title %></td>
          <td class="item_price">
            <%= number_to_currency(item.total_price) %>
          </td>
        </tr>
      <% end %>

<!SLIDE transition=fade>
## A teraz napiszmy partial koszyka


<!SLIDE smaller transition=fade>
## Definicja partialu Koszyk

    @@@ html
      <!-- app/views/carts/_cart.html.erb -->

      <h2>Twój koszyk</h2>
      <table>
        <%= render(cart.line_items) %>
        <tr class="total_line">
          <td colspan="2">Razem</td>
          <td class="total_cell">
            <%= number_to_currency(cart.total_price) %>
          </td> 
        </tr>
      </table>
      <%= button_to 'Opróżnij koszyk', cart, method: 
            :delete, data: { confirm: 'Czy aby na pewno?' } %>

<!SLIDE transition=fade>
## Wyrenderujmy box z koszykiem w layoucie

<!SLIDE smaller transition=fade>

    @@@ html
      <!-- app/views/layouts/application.html.erb -->

      znajdź linie :
      
      <div id="columns">
        <div id="side"> 
          
      
      poniżej dodaj te 3 linie :

        ➤  <div id="cart">
        ➤    <%= render @cart %>
        ➤  </div>


<!SLIDE transition=fade>
## Ale box nam jeszcze nie zadziała bo... 

<!SLIDE small transition=fade>
## Musimy wyszukać koszyk w kontrolerze


    @@@ Ruby 
      # app/controllers/store_controller.rb 

      def index
        @products = Product.order(:title) 
      ➤  @cart = current_cart
      end

<!SLIDE transition=fade>
## Zmiana przepływu akcji w kontrolerze

<!SLIDE smaller transition=fade>
## Po zapisaniu koszyka przekierowujemy do strony głownej sklepu.

    @@@ Ruby 
      # app/controllers/line_items_controller.rb

      respond_to do |format| 
        if @line_item.save
        ➤  format.html { redirect_to store_url } 
          format.json { render json: @line_item,
        end
      end


<!SLIDE transition=fade>
## Praca z AJAXem czystym relaksem


<!SLIDE smaller transition=fade>
## Dodajemy przycisk w widoku sklepu

    @@@ html
      <!-- app/views/app/views/store/index.html.erb -->

      <span class="price">
        <%= number_to_currency(product.price) %>
      </span> 

     ➤ <%= button_to 'Do koszyka', 
      line_items_path(product_id: product), remote: true %>

<!SLIDE smaller transition=fade>
## Dodajemy obslugę ajaxa w kontrolerze

    @@@ Ruby
    
    # app/controllers/line_items_controller.rb
    # def create

    respond_to do |format| 
      if @line_item.save
        format.html { redirect_to store_url }
      ➤  format.js

<!SLIDE smaller transition=fade>
## Tworzymy plik JS
    @@@ html
      <!-- app/views/app/views/line_items/create.js.erb -->

    ➤  $('#cart').html("<%=j render @cart %>");

