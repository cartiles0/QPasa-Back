# QPasa_Back

## CONCEPT
A web page which offers complete and detailed information about all public events that may interest the user. Each user chooses and defines what is useful and of interest to the user.

## OBJECTIVE
An easy, fast and useful demand aggregation platform to match users and organizers. The platform will create public events, and provide users with the information and sale of tickets for the events.

## EVENT CATEGORIES
- Concerts
- Conferences/Workshops
- Expo/Fairs
- Festivals
- For Kids
- Gastronomy
- Parties
- Retreats
- Shows
- Sports
- Theater/Film

# DB SCHEMAS

## USER

| KEY             | TYPE         | REFERENCE | REQUIRED | VALIDATION     |
|-----------------|--------------|-----------|----------|----------------|
| name            | string       |           | YES      |                |
| lastName        | string       |           | NO       |                |
| username        | string       |           | YES      | Unique         |
| email           | string       |           | YES      | RegExp, Unique |
| password        | string       |           | YES      |                |
| photo           |              |           | YES      |                |
| areaPreference  | string       |           | YES      |                |
| address         | string       |           | YES      |                |
| rating          | number       |           | NO       |                |
| aboutMe         | string       |           | NO       |                |
| yourEvents      | [ ObjectId ] | Events    | NO       |                |
| savedEvents     | [ ObjectId ] | Events    | NO       |                |
| attendingEvents | [ ObjectId ] | Events    | NO       |                |

## EVENTS

| KEY         | TYPE         | REFERENCE | REQUIRED | VALIDATION     |
|-------------|--------------|-----------|----------|----------------|
| title       | string       |           | YES      |                |
| description | string       |           | YES      |                |
| eventDate   | date         |           | YES      |                |
| capacity    | number       |           | YES      |                |
| price       | number       |           | YES      |                |
| photos      |              |           | YES      |                |
| category    | string       |           | YES      |                |
| creator     | [ ObjectId ] | Users     | NO       |                |
| address     | [ ObjectId ] | Users     | NO       |                |
| saved       | [ ObjectId ] | Users     | NO       |                |
| attendance  | [ ObjectId ] | Users     | NO       |                |
| views       | number       |           | NO       |                |
| tags        | [ ObjectId ] | Tags      | NO       |                |
| dateCreated | date         |           | NO       |                |

## TAGS

| KEY    | TYPE   | REFERENCE | REQUIRED | VALIDATION     |
|--------|--------|-----------|----------|----------------|
| name   | string |  Users    | YES      |                |
| clicks | number |           | YES      |                |


# API ROUTES

## AUTHENTICATION ENDPOINTS

| METHOD | URL            | AUTH | FUNCTION             |
|--------|----------------|------|----------------------|
| POST   | '/auth/signup' | NO   | Create a new account |
| POST   | '/auth/login'  | NO   | Authenticate a user  |

## USERS ENDPOINTS

| METHOD | URL               | AUTH | FUNCTION                    |
|--------|-------------------|------|-----------------------------|
| GET    | '/users/:id'.     | NO   | Get user profile            |
| GET    | '/users/me'       | YES  | Get registered user profile |
| PUT    | '/users/me'       | YES  | Edit user profile           |
| PUT    | '/users/me/photo' | YES  | Edit users photo            |
| DELETE | '/users/me'       | YES  | Delete user account         |

## EVENTS ENDPOINTS

| METHOD | URL                                       | AUTH | FUNCTION                              |
|--------|-------------------------------------------|------|-------------------------------------- |
| GET    | '/events/:eventId'.                       | NO   | Look at an event                      |
| GET    | '/events/tags/:tagId'                     | NO   | List all events of a specific tag     |
| GET    | '/events/search/:term'                    | NO   | List all events of a specific search  |
| POST   | '/events/me'                              | YES  | Create an event                       |
| PUT    | '/events/me/:eventId'                     | YES  | Update event information              |
| PUT    | '/events/me/:eventId/saved'               | YES  | Increase event saved                  |
| PUT    | '/events/me/:eventId/attendance'          | YES  | Increase event attendance             |
| PUT    | '/events/:eventId/views'                  | NO   | Increase event views                  |
| DELETE | '/events/me/:eventId'                     | YES  | Delete an event                       |

## TAG ENDPOINTS

| METHOD | URL                 | AUTH | FUNCTION                         |
|--------|-------------------- |------|----------------------------------|
| GET    | '/tag'              | NO   | List all tags                    |
| POST   | '/tags/:tagId/click | NO   | Increases a tag amount of clicks |

