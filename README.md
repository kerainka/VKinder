# VKinder
Chat Bot for VKontakte Group to help you find your significant other. Built with Python, SQLAlchemy, PostgreSQL, VK API and PyCharm.

## Project Structure

```
|handler
|- helper (folder for general utilities)
|--- message_sender.py
|
|- question (this is a utility module for search_handler.py)
|--- base_question.py
|--- status_question.py
|--- ... other questions ....
|
|- base_handler.py
|- search_handler.py
|- ... other handlers ...

|model
|- base.py
|- candidate.py
|- photo.py
|- user.py
|- user_to_candidate.py

|main.py
|vk_bot.py
```

## Data Model

### Properties

```
---------------------------    ------------------------    -------------------------------    --------------------------------
|           User          |    |       Candidate      |    |            Photo            |    |       user_to_candidate      |
---------------------------    ------------------------    -------------------------------    --------------------------------
| id: Integer             |    | id: Integer          |    | id: String                  |    | user_id: User.id             |
| token: String           |    | first_name: String   |    | photo_id: Integer           |    | candidate_id: Candidate.id   |
| candidates: [Candidate] |    | last_name: String    |    | candidate_id: Candidate.id  |    |                              | 
|                         |    | screen_name: String  |    | likes_count: Integer        |    |                              | 
|                         |    | photos: [Photo]      |    | comments_count: Integer     |    |                              | 
|                         |    | users: [User]        |    |                             |    |                              |
---------------------------    ------------------------    -------------------------------    --------------------------------
```

### Relationships

```
User [many]-------[many] Candidate
Candidate [one]-------[many] Photos
```

## New Handlers

You can add new message handlers in handlers folder. Make sure to inherit the `handler/base_handler.py` then add the handler in `vk_bot.py`.

## Execution

1. You need to specify `GROUP_TOKEN` and `DSN` in `main.py`. `GROUP_TOKEN` can be found in VK group settings and required for bot to respond to messages sent to the group. `DSN` is a data source name to your PostgreSQL database (eg. `postgresql://demo:demo@localhost:5432/db`).
2. To allow the bot authenticate with a user token you need to specify `CLIENT_ID` of your app in `handler/question/token_question.py`. This is necessary to perform the user search.
3. Run `main.py`
