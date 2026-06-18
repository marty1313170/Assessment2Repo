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










# Part D - Game Mechanics

### How each round is played
Each player has a face down pile and can see only their own top card. The player who is going, picks one attribute Every player then reaveals their top card's value for that specific attribute, the values are than compared, and the person with the best one stat (whter it is higher or lower) wins. The winner takes all the played cards (or any tie cards over from an eariler draw) puts them at the bottom of their hand. They become the next caller. 

### How attributes are selected
Only the current caller chooses the  attribute that they want to compete with. They pick the strongest attirbute on their top card and will use it for this round. It can be the highest value, or for a reverse-direction stat like `km_driven` or the the lowest. Then everyone reveals their stat 

### How winners are determined
Each player value for the claled attribute is compared using that attributes win-direction from the `direction` method. Higher-win stats, horsepower, top speed and the lower-win stats are `km_driven`, goes to the lowest.

### What happens in a draw
If two or more top cards share the best value, no one wins immediately. All the played cards go into a different pile in the middle and another round is played right after, whoever wins that round collects the middle deck cards. The caller stays the same during that round

### How the game ends
The rounds repeat until one player has collected every card and the others have empty hands, so that player wins. Although most games have a cap

### Game Balance
The deck is balanced when no single card or stat can dominate over a majority. So both skill and luck matter and games stay close and competitve. Although there is a dependency on if the ***attributes*** are fair and with a wide spread so it is decisive, no attributes give a guaranteed winner eveyrtime and the values are normalised so extreme outliers can't just win immediately. So in a balanced deck, whoever happens to hold any card has a fair shot with it.

### An unfair advantage; how to fix it
The clearest one is the outlier card. If even a single card carries an extreme value which doesn't fit in with the majority of the cards, such as a car with 1000HP (horsepower) while most cars sit at 200-300 HP, someone who is dealt this card can call horsepower everytime and win eveyrtime. One card becomes an automatic win so it stops being competitive. The solution is to band every stat into a common number rating ( such as 1-10 or even 1-100), this curates the deck so values are evenly distributed rather than just sample. The card stays strong but it is beatable, so cards that hold a 9 or 10 can match it or beat it. This restores balance in the game


![Project Screenshot](structurechart.jpg)