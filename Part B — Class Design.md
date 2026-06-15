# Part B - Class Design

# Class Name: Car - 
Car's main attributes are: 

Car Attributes
|------------|
|make_model - String
|horsepower - int
|top_speed - int
|fuel_economy - int
|safety_rating - int
|price - double
|km_driven - dobule


Car Methods
|------------|
| get_stat(attribute)
| drive()

# Class Name: Card -

Card Attributes 
|-------------|
| Car (it wraps it) - String
| Directions(in which direction is better higher or lower) - String

Card Methods
|-------------|
| get_value()
| beats(other_card, attribute)

# Class Name: Deck -

Deck Attributes
|--------------|
| cards() - int
| num_of_players() - int

Deck Methods
|-------------|
| shuffle()
| pack_up()

# Class Name: Player -

Player Attributes
|--------------|
| name_of_player() - String
| hand() - String
| wins() - int
| losses() - int
| draws() - int


Player Methods
|--------------|
| top_card(view top card)
| play_top_card() 
| add_cards()
| has_card()

# Class Name: Game -

Game Attributes
|--------------|
| players() - int
| deck() - string
| spoils( cards carreid after a tie)

Game Methods
|--------------|
| setup()
| play_round()
| turn()












