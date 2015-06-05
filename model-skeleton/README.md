1)
SELECT COUNT(*) FROM "users"
=> 249



2)
Item.order(price: :desc).limit 5
D, [2015-06-05T13:50:38.207229 #6364] DEBUG -- :   Item Load (0.4ms)  SELECT  "items".* FROM "items"  ORDER BY "items"."price" DESC LIMIT 5
=> [#<Item:0x007fa612baf5f8
  id: 57,
  name: "Awesome Granite Hat",
  price: #<BigDecimal:7fa612b8ee48,'0.9869E2',18(36)>,
  category: "Beauty">,
 #<Item:0x007fa612baf1e8
  id: 38,
  name: "Awesome Rubber Computer",
  price: #<BigDecimal:7fa612b666c8,'0.985E2',18(36)>,
  category: "Jewelery & Beauty">,
 #<Item:0x007fa612baeec8
  id: 18,
  name: "Incredible Steel Table",
  price: #<BigDecimal:7fa612b36a18,'0.9685E2',18(36)>,
  category: "Clothing, Health & Kids">,
 #<Item:0x007fa612baec48
  id: 67,
  name: "Sleek Granite Shirt",
  price: #<BigDecimal:7fa612b065c0,'0.9682E2',18(36)>,
  category: "Home">,
 #<Item:0x007fa612baea90
  id: 55,
  name: "Intelligent Rubber Pants",
  price: #<BigDecimal:7fa612ac5d18,'0.9629E2',18(36)>,



3)
i=Item.where("category LIKE ?", "%Electronics%")

  i.order(price: :asc).limit 1
D, [2015-06-05T14:12:41.140176 #6364] DEBUG -- :   Item Load (0.3ms)  SELECT  "items".* FROM "items" WHERE (category LIKE '%Electronics%')  ORDER BY "items"."price" ASC LIMIT 1
=> [#<Item:0x007fa6139b4cc0
  id: 15,
  name: "Sleek Steel Pants",
  price: #<BigDecimal:7fa612a16f48,'0.2383E2',18(36)>,
  category: "Industrial, Outdoors & Electronics">]



4)
Address.find(1)

Address.where(user_id: 1)
D, [2015-06-05T15:09:44.615417 #6442] DEBUG -- :   Address Load (0.2ms)  SELECT "addresses".* FROM "addresses" WHERE "addresses"."user_id" = ?  [["user_id", 1]]
=> [#<Address:0x007fd6c21e85c0
  id: 1,
  user_id: 1,
  street: "3624 Felipe Islands",
  city: "West Erwintown",
  state: "Pennsylvania",
  zip: 30658>]



5)
n = Address.find(1)

  n.zip = 10108

n
=> #<Address:0x007fd6c51a9750
 id: 1,
 user_id: 1,
 street: "3624 Felipe Islands",
 city: "West Erwintown",
 state: "Pennsylvania",
 zip: 10108>



5)
j=Item.where("category LIKE ?", "%jewelery%")

  j.sum("price")
D, [2015-06-05T14:36:25.465642 #6442] DEBUG -- :    (0.2ms)  SELECT SUM("items"."price") FROM "items" WHERE (category LIKE '%jewelery%')
=> #<BigDecimal:7fd6c51fa100,'0.50467E3',18(36)>



6)
Order.sum(:quantity)
D, [2015-06-05T14:40:48.722195 #6442] DEBUG -- :    (0.3ms)  SELECT SUM("orders"."quantity") FROM "orders"
=> 6135



7)
h=Item.where("category LIKE ?", "Health")

  h.sum(:price)
D, [2015-06-05T14:43:21.740736 #6442] DEBUG -- :    (0.2ms)  SELECT SUM("items"."price") FROM "items" WHERE (category LIKE 'Health')
=> #<BigDecimal:7fd6c2d6e9f8,'0.1517E3',18(36)>



8)
pry(main)> User.find_or_create_by(first_name: 'Marky')

  Order.find_or_create_by(user_id: 251, item_id:95, quantity:)
D, [2015-06-05T14:51:26.688649 #6442] DEBUG -- :   Order Load (0.3ms)  SELECT  "orders".* FROM "orders" WHERE "orders"."user_id" = ? AND "orders"."item_id" = ? AND "orders"."quantity" = ? LIMIT 1  [["user_id", 251], ["item_id", 95], ["quantity", 1]]
D, [2015-06-05T14:51:26.689254 #6442] DEBUG -- :    (0.1ms)  begin transaction
D, [2015-06-05T14:51:26.690746 #6442] DEBUG -- :   SQL (0.9ms)  INSERT INTO "orders" ("user_id", "item_id", "quantity") VALUES (?, ?, ?)  [["user_id", 251], ["item_id", 95], ["quantity", 1]]
D, [2015-06-05T14:51:26.693285 #6442] DEBUG -- :    (2.1ms)  commit transaction
=> #<Order:0x007fd6c2ba6580 id: 1121, user_id: 251, item_id: 95, quantity: 1>