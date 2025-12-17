# Roles and their permissions

---

## 🧑‍🦲 **Guest**

- ✅ Access the main page
- ❌ Access the ressource creation page
    - ❌ Create a ressource
- ❌ Access the reservation page
    - ❌ Create a reservation

- ✅ Access the login page
    - ✅ Can login
- ✅ Access the registration page
    - ✅ Create a reserver account
    - ✅ Create an administrator account
- ❌ Can logout


---

## 🧑‍💼 **Reserver**

- ✅ Access the main page
- ✅ Access the ressource creation page
    - ✅ Create a ressource
        - ✅ With a name and description
        - ✅ With the same name/description as another ressource
- ✅ Access the ressource modification page
  - ❌ Access through UI (must edit URL manually)
    - ✅ Modify a ressource
      - ✅ Modify name
      - ✅ Modify description
    - ❌ Delete a ressource

- ✅ Access the reservation page
    - ✅ Create a reservation
        - ✅ With a username, specified ressource, start and end date and time
        - ✅ If it overlaps with another reservation
        - ✅ If it overlaps with the reservation of another user
- ✅ Access the reservation modification page
  - ✅ If it is their reservation
    - ✅ Modify a reservation
      - ✅ Modify reserver
      - ✅ Modify reserved ressource
      - ✅ Modify start/end dates and times
    - ✅ Delete a reservation
  - ❌ If it is someone else's reservation

- ✅ Access the login page
  - ✅ By modifying the URL manually 
  - ❌ By using UI
  - ✅ Can login
- ✅ Access the registration page
  - ✅ By modifying the URL manually 
  - ❌ By using UI
- ✅ Can logout


---

## 🧑‍💼🛡️ **Administrator**

- ✅ Access the main page
- ✅ Access the ressource creation page
    - ✅ Create a ressource
        - ✅ With a name and description
        - ✅ With the same name/description as another ressource
- ✅ Access the ressource modification page
  - ✅ If a reservation using this ressource exists
    - ✅ Access through UI
    - ✅ Modify a ressource
    - ❌ Delete a ressource (NOTE: no error message was provided)
  - ✅ If there is no reservation using the ressource
    - ❌ Access through UI (must edit URL manually)
    - ✅ Modify a ressource
      - ✅ Modify name
      - ✅ Modify description
    - ✅ Delete a ressource
      - ❌ If the name input field, or the description input field is empty 
  - ✅ If the ressource does not exist
    - ❌ Access through UI (must edit URL manually)
    - ✅ Modify a ressource
      - ✅ Modify name
      - ✅ Modify description
    - ✅ Delete a ressource
      - ❌ If the name input field, or the description input field is empty (The "required" attribute prevents the deletion)

- ✅ Access the reservation page
    - ✅ Create a reservation
        - ✅ With a username, specified ressource, start and end date and time
        - ✅ If it overlaps with another reservation
        - ✅ If it overlaps with the reservation of another user
- ✅ Access the reservation modification page (NOTE: Accessing the reservation page of a non-existing reservation (i.e. deleted) causes an internal server error)
  - ✅ Modify a reservation
    - ✅ Modify reserver
    - ✅ Modify reserved ressource
    - ✅ Modify start/end dates and times
  - ✅ Delete a reservation

- ❌ Access the login page
- ❌ Access the registration page
- ✅ Can logout


---

# Table view

This is a condensed view of the permissions listed above.

| Permission | 🧑‍🦲 Guest | 🧑‍💼 Reserver | 🧑‍💼🛡️ Administrator |
| ----- |---- |---- |---- |
| Access the main page | ✅ | ✅ | ✅ |
| Access the ressource creation page | ❌ | ✅ | ✅ |
| Create a ressource | ❌ | ✅ | ✅ |
| Access the ressource modification page (NOTE: Reservers can only access that page by modifying the URL manually) | ❌ | ✅ | ✅ |
| Modify a ressource | ❌ | ✅ | ✅ |
| Delete a ressource (NOTE: The delete button is visible for the Reserver, but the button creates an error) | ❌ | ❌ | ✅ |
| Access the ressource modification page even if the ressource does not exist | ❌ | ✅ | ✅ |
| Access the reservation page | ❌ | ✅ | ✅ |
| Create a reservation | ❌ | ✅ | ✅ |
| Access the reservation modification page | ❌ | ✅ | ✅ |
| Modify a reservation | ❌ | ✅ | ✅ |
| Delete a reservation | ❌ | ❌ | ✅ |
| Access the login page (NOTE: Reservers and administrators can only access this page through URL)| ✅ | ✅ | ✅ |
| Access the registration page (NOTE: Reservers and administrators can only access this page through URL) | ✅ | ✅ | ✅ |
| Can logout (NOTE: Technically, Guests can access /logout by manually typing it in the URL, but it has no effect) | ❌ | ✅ | ✅ |


---

# Keypoints / Suggestions

These are our conclusions on the current state of user permissions. This list is not ordered.

- Administrators cannot delete a ressource if it is reserved, and cannot access the ressource modification page if the ressource is not reserved. This makes it impossible/very hard for a regular person to delete a ressource. To fix this, either add a way for administrators to see a list of all ressources, or allow deleting a ressource even if it is reserved, and automatically remove all reservations of this ressource.

- When an administrator visits the ressource modification page, emptying one of the input fields will prevent them from deleting the ressource. Remove the "required" attribute and replace them with JS verification. 

- Administrators and reservers can access ressource modification pages even if they do not exist. When this happens, the server should answer with an error saying that the ressource doesn't exist.

- Guests should not be able to create administrator accounts (Major security risk). Remove this option ASAP.

- Two ressources should not have the same name. This can lead to confusion for the users. Implement a server-side verification and display an error accordingly.

- Reservers are not able to access the ressource modification page through UI, yet they are authorized to modify a ressource. Either remove the ability of reservers to modify ressources, or add a link in UI depending on what you believe users should be able to do

- Reservations of a same ressource should not be allowed to overlap. Add a server-side verification to look for any over lap, and display an error accordingly.

- Reservers are able to access the reservation modification page for reservation they do not own by modifying the URL manually. Reservers can then modify the reservation and put themselves as the reserver. Basically stealing. 

(NOTE: Accessing the reservation page of a non-existing reservation (i.e. deleted) causes an internal server error)

## Extra
We found a little error when creating a reservation with a date before the year 25 (Year 25, not 2025). The error displays "User must be over 15 years old to make a reservation", which is not the correct error message.