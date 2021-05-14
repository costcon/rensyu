

モデル作成



rails g model SendAddress customer_id:integer postal_code:string address:string name:string

rails g model CartItem customer_id:integer item_id:integer amount:integer

rails g model Item ganre_id:integer name:string introduction:text image_id:string price:integer is_active:boolean

rails g model Genre name:string

rails g model Order customer_id:integer postal_code:string address:string name:string shopping_cost:integer total_payment:integer payment_method:integer status:integer

rails g model OrderDetail item_id:integer order_id:integer price:integer amount:integer making_status:integer





アソシエーション




>Customer.rb
~~~customer.rb
has_many :send_addresses, dependent: :destroy
has_many :cart_items, dependent: :destroy
has_many :orders, dependent: :destroy
~~~


>SendAddress.rb
~~~send_address.rb
belong_to :customer
~~~

>CartItem.rb
~~~cart_item.rb
belong_to :customer
belong_to :item
~~~

>Order.rb
~~~order.rb

belongs_to :customer
has_many :order_details

~~~

>OrderDetail.rb
~~~order_detail.rb
belongs_to :order
belongs_to :item
~~~

>Item.rb
~~~item.rb

belong_to :Ganre
has_many :cart_items, dependent: :destroy
has_many :order_details, dependent: :destroy

~~~


>Ganre.rb
~~~ganre.rb

has_many :Items

~~~

>routes.rb
~~~route.rb

root :to => "homes#top"
get "home/about" =>"homes#about"

resources :customers
resources :admins
resources :items do
    resources :cart_items,only[:show, :destroy]
end
    
resources :order,only[:show,:comfirm,:create,:index]
get "/thanks" => "thanks#index"
resources :order_detail
resources :addresses,only[:index, :edit, :destroy]
resources ;ganre
~~~
