[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/VuODydzp)

# Collaborators
## Jainam Modh (jmodh)
## Arav Jain (aravj)

# Task 1
## Steps for replication 
- Download github repo for dataset and code
- Create a schema in postgres with the name "fifa"
- Change username in db_properties
- Change password in db_properties

## Feature Descriptions
The fifa dataset imported into PostgreSQL contain the following features:
<details>
<summary>Key identifiers</summary>
    record_id (PRIMARY KEY),
    sofifa_id,
    year
</details>
<details>
<summary>2. Player personal data</summary>
    short_name, 
    long_name,
    player_positions,
    overall,
    potential,
    value_eur,
    wage_eur,
    age,
    dob,
    height_cm,
    weight_kg,
    gender
</details>
<details>
<summary>3. Club membership info</summary>
    club_team_id,
    club_name,
    league_name,
    league_level,
    club_position,
    club_jersey_number,
    club_loaned_from,
    club_joined,
    club_contract_valid_until
</details>
<details>
<summary>4. Nationality info</summary>
    nationality_id,
    nationality_name,
    nation_team_id,
    nation_position,
    nation_jersey_number
</details>
<details>
<summary>5. Player skill attributes</summary>
    preferred_foot,
    weak_foot,
    skill_moves,
    international_reputation,
    work_rate,
    body_type,
    real_face,
    release_clause_eur,
    player_tags,
    player_traits,
    pace,
    shooting,
    passing,
    dribbling,
    defending,
    physic,
    attacking_crossing,
    attacking_finishing,
    attacking_heading_accuracy,
    attacking_short_passing,
    attacking_volleys,
    skill_dribbling,
    skill_curve,
    skill_fk_accuracy,
    skill_long_accuracy,
    skill_ball_control,
    movement_acceleration,
    movement_sprint_speed,
    movement_agility,
    movement_reactions,
    movement_balance,
    power_shot_power,
    power_jumping,
    power_strength,
    power_long_shots,
    mentality_aggression,
    mentality_interceptions,
    mentality_vision,
    mentality_penalties,
    mentality_composure,
    defending_marking_awareness,
    defending_standing_tackle,
    defending_sliding_tackle,
    goalkeeping_diving,
    goalkeeping_handling,
    goalkeeping_positioning,
    goalkeeping_reflexes,
    goalkeeping_speed
</details> 
<details>
<summary>6. Player positions </summary>
    ls,
    st,
    rs,
    lw,
    lf,
    cf,
    rf,
    rw,
    lam,
    cam,
    ram,
    lm,
    lcm,
    cm,
    rcm,
    rm,
    lwb,
    ldm,
    cdm,
    rdm,
    rwb,
    lb,
    lcb,
    cb,
    rcb,
    rb,
    gk
</details>
<details>
<summary>7. Player URLs</summary>
    player_url,
    player_face_url,
    club_logo_url,
    club_flag_url,
    nation_logo_url,
    nation_flag_url
</details>

## PostgreSQL vs. NoSQL
PostgreSQL is a relational database that allows for faster storage, simpler data representation, and faster manipulation than the more complex data structures possible with a NoSQL database. A relational database is more useful for the fifa dataset as the data is already structured in the format of a row-column table in the given csv files. Additionally, a relational database representation is more useful for faster and more complex querying and analytics without worrying about how the data is stored for long-term use. Because we only need to use the database to store and retrieve data for a small analytics based project, it does not require the high scalability and performance optimization capabilities of a NoSQL database. 


# Task 2
## Steps for replication 
- Download github repo for dataset and code
- Create a schema in postgres with the name "fifa"
- Change username in db_properties
- Change password in db_properties
- For Task 2.1
    - input X, Y, Z
- For Task 2.2
    - input X, Y, highest (Boolean - True if Highest avg age False if Lowest avg age)

