# Austin Hobart

#A dictionary for the simplified dragon text game
#The dictionary links a room to other rooms.
rooms = {
        'Great Hall': {'South': 'Bedroom'},
        'Bedroom': {'North': 'Great Hall', 'East': 'Cellar'},
        'Cellar': {'West': 'Bedroom'}
    }

# I changed my original idea of the game to a more standard version to go along with the video
# Also I am submitting all my code that I have done for the game
# declaration

rooms = {
    'Great Hall': {'South': 'Bedroom', 'North': 'Dungeon', 'East': 'Kitchen', 'West': 'Library', 'Item': 'Shield'},
    'Bedroom': {'North': 'Great Hall', 'East': 'Cellar', 'Item': 'Armor'},
    'Cellar': {'West': 'Bedroom', 'Item': 'Helmet'},
    'Dining Room': {'South': 'Kitchen', 'Item': 'Dragon'},
    'Kitchen': {'West': 'Great Hall', 'North': 'Dining Room', 'Item': 'Sandwich'},
    'Dungeon': {'South': 'Great Hall', 'Item': 'Sword'},
    'Library': {'East': 'Great Hall', 'Item': 'Book'}

}
state = 'Great Hall'


def get_new_state(state, direction):
    new_state = state
    for i in rooms:
        if i == state:
            if direction in rooms[i]:
                new_state = rooms[i][direction]
    return new_state


def get_item(state):
    return rooms[state]['Item']


def show_instructions():
    print('Dragon Text Adventure Game')
    print('Collect 6 items to win the game, or be eaten by dragon.')
    print('Move commands: go South, go North, go East, go West')
    print("Add to Inventory: get 'item_name'")


show_instructions()
Inventory = []
items = ['Shield', 'Sword', 'Sandwich', 'Peanut butter', 'Book', 'Armor', 'Helmet']
while (1):
    print('You are in ', state)
    print('Inventory:', Inventory)
    item = get_item(state)
    print('You see a ', item)
    print('--------------------')
    if item == 'Dragon':
        print('NOM NOM...GAME OVER!')
        exit(0)
    direction = input('Enter your move: ')
    if direction == 'go East' or direction == 'go West' or direction == 'go North' or direction == 'go South':
        direction = direction[3:]
        new_state = get_new_state(state, direction)
        if new_state == state:
            print('The room has wall in that direction enter other direction!')
        else:
            state = new_state
    elif direction == str('get ' + item):
        if item in Inventory:
            print('Item already taken go to another room!!')
        else:
            Inventory.append(item)
    else:
        print('Invalid input or move or item')
    if len(Inventory) == 6:
        print('Congratulations! You have collected all items and defeated the dragon!')
        exit(0)
