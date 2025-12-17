
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

## Table view

This is a condensed view of the permissions listed above.

| Permission | 🧑‍🦲 Guest | 🧑‍💼 Reserver | 🧑‍💼🛡️ Administrator |
| --- | --- | --- | --- |
| Access the main page | ✅ | ✅ | ✅ |
| Access the ressource creation page | ❌ | ✅ | ✅ |
| Create a ressource | ❌ | ✅ | ✅ |
| Access the ressource modification page (NOTE: Reservers can only access that page by modifying the URL manually) | ❌ | ✅ | ✅ |
| Modify a ressource | ❌ | ✅ | ✅ |
| Delete a ressource (NOTE: no error message was provided) | ❌ | ❌ | ✅ |
| Access the ressource modification page even if the ressource does not exist | ❌ | ✅ | ✅ |
| Access the reservation page | ❌ | ❌ | ❌ |
| Create a reservation | ❌ | ❌ | ❌ |
| With a username, specified ressource, start and end date and time | ❌ | ❌ | ❌ |
| If it overlaps with another reservation | ❌ | ❌ | ❌ |
| If it overlaps with the reservation of another user | ❌ | ❌ | ❌ |
| Access the reservation modification page (NOTE: Accessing the reservation page of a non-existing reservation (i.e. deleted) causes an internal server error) | ❌ | ❌ | ❌ |
| Modify a reservation | ❌ | ❌ | ❌ |
| Modify reserver | ❌ | ❌ | ❌ |
| Modify reserved ressource | ❌ | ❌ | ❌ |
| Modify start/end dates and times | ❌ | ❌ | ❌ |
| Delete a reservation | ❌ | ❌ | ❌ |
| Access the login page | ❌ | ❌ | ❌ |
| Access the registration page | ❌ | ❌ | ❌ |
| Can logout | ❌ | ❌ | ❌ |


---

# Keypoints / Suggestions

These are my conclusions on the current state of user permissions. This list is not ordered.

- Administrators cannot delete a ressource if it is reserved, and cannot access the ressource modification page if the ressource is not reserved. This makes it impossible/very hard for a regular person to delete a ressource.
- When an administrator visits the ressource modification page, emptying one of the input fields will prevent them from deleting the ressource
- Administrators can access ressource modification pages even if they do not exist
- Guests should not be able to create administrator accounts
- Two ressources should not have the same name. This can lead to confusion for the users. 