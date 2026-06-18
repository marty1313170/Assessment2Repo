# Part B - Class Design

# Class Name: Car - 
Car's main attributes are: 

Car Attributes| Type | Description | 
|-------------|------|-------------|
|make_model    | String | The car's name 
|horsepower    | int    | Engine Power (hp)
|top_speed     | int    | max speed(km/h)
|fuel_economy  | int    | efficiency (km per litre)
|safety_rating | int    | ANCAP safety score as a %
|price         | double | Listing Price (AUD)
|km_driven     | double | Odometer reading (km)


### Methods
Car Methods| Description
|---------|-----|
| get_stat(attribute)| Returns the value of the named stat
| drive()| behaviour for the car object

**Role**: The *Car* class holds the raw car data from a listing, it represents one real-world car as pure information, it stores the six stats that we made from the lisitng. We keep the source data as isolated, so changing the data source never disturbs the game's rules.

![Toyota example car][https://car-images.bauersecure.com/wp-images/3995/toyota_highlander_55.jpg]

# Class Name: Card -

Card Attribute|Type |Description
|-------------|-----|------------|
| car | String | the Car Object this card wraps
| Directions() | Dictionary | maps each attribute to its win direction whether that is higher or lower

Card Methods | Description
|-------------|------|
| get_value(attribute) | reads a stat off the wrapped car
| beats(other_card, attribute) | compares the stat with other cards

**Role:** This is essentially the gap between data and gamplay, its role is to turn car into something playable. It wraps one *Car* and adds logic which is direction of the stat that wins, whether that is lower or higher and its ability to compare its self to another card. Its a unit that can be move around the table and changes hands.

![Toyota example car][https://i.ebayimg.com/images/g/pmEAAOSwCVZhXdP0/s-l1200.jpg]

# Class Name: Deck -

Deck Attributes | Type | Description
|--------------|-------|-----------|
| cards() | String | lists the full set of cards in the deck
| num_of_players() | int | how many cards to deal to

Deck Methods | Description
|-------------|-------|
| shuffle() | ramdonises the card deck
| pack_up() | collects the cards back together
| deal_cards() | gives cards to the players
| build_deck() | puts the card into the pile to start shuffle() and deal()

**Role:** The Deck is the manager. It holds the full set of cards before play begins, shuffles them for fairness, and deals them out. Once the cards are in players' hands its job is essentially done.

# Class Name: Player -

Player Attributes | Type | Description
|--------------|--------|-------------|
| name_of_player() | String | player's name
| hand() | String | the cards the player currently holds
| wins() | int | rounds won
| losses() | int | rounds lost
| draws() | int | rounds drawn


Player Methods| Description
|--------------|-----------|
| top_card() | view the top card
| play_top_card() | remove top card 
| add_cards() | add won cards to the hand
| has_card() | whether the player still has cards

**Role**:The player is the decision-maker, it represent the one participant and their own pile of cards. Its the class that makes the *choice*, it selects what stats to call when it is their turn, and manages its own hand, by playing the top card. Each player is indepedent and no other class can/should reach into it.

# Class Name: Game -

Game Attributes | Type
|--------------|------|
| players | List of `Player` | all the players in the game
| deck    | `Deck` | the deck used to set up the game
| spoils | List of `Card` | cards carried over 

Game Methods | Description
|--------------|-----|
| setup() | shuffles card and deals
| play_round() | runs one round of play
| turn() | advances to the next players turn
| reveal() | reveal cards
| award_cards() | award cards to the winner


**Role**:The game is the contoller and creator, its role is run everything and enforce the rules. It sets the game up through *Deck*, and uses the round-by-round loop and compares played card, resolves wins and ties. It manages the cards that are given to the winner and allows the *Player* to know when the game is over and coordinates every other class. 


hrough the overall chain, `Car` supplies the data, `Card` makes the game actually work, `Deck` deals it out, `Player` chooses and `Game` wraps everything and organsies everything.








