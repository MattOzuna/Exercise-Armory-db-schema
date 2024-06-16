# Workout App Database Schema

This document outlines the database schema for the Exercise Armory App, which includes tables for exercises, users, workouts, and the relationship between workouts and exercises. The schema is designed to facilitate the organization and management of workout data for users of the app.

## Tables

### 1. Exercises
This table stores information about various exercises.

| Column              | Type      | Constraints                |
|---------------------|-----------|----------------------------|
| id                  | int       | Primary Key, Auto Increment|
| body_part           | text      | Not Null                   |
| equipment           | text      | Not Null                   |
| gif_url             | text      | Not Null                   |
| name                | text      | Not Null                   |
| target              | text      | Not Null                   |
| secondary_muscles   | text[]    |                            |
| instructions        | text[]    | Not Null                   |

### 2. Users
This table stores user information.

| Column     | Type        | Constraints                                |
|------------|-------------|--------------------------------------------|
| username   | varchar(25) | Primary Key                                |
| password   | text        | Not Null                                   |
| first_name | text        | Not Null                                   |
| last_name  | text        | Not Null                                   |
| email      | text        | Not Null, CHECK (position('@' IN email) > 1)|
| is_admin   | boolean     | Not Null, Default: FALSE                   |
| created_at | timestamp   | Default: CURRENT_TIMESTAMP                 |
| updated_at | timestamp   | Default: CURRENT_TIMESTAMP                 |

### 3. Workouts
This table stores information about user workouts.

| Column     | Type        | Constraints                      |
|------------|-------------|----------------------------------|
| id         | int         | Primary Key, Auto Increment      |
| user_id    | varchar(25) | Foreign Key References users(username) ON DELETE CASCADE |
| date       | date        | Not Null                         |
| exercises  | int[]       | Not Null                         |
| notes      | text        |                                  |

### 4. Workouts_Exercises
This table links workouts to exercises with details about sets, reps, and weight.

| Column      | Type   | Constraints                                    |
|-------------|--------|------------------------------------------------|
| workout_id  | int    | Foreign Key References workouts(id) ON DELETE CASCADE |
| exercise_id | int    | Foreign Key References exercises(id) ON DELETE CASCADE |
| sets        | int    | Not Null                                       |
| reps        | int    | Not Null                                       |
| weight      | int    |                                                |

## Relationships

- A user can have multiple workouts.
- A workout belongs to one user.
- A workout can include multiple exercises.
- An exercise can be part of multiple workouts.

