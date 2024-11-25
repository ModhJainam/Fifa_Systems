# Collaborators
Jainam Modh (jmodh)
<br>
Arav Jain (aravj)

## Video Demos
- Local - https://cmu.box.com/s/cc0eqs5xg3aafstn7pqe0qafl6lxwpj6
- Cloud (Task 4) - [https://cmu.box.com/s/bt92jkeknbd46oya9qcwohkl4oi7jmbz](https://cmu.box.com/s/olwyan6o3z3rvemuvphmi3xgbd4n4r7y)

## Steps for replication 
### Setup
To run the entire code locally using fifa.ipynb (using m1pro Apple silicon "mps"):
- Download github repo for dataset and code
- Install pyspark and other required packages as listed in requirements.txt
- Create a schema in postgres with the name "fifa"
- Change username in db_properties
- Change password in db_properties

To run the entire code on the cloud using fifa_cloud.ipynb:
- Download github repo for dataset and code
- Create a Google Cloud Dataproc cluster with a master and >2 worker nodes
- Upload the fifa_cloud.ipynb file to the cluster
- Run the fifa_cloud.ipynb file on the Jupyter web interface

### Task Considerations
- For Task 2.1
    - Select inputs 
        - X: year from 2015-2022
        - Y: number of clubs
        - Z: year from 2023 onwards
- For Task 2.2
    - Select inputs 
        - X: number of clubs 
        - Y: year
        - highest: True for the highest average ages, False for the lowest average ages
- For Task 2.3 - run directly
- For Task 3
    - SparkML Linear Regression and Decision Tree Regression: Training + hyperparameter tuning with 5-fold cross validation will take ~10 minutes on a M1Pro macbook pro with 16 GB ram
    - PyTorch Multi Layer Perceptron: Training + hyperparameter tuning will take ~1.5 hours on a M1Pro macbook pro with 16 GB ram
    - Linear Regression: Training + hyperparameter tuning will take ~0.5 hours on a M1Pro macbook pro with 16 GB ram
    - For testing purposes: best to use the saved .pth models (there is a test_function(model_class) function which takes "MLP" or "LR" as input). This is for PyTorch models only.

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

## Model Training

Goal: Predict the overall value for each player based on their skillsets. 2 SparkML and 2 PyTorch regressors were trained by minimizing MSE loss and evaluated using the coefficient of determination ($R^2$ score). Hyperparameter-tuning was used to find the best hyperparameters for each model. 

### SparkML Models

The dataset was split into train and test sets with a 80:20 split. The following models were used:

1. Linear Regressor: Selected due to its simplicity and ability to handle linear relationships between the features and the target.
2. Decision Tree Regressor: Selected due to its ability to identify complex, non-linear relationships between the features and the target.

The following hyperparameters were tuned for each model using 5-fold cross validation:

1. Linear Regressor:
    - Regularization parameter: 0.01, 0.5, 2.0.
        - As regularization increases, the model becomes more generalized, leading to worse performance on this data when using cross validation.
    - Number of iterations: 1, 5, 10    
        - As the number of iterations increases, the model converges to a lower loss, leading to better performance.
2. Decision Tree Regressor:
    - Minimum information gain: 0.0, 0.1, 0.2
        - Higher values prevent overfitting by increasing the amount of information gain required to split the tree further, leading to better performance through generalization.
    - Minimum instances per leaf node: 1, 2
        - Higher values prevent overfitting by reducing the depth of the tree, leading to better performance through generalization.

### PyTorch Models

The dataset was split into train and test sets with a 80:20 split. The train set was split again into train and validation sets with a 80:20 split. Training was performed using batches and an Adam optimizer over 100 epochs. The following models were used: 

1. Linear Regressor: Selected due to its simplicity and ability to handle linear relationships between the features and the target.
2. Multi Layer Perceptron: Selected due to its ability to handle both linear and non-linear relationships between the features and the target.

The following hyperparameters were tuned for each model:

1. Linear Regressor:
    - Learning rate: 0.001, 0.01
        - As the learning rate increases, the model changes faster over the 100 epochs. This can lead to better or worse performance depending on how fast the model converges. 
    - Batch Size: 32, 64
        - As the batch size increases, the model converges in a more stable manner but can take longer to converge. This can lead to better or worse performance depending on the nature of the model training and loss curve. 
2. Multi Layer Perceptron:
    - Learning rate: 0.001, 0.01
        - As the learning rate increases, the model changes faster over the 100 epochs. This can lead to better or worse performance depending on how fast the model converges. 
    - Batch Size: 32, 64
        - As the batch size increases, the model converges in a more stable manner but can take longer to converge. This can lead to better or worse performance depending on the nature of the model training and loss curve. 
    - Hidden layer width: 32, 64
        - Increased width means that there are more neurons in the hidden layer of the MLP. This allows for the model to learn more complex relationships between the features and the target leading to a better fit on the training data.

## Model Performance Comparison

The following table compares the performance ($R^2$ scores) of the best 2 SparkML models and the 2 PyTorch models on the test dataset:

| Model | $R^2$ Score |
| --- | --- |
| SparkML Linear Regressor | 0.9353 |
| SparkML Decision Tree Regressor | 0.9287 |
| PyTorch Linear Regressor | 0.9350 |
| PyTorch MLP | 0.9884 |

As expected, the PyTorch Multi Layer Perceptron had the best performance with a $R^2$ score of 0.9884.
