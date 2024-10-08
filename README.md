[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/VuODydzp)

# Collaborators
## Jainam Modh (jmodh)
## Arav Jain (aravj)

# Task 1
## Feature Descriptions
The fifa dataset imported into PostgreSQL contain the following features:
1. record_id - primary key identifier of each row in the dataset
2. Player-specific data:
    - sofifa_id
    - player_url
    - short_name
    - long_name
    - player_positions
    - overall
    - potential
    - value_eur
    - wage_eur
    - age
    - dob
    - height_cm
    - weight_kg
3. Club membership data
    - club_team_id
## PostgreSQL vs. NoSQL
PostgreSQL is a relational database that allows for faster storage, simpler data representation, and faster manipulation than the more complex data structures possible with a NoSQL database. A relational database is more useful for the fifa dataset as the data is already structured in the format of a row-column table in the given csv files. Additionally, a relational database representation is more useful for faster and more complex querying and analytics without worrying about how the data is stored for long-term use. Because we only need to use the database to store and retrieve data for a small analytics based project, it does not require the high scalability and performance optimization capabilities of a NoSQL database. 
