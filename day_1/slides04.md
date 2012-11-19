<!SLIDE title-slide transition=fade>

# Część 4 #

<!SLIDE smaller incremental transition=fade>

# Tworzenie aplikacji bazodanowej. #
## ORM? ##
      
      Tabela: users
      Model: User

## Dzięki ORMowi mamy automatyczny dostęp do wszystkich pól w tabeli ##
## Są one zmapowane na metody obiektu ##

    @@@ ruby
      user = User.first
      user.email

<!SLIDE transition=fade>

# Operacje na ActiveRecord #

<!SLIDE smaller transition=fade>

# find #

    @@@ ruby
      User.find(1)
      User.find_by_email('adam@google.com')
      User.find_all_by_email('adam@google.com')

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE smaller transition=fade>

# where #

    @@@ ruby
      User.where(:email => 'adam@google.com')

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE smaller transition=fade>

# conditions #

    @@@ ruby
      # parametry z sieci są eskejpowane

      User.find(:first, 
        :conditions => ['email = ?', params[:email]]
      ) 

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE smaller transition=fade>

# select #
    
    @@@ ruby
      User.find(:first,
        :conditions => ['email = ?', params[:email]], 
        :select => [:first_name, :email]
      )          

<!SLIDE transition=fade>

# Zadanie #
## Treść zadania ##

<!SLIDE code transition=fade>

    @@@ ruby

<!SLIDE smaller transition=fade>

# Operacja na bazie #
    
    @@@ ruby
      Order.where(name: 'dave').each do |order|
        order.pay_type = "Purchase order"
        order.save
      end

<!SLIDE transition=fade>

# Relacje: #
    @@@ ruby
      has_many
      has_one
      belongs_to

<!SLIDE transition=fade>

    @@@ ruby
      # app/models/post.rb
      has_many :comments

      # app/models/comment.rb
      belongs_to :post

<!SLIDE transition=fade>

# Zadanie #
## Stworzyć post i dodać do niego komentarz przez konsolę ##
