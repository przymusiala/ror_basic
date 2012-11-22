<!SLIDE title-slide transition=fade>

# Część 2 #

<!SLIDE transition=fade>

# Autoryzacja użytkownika na przykładzie CanCan'a

<!SLIDE bullets incremental transition=fade>

# Instalacja

  * Dodajemy do Gemfile:
    gem "cancan"
  * $ bundle install

<!SLIDE commandline incremental transition=fade>

# Definiowanie uprawnień

### Prawa dostępu usera definiowane są w klasie _Ability_, wygenerujmy ją:

    $ rails g cancan:ability

<!SLIDE smaller transition=fade>
      
    @@@ ruby
      # app/models/ability.rb

      class Ability
        include CanCan::Ability
        
        # Przykładowe uprawnienia
        def initialize(user)
          user ||= User.new # Gość (nie zalogowany)

          if user.admin?
            can :manage, :all
          else
            can :read, :all
          end
        end
      end
      
      # can :manage, :all if user.role == "admin"
      # can :update, Product
      # can :manage, Product  # user może wszystko z Product
      # can :read, :all       # user może czytać każdy obiekt
      # can :manage, :all     # user może wszystko ;)

<!SLIDE smaller transition=fade>

# Użycie

## Uprawnienia użytkownika sprawdzamy przy użyciu metod __can?__ i __cannot?__ zarówno w widoku jak i w kontrolerze

<!SLIDE smaller transition=fade>

## Przykład dla widoku:

    @@@ html

      <% if can? :update, @product %>
        <%= link_to "Edytuj", edit_product_path(@product) %>
      <% end %>

<!SLIDE smaller transition=fade>

## Przykład dla kontrolera:

    @@@ ruby
      # app/controllers/application_controller.rb

      def show
        @product = Product.find(params[:id])
        authorize! :read, @product
      end

### lub

    @@@ ruby
      # app/controllers/product_controller.rb

      class ProductController < ApplicationController
      ➤ load_and_authorize_resource :only => [:index, :show]

        def show
          # @product jest już załadowany i zautoryzowany
        end
      end

<!SLIDE smaller transition=fade>

# Wiele różnych ról
    
    @@@ ruby
      # app/models/user.rb
      
      class User < ActiveRecord::Base
        ROLES = %w[admin moderator author banned]
      end

      $ rails generate migration add_role_to_users role:string
      $ rake db:migrate

      # users/_form.html.erb
      
      <%= f.collection_select :role, User::ROLES, :to_s, :humanize %>

<!SLIDE smaller transition=fade>

# Obsługa nieautoryzowanego dostępu

    @@@ ruby
      # app/controllers/application_controller.rb

      class ApplicationController < ActionController::Base
      ➤ rescue_from CanCan::AccessDenied do |exception|
      ➤   redirect_to root_url, :alert => "Nie masz dostępu"
      ➤ end
      end

<!SLIDE smaller transition=fade>

# Automatyczne sprawdzenie autoryzacji dla wszystkich kontrolerów
    
    @@@ ruby
      # app/controllers/application_controller.rb

      class ApplicationController < ActionController::Base
        check_authorization
      end

<!SLIDE smaller transition=fade>

# Pominięcie autoryzacji

    @@@ ruby
      # app/controllers/store_controller.rb

      class StoreController < ActionController::Base
        skip_authorization_check
      end
