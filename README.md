# Lambda MUD

> Link to [Landing Page]()

> Link to [backend API](https://lambdamud-be.herokuapp.com/admin/)

## What is a MUD?

> A MUD...is a multiplayer real-time virtual world, usually text-based. MUDs combine elements of role-playing games, hack and slash, player versus player, interactive fiction, and online chat. Players can read or view descriptions of rooms, objects, other players, non-player characters, and actions performed in the virtual world. Players typically interact with each other and the world by typing commands that resemble a natural language. - Wikipedia

## How to install the project?

### Download Project Files

- **Fork** and **Clone** this repository.
- **CD into the folder** where you cloned the repository.
- pipenv install to install all the necessary packages.
- manage.py makemigrations
- manage.py migrate
- ** Have to setup these environment variables**
- SECRET_KEY: a secret string
- In production - Have to add the Postgres add-on to Heroku
- DEBUG: False
- ALLOWED_HOSTS: .herokuapp.com

## API Endpoints

### Auth Endpoints

| Method | Endpoint           | Description                                                                                                                                                                |
| ------ | ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| POST   | /api/registration/ | Creates a `user` sent inside the `body` of the request in the form of {username, password1, password2}. Returns a key.                                                     |
| POST   | /api/              | Uses the credentials sent inside the `body` {username, password} to authenticate the user. On successful login, returns a token to be used to access restricted endpoints. |
| POST   | /api/make_maze/    | Uses the passed rows and columns numbers to generates a maze built with rooms. Returns a list containing the information for each room in the maze.                        |

### Adv endpoints

| Method | Endpoint       | Description                                                                                             |
| ------ | -------------- | ------------------------------------------------------------------------------------------------------- |
| GET    | /api/adv/init  | Initializes the player with the current user                                                            |
| GET    | /api/adv/reset | Reset the player's position to the first room                                                           |
| POST   | /api/adv/move  | Moves the player in the direction ('n', 's', 'w', 'e'). If the move is allowed, returns new coordinates |

## Data Models

### Room Data Model

| Field  | Type    | Description                                           |
| ------ | ------- | ----------------------------------------------------- |
| id     | Integer | ID of the newly created room.                         |
| row    | Integer | Row number where the room is situated in the maze.    |
| column | Integer | Column number where the room is situated in the maze. |
| wall_n | Boolean | To signal if the room has a wall to the north         |
| wall_s | Boolean | To signal if the room has a wall to the south         |
| wall_e | Boolean | To signal if the room has a wall to the east          |
| wall_w | Boolean | To signal if the room has a wall to the west          |

### Player Data Model

| Field        | Type    | Description                             |
| ------------ | ------- | --------------------------------------- |
| id           | Integer | ID of the newly created room.           |
| user         | ID      | id of the current user.                 |
| current_room | Integer | id of the player's current room.        |
| uuid         | ID      | special id used to identify the player. |
