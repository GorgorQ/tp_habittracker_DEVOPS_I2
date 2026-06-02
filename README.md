# Habit Tracker

Habit Tracker is a simple full-stack web application for tracking daily habits. Users can create routines, edit them, delete them, mark a habit as completed once per day, view the current streak, and see progress over the last seven days.

The project is intentionally clean and student-friendly: no authentication, no external UI library, clear Spring Boot layers, Angular standalone components, H2 sample data, and focused backend unit tests.

## Technologies Used

- Java 17
- Spring Boot 3
- Spring Web
- Spring Data JPA
- H2 in-memory database
- JUnit 5
- Mockito
- Angular 17
- RxJS
- Plain CSS

## Project Structure

```text
backend/
frontend/
README.md
```

## Run the Backend

```bash
cd backend
mvn spring-boot:run
```

The API runs at:

```text
http://localhost:8080
```

The H2 console is available at:

```text
http://localhost:8080/h2-console
```

Use this JDBC URL:

```text
jdbc:h2:mem:habittrackerdb
```

Sample habits and checks are inserted automatically at startup.

## Run the Frontend

```bash
cd frontend
npm install
npm start
```

The Angular app runs at:

```text
http://localhost:4200
```

Make sure the backend is running on port `8080` before using the frontend.

## Run Backend Tests

```bash
cd backend
mvn test
```

The tests cover:

- creating a habit
- updating a habit
- deleting a habit
- checking a habit for today
- preventing duplicate checks on the same day
- calculating a streak
- calculating progression over the last 7 days

## Business Rules

- A habit can be checked only once per day.
- A habit check must be linked to an existing habit.
- The current streak counts completed consecutive days starting from today.
- Progression is the percentage of completed days over the last seven days, including today.

## API Endpoints

### Habits

| Method | Endpoint | Description |
| --- | --- | --- |
| GET | `/api/habits` | Get all habits |
| GET | `/api/habits/{id}` | Get one habit by id |
| POST | `/api/habits` | Create a habit |
| PUT | `/api/habits/{id}` | Update a habit |
| DELETE | `/api/habits/{id}` | Delete a habit and its checks |

Example habit body:

```json
{
  "name": "Read 20 pages",
  "description": "Read every evening.",
  "category": "Learning",
  "targetFrequency": "Daily"
}
```

### Habit Checks

| Method | Endpoint | Description |
| --- | --- | --- |
| POST | `/api/habits/{id}/check` | Mark a habit as completed for today |
| DELETE | `/api/habits/{id}/check/{date}` | Remove a check for a date, using `yyyy-MM-dd` |
| GET | `/api/habits/{id}/checks` | Get all checks for a habit |
| GET | `/api/habits/{id}/streak` | Get the current streak |
| GET | `/api/habits/{id}/stats` | Get streak, completed days, and progression |

Optional check body:

```json
{
  "checkDate": "2026-06-02",
  "completed": true
}
```

Stats response:

```json
{
  "habitId": 1,
  "habitName": "Read 20 pages",
  "currentStreak": 3,
  "completedDaysLast7": 4,
  "progressionPercentage": 57.1
}
```
# tp_habittracker_DEVOPS_I2
