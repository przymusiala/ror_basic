<!SLIDE title-slide transition=fade>

# Część 3 #

<!SLIDE transition=fade>

# Emaile
## Poradnik młodego spammera 

<!SLIDE bullets incremental transition=fade>

# Od przybytku głowa nie boli?!
## ... Czyli jak ogarnąć dużo obiektów

  * * konfiguracja środowiska
  * * jak rails wysyła maile ? 
  * * szablony html

<!SLIDE bullets incremental transition=fade>

# Hej czy nie wiecie ? 

  * * jakie znacie protokoły obsługujące maile ?
  * * jak system operacyjny wysyła maile ?


<!SLIDE smaller transition=fade>
# Konfiguracja środowiska
    @@@ Ruby

      # config/environments/development.rb
      
      config.action_mailer.delivery_method = :sendmail

      lub

      config.action_mailer.delivery_method = :smtp
      config.action_mailer.smtp_settings = { 
        address: "smtp.gmail.com", port: 587, 
        domain: "domain.of.sender.net", 
        authentication: "plain", user_name: "dave", 
        password: "secret", enable_starttls_auto: true 
      }

<!SLIDE smaller transition=fade>
# Generujemy mailery
    @@@ Ruby
      
      $rails generate mailer OrderNotifier received 
          shipped create app/mailers/order_notifier.rb
      
      ===

        invoke erb
        create app/views/order_notifier
        create    app/views/order_notifier/received.text.erb
        create    app/views/order_notifier/shipped.text.erb
        invoke  test_unit
        create    test/functional/order_notifier_test.rb


<!SLIDE smaller transition=fade>
# Konfiguracja maila
    @@@ Ruby

      # app/mailers/order_notifier.rb

      class OrderNotifier < ActionMailer::Base
        ➤ default from: 
            'Ksiegarnia Śląska <ksiegarnia@slaska.pl>'


<!SLIDE smaller transition=fade>
# Szablony emaili
    @@@ Ruby

      # app/views/order_notifier/received.text.erb

      Witaj <%= @order.name %>,
      Dziękujemy za złożenie zamówienia w Księgarni Śląskiej
      Zamówiłeś następujące pozycje:

      <%= render @order.line_items %>

      Usiądź wygodnie i odpocznij sobie. Kiedy skompletujemy
       zamówienie poinformujemy Cię o tym mailem.

<!SLIDE smaller transition=fade>
# Konfiguracja maila c.d.
    @@@ Ruby

      # app/views/line_items/_line_item.text.erb

      <%= sprintf("%2d x %s", line_item.quantity,
        truncate(line_item.product.title, length: 50)) %>


      # app/mailers/order_notifier.rb
      def received(order)
        @order = order
        mail to: order.email, subject: 'Księgarnia Śląska - 
          Potwierdzenie zamówienia'
      end
<!SLIDE smaller transition=fade>
# Generowanie emaila
    @@@ Ruby
      # app/controllers/orders_controller.rb

      respond_to do |format| 
        if @order.save
          Cart.destroy(session[:cart_id])
          session[:cart_id] = nil
        
          ➤ OrderNotifier.received(@order).deliver
        
          format.html { redirect_to store_url, notice: 
            'Thank you for your order.' }
          format.json { render json: @order, 
          status: :created, location: @order }

<!SLIDE smaller transition=fade>
# Tworzymy wysyłkę zamówienia
    @@@ Ruby
      # app/mailers/order_notifier.rb

      def shipped(order)
        @order = order
        mail to: order.email, subject: 'Księgarnia Śląska 
                - zamówienie zostało wysłane'
      end
<!SLIDE smaller transition=fade>
# Definiujemy widok wysyłki
    @@@ html
      
      <#!-- app/views/order_notifier/shipped.html.erb --> 
      
      <h3>Księgarnia Śląska - Zamówienie</h3> <p>
        Właśnie wysłaliśmy Twoje zamówienie:
      </p> <table>
      <tr><th colspan="2">Il.</th>
      <th>Opis</th></tr> 
        <%= render @order.line_items %>
      </table>

<!SLIDE smaller transition=fade>
# Partiale zawsze się nam przydają
## Nie musimy nic robić... 

    @@@ html
      <#!-- app/views/line_items/_line_item.html.erb --> 

      <% if line_item == @current_item %> 
        <tr id="current_item">
      <% else %>
        <tr>
      <% end %>
      <td><%= line_item.quantity %>&times;</td>
      <td><%= line_item.product.title %></td>
      <td class="item_price"><%= number_to_currency(line_item.total_price) %></td>
      </tr>  
