<!SLIDE title-slide transition=fade>

# Część 4 #

<!SLIDE transition=fade>

## Rozwijanie własnych widoków, helpery, ##
## formatowanie walut, testy kontrolerów ##

<!SLIDE commandline incremental transition=fade>

# Oddzielny widok dla wszystkich produktów #
    $ rails generate controller Store index

<!SLIDE small transition=fade>

# Ustawmy stronę główną na index produktów #
    @@@ ruby
      # config/routes.rb

      Ksiegarnia::Application.routes.draw do 
        get "store/index"
        resources :products

        root to: 'store#index', as: 'store'
      end

    $ rm public/index.html
    $ rake routes

<!SLIDE transition=fade>

# Pobierzmy wszystkie produkty #
# posortowane tytułami #

<!SLIDE small transition=fade>

    @@@ ruby
      # app/controllers/store_controller.rb

      class StoreController < ApplicationController
        def index
          @products = Product.order(:title)
        end
      end

<!SLIDE transition=fade>

# Ale niech to jakoś wygląda... #

<!SLIDE smaller transition=fade>

    @@@ html
      <!-- app/views/store/index.html.erb  -->

      <% if notice %>
        <p id="notice"><%= notice %></p>
      <% end %>

      <h1>Nasze książki</h1>

      <% @products.each do |product| %>
        <div class="entry">
          <%= image_tag(product.image_url) %>
          <h3><%= product.title %></h3>
          <p><%= sanitize(product.description) %></p>
          <div class="price_line">
            <span class="price"><%= product.price %></span>
          </div>
        </div>
      <% end %>

<!SLIDE smaller transition=fade>

# Czas na główny layout #

<!SLIDE smaller transition=fade>

    @@@ html
      <!-- app/views/layouts/application.html.erb -->

      <body class="<%= controller.controller_name %>">
        <div id="banner">
          <%= @page_title || "Nasza księgarnia" %>
        </div>
        <div id="columns">
          <div id="side">
            <ul>
              <li><%= link_to 'link 1', '#' %></li>
              <li><%= link_to 'link 2', '#' %></li>
              <li><%= link_to 'link 3', '#' %></li>
              <li><%= link_to 'link 4', '#' %></li>
            </ul>
          </div>
          <div id="main">
            <%= yield %>
          </div>
        </div>
      </body>

<!SLIDE smaller transition=fade>

# Lepsza cena #

<!SLIDE smaller transition=fade>

## Trochę skomplikowane ##
    @@@ html
      <!-- app/views/store/index.html.erb -->

      <span class="price">
        <%= sprintf("$%0.02f", product.price) %>
      </span>

<!SLIDE smaller transition=fade>

## Tak już dużo lepiej ##
    @@@ html
      <!-- app/views/store/index.html.erb -->

      <span class="price">
        <%= number_to_currency(product.price) %>
      </span>

<!SLIDE smaller transition=fade>

## Przetestujmy to ;) ##

    @@@ ruby
      # test/functional/store_controller_test.rb

      require 'test_helper'

      class StoreControllerTest < ActionController::TestCase
        test "should get index" do
          get :index
          assert_response :success
          assert_select '#columns #side a', minimum: 4
          assert_select '#main .entry', 3
          assert_select 'h3', 'Moja książka'
          assert_select '.price', /\$[,\d]+\.\d\d/
        end
      end

    $ rake test