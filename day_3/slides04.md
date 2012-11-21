<!SLIDE title-slide transition=fade>

# Część 4 #

<!SLIDE transition=fade>

# jQuery i skrypty Client-side


<!SLIDE transition=fade>
## Plik manifestowy Javascriptów

    @@@ Ruby
      # assets/javascripts/application.js
      //= require jquery
      //= require jquery-ui
      //= require jquery_ujs
      //= require_tree .


<!SLIDE small transition=fade>
## Dodajemy obsługę formatu wyjscia JS

    @@@ Ruby 
      # app/controllers/line_items_controller.rb

      respond_to do |format| 
        if @line_item.save
          format.html { redirect_to store_url }    
          format.js       # tutaj dodałem
          format.json { render json: @line_item,
        end
      end


<!SLIDE smaller transition=fade>
## Dynamicznie oznaczamy wybrany obiekt

    @@@ html
      <!-- app/views/line_items/_line_item.html.erb -->

      <% if line_item == @current_item %>
        <tr id="current_item">
      <% else %>
        <tr>
      <% end %>

<!SLIDE smaller transition=fade>
## Animujemy podświetlenie
    @@@ html
      <!-- app/views/line_items/create.js.erb -->

      $('#cart').html("<%=j render @cart %>");


      Dodajemy te linie : 

      $('#current_item').css({'background-color':'#88ff88'}).
      animate({'background-color':'#114411'}, 1000);


<!SLIDE transition=fade>

# Efekty wizualne w JavaScript

