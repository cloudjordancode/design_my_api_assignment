


### PET ADOPTION SERVICE

[MAPPED_API_DESIGN]

1. ## Resources:
   - Pets
   - Users
   - Applications

2. ## Relationships
   - A User can have many Applications (one-to-many)
   - Each application belongs to one User
   - A Pet can have many Applications (one-to-many)
   - Each Application belongs to one Pet
   - Users and Pets have a (many-to-many) relationship through Applications

3. ## Endpoints

   [Pets]
   - POST /pets — Add a new pet
   - GET /pets — List pets
   - GET /pets/{id} — Get a specific pet
   - PUT /pets/{id} — Update a pet
   - DELETE /pets/{id} — Remove a pet

   [Applications]
   - POST /applications — Submit an adoption application
   - GET /applications — List applications
   - GET /applications/{id} — Get a specific application

   [Users]
   - GET /users/{id} — Get a specific user

4. ## Schemas 

      [REQUEST]

         POST /pets   
         
         {
            "name": string (required),
            "species": string (required),
            "breed": string (required),
            "age": integer (required),
            "description": string (required),
            "adoption_fee": number (required),
            "status": string (required)
         }

      [RESPONSE]

         POST /pets
         {
            "id": integer,
            "name": string
            "species": string,
            "breed": string,
            "age": integer,
            "description": string,
            "adoption_fee": number,
            "status": string 
         }

      ---------------------------------------

      [REQUEST]

         POST /applications

         {
            "user_id": int (required),
            "pet_id": int (required),
            "message": string (required)

         }

      [RESPONSE]

         POST/applications
         {
            "application_id": integer,
            "user_id": integer,
            "pet_id": integer,
            "message": string, 
            "status": string 
         }

      ---------------------------------------

      [REQUEST]

         GET /pets/{id}

         Path Parameter:
         "id": integer (required)


      [RESPONSE]

         GET /pets/{id}

         {
            "id": integer,
            "name": string,
            "species": string,
            "breed": string,
            "age": integer,
            "description": string,
            "adoption_fee": number,
            "status": string
         }

      ---------------------------------------

      [REQUEST]

         GET /pets

         No request body required.


         [RESPONSE]

         GET /pets

         {
            "pets": [
               {
                     "id": integer,
                     "name": string,
                     "species": string,
                     "breed": string,
                     "age": integer,
                     "description": string,
                     "adoption_fee": number,
                     "status": string
               }
            ]
         }


5. ## AUTHENTICATION

      GET /pets
            Authentication: No
            Access: Public


      POST /applications
            Authentication: Yes
            Access: Logged-in users


      PUT /pets/{id}
            Authenticaiton: Yes
            Access: Staff 


      DELETE /pets/{id}
            Authentication: YES
            Access: Staff


      GET /applications/{id}
            Authentication: Yes
            Access: Application owner or Staff


6. ## Error Responses 

   POST /applications

      201 — Application created successfully

      400 — Bad Request
      Required application information is missing or invalid.

      401 — Unauthorized
      User is not logged in/authenticated.

      403 — Forbidden
      User is logged in but is not allowed to submit the application.

      404 — Not Found
      The pet being applied for does not exist.

      409 — Conflict
      The user has already applied for this pet, or the pet is no longer available.

      500 — Internal Server Error
      Something unexpected went wrong on the server.


   