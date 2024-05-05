# Media Hub API Design Document

## Overview
The Media Hub API serves as the backend for the Media Hub web application. It provides endpoints for user authentication, media tracking, playlist management, data visualization, and integration with third-party streaming platforms.

## Base URL

http://media-hub.com/

## Authentication
Access to the media-hub API does not require authentication for public assessment. However, certain endpoints may necessitate authentication for specific operations such as creating or updating user and user data.

## Error Handling

The API returns appropriate HTTP status codes and error messages in case of errors. Detailed error handling is implemented to ensure a smooth user experience.

## Endpoints

### User Authentication

#### POST /api/auth/register

- *Description*: Registers a new user with the media-hub API.
- *Request Body*:
  - username (string): The username of the new user.
  - password (string): The password of the new user.
  - email (string): The email of the new user.
- *Response*:
  - Status: 201 Created
  - Body: JSON object containing user data, including username, password and email.

Example req.Body
{
	“Username”:”user123”,
	“Email”:user@hostname.com”,
	“Password”: “userpassword”
}

#### POST /api/auth/login

- *Description*: logs in an existing user with the media-hub API.
- *Request Body*:
  - email (string): The email of the user.
  - password (string): The password of the user.
- *Response*:
  - Status: 200 Ok
  - Body: JSON object containing user data, including password and email.

Example req.Body

{
	“email”:user@hostname.com”,
	“Password”: “userpassword”
}
Example response
{
	Token: “jwt”,
	User:
{	
	“id”: “userid”
		“Username”:”user123”,
		“Email”: “user@hostname.com”
}
}

## Endpoints after logging in

### Media management

#### POST /api/media
- *Description*: Allows users to add media to our website through api calls or custom.
- *Request Body*:
  - title (string): “name of the movie”.
  - type (string): “movie”.
  - platform (string): “netflix” [default custom].
  - added: timestamp. 
- *Response*:
  - Status: 201 Created

Example req.body 
{
  "title": "Movie Title",
  "type": "movie",
  "platform": "Netflix",
  "added": "2024-04-30T20:00:00Z"
}

#### GET /api/media
- *Description*: Allows users to view added media on our website
- *Response Body*:
  - title (string): “name of the movie”.
  - type (string): “movie”.
  - platform (string): “netflix” [default custom].
  - added: timestamp. 
  - Status: 200 Ok

Example response

[
  {
    "_id": "media_id",
    "title": "Movie Title",
    "type": "movie",
    "platform": "Netflix",
    "watched_at": "2024-04-30T20:00:00Z"
  },
  {
    "_id": "media_id",
    "title": "Music Track",
    "type": "music",
    "platform": "Spotify",
    "watched_at": "2024-05-01T12:00:00Z"
  }
]

#### DELETE /api/media/:mediaId
- *Description*: Allows users to delete added media on our website.
- *Response*:
  - Status: 200 Ok

### Playlist management

#### POST /api/playlists
- *Description*: Allows users to create different playlists on our website.
- *Request Body*:
  - name (string): “favourites1”.
  - description (string): “A collection of favorite movies and music”.
- *Response*:
  - Status: 201 Created

Example req.body

{
  "name": "My Favorites",
  "description": "A collection of favorite movies and music"
}

#### GET /api/playlists
- *Description*: Allows users to get playlists added on our website.
- *Response Body*:
  - name (string): “favorites”.
  - database (string): “A collection of favorite movies and music”.
  - created: timestamp. 
  - Status: 200 Ok

Example response

[
  {
    "_id": "playlist_id",
    "name": "My Favorites",
    "description": "A collection of favorite movies and music"
  }
]

#### PUT /api/playlists/:playlistId
- *Description*: Allows users to edit and update a playlist on our website.
- *Request Body*:
  - name (string): “favourites1”.
  - description (string): “A collection of favorite movies and music”.
  - added: timestamp.
  - modified: timestamp.
- *Response*:
  - Status: 200 Ok

#### DELETE /api/playlists/:playlistId
- *Description*: Allows users to delete playlists added on our website.
- *Response Body*:
  - Status: 200 Ok

## Dependencies

- express: Web framework for Node.js.
- cors: Middleware for enabling CORS (Cross-Origin Resource Sharing).
- dotenv: Loads environment variables from a .env file into process.env.
- colors: Library for colorizing console output.
- mongoose: MongoDB object modeling tool designed to work in an asynchronous environment.

## Configuration

- MongoDB connection URI and port are configured via environment variables for flexibility and security.
