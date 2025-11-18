Original App Design Project - README
===

# Bloom

## Table of Contents

1. [Overview](#Overview)
2. [Product Spec](#Product-Spec)
3. [Wireframes](#Wireframes)
4. [Schema](#Schema)

## Overview

### Description

a personalized self-care tracker designed to help users stay consistent with habits that support physical, mental, and academic wellness. Users log daily activities like hydration, sleep, mindfulness, journaling, or workouts and see their growth through streaks, icons, and visual dashboards. It aims to make self-care feel motivating and aesthetic, turning everyday habits into a rewarding “personal glow-up journey.” The app may also include an AI-powered reflection feature where users describe their recent habits and goals and receive personalized suggestions.

### App Evaluation
- **Category:** Health and Wellness
- **Mobile:** Mobile enhances the experience through push notifications for daily habits, quick logging from anywhere. The mobile format also supports short daily check-ins and streak tracking, making it more than a website—it is a guided, on-the-go self-care companion.
- **Story:**  Focuses on empowering users to maintain balanced wellness in their busy lives. It transforms routines into visual “growth,” making self-improvement feel satisfying and personal. Students and young adults would connect deeply with the idea because many struggle to stay consistent with self-care, and this will bring structure and motivation to that process.
- **Market:** The wellness app market is huge and steadily expanding. Bloom will provide meaningful value to a wide group students, working adults, and anyone building a healthier routine. It also appeals to a niche: people who enjoy aesthetic, habit-focused lifestyle apps. Because self-care is universal.
- **Habit:** This app is designed to be opened daily, sometimes multiple times. Users create content by logging activities, writing reflections, and tracking their streaks. Visual progress keeps the app engaging, and AI-generated suggestions encourage users to return to monitor and improve their routines.
- **Scope:** V1 can include 3–5 daily habits, a minimal dashboard, mood logging, and simple visuals—very achievable within the course timeline. V2 could add AI habit recommendations, editable habits, and enhanced graphics. V3 could incorporate rewards, more customization, or long-term insights. Even a stripped-down prototype communicates the full vision effectively.

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**

* User can register for an account
* User can log in / log out
* User can select 3-5 daily self-care habits
* User can track dailt habit completion
* User can add optional notes to dailt entries
* User can viw a Progress dashboard showing streaks, completion %, and trends
* User can recieve AI-generated habit suggestions based on goals
* User can view historical logs for past days/weeks
* User can edit, add, or delte habits
* User can manage basic profile settings

**Optional Nice-to-have Stories**

* Push notifications for reminders
* Gamified rewards or badges

### 2. Screen Archetypes

- [ ] [**Register Screen**]
* User can create an account with email, password, display/username
- [ ] [**Login Screen**]
* User can log into their existing account
- [ ] [**Habit selection Screen**]
* User selects 3-5 habits to track
* User can add custom habits
- [ ] [**Home/Daily Tracker Screen**]
* User can mark habits as completed
* User can enter notes
- [ ] [**Progress Dashboard**]
* User views streaks, completion %, and weekly/monthly trends
- [ ] [**Ai Suggestions Screen**]
* User enters goals
* App returns personalized tips via LLM
- [ ] [**Profile/Settings Screen**]
* User updates profile and preferences
* Toggle reminders, theme, privacy options


### 3. Navigation

**Tab Navigation** (Tab to Screen)
- [ ] Home / Daily Tracker
- [ ] Dashboard
- [ ] Ai Suggestions
- [ ] Profile

**Flow Navigation** (Screen to Screen)

- [ ] [**Register Screen**]
  * Leads to [**Login Screen -> Habit Selection**]
- [ ] [**Home Screen**]
  * Leads to [**Habit Detail -> Dashboard**] 
- [ ] [**Dashboard**]
  * Leads to [**History View**]
- [ ] [**Profile**]
  * Leads to [**Edit profile / Reminders**]
- [ ] [**Ai Suggestions**]
  * Leads to [**Optional notes save**]


## Wireframes

![wireframe](https://github.com/user-attachments/assets/b4705784-f200-409b-99e0-e79dcf192486)

### Digital Wireframes & Mockups
<img width="206" height="458" alt="image" src="https://github.com/user-attachments/assets/e7218cd3-ab8f-4e14-8b81-daf9b1107093" />
<img width="206" height="450" alt="image" src="https://github.com/user-attachments/assets/3b14c2ca-2dbb-4bea-b78c-b7c624ad9e5f" />
<img width="204" height="454" alt="image" src="https://github.com/user-attachments/assets/44138761-f935-48a3-857d-d81189819752" />
<img width="207" height="450" alt="image" src="https://github.com/user-attachments/assets/0bca5e8e-0ffb-4ca8-ba30-fb4f3bb84cd5" />


## Schema 


### Models

[User]
| Property | Type   | Description                                  |
|----------|--------|----------------------------------------------|
| username/id | String | unique identifier |
| email | String | Login email   |
| DisplayName      | String    | Visible name |
| PreferredHabits | Array | User-selected habits |
| Goals | String | Stored goals for Ai suggestions |
| CreatedAt | Date | Creation timestamp |

[Habit]
| Property | Type   | Description                                  |
|----------|--------|----------------------------------------------|
| id | String | Habit ID |
| userid | String | Owner of habit   |
| name      | String    | Habit name |
| targetType | String | ex. "minutes", "hours" |
| archived | Boolean | Whether habit is archived |
| CreatedAt | Date |  timestamp |

[HabitEntry]
| Property | Type   | Description                                  |
|----------|--------|----------------------------------------------|
| id | String | Entry ID |
| habitid | String | Linked habit   |
| date     | String    | "YYYY-MM-DD" |
| value | String | Numeric completion value |
| note | String | Optional notes |
| CreatedAt | Date |  timestamp |

[SreakSummary]
| Property | Type   | Description                                  |
|----------|--------|----------------------------------------------|
| currentStreak| Int | Ongoing streak |
| longestStreak | Int | Record streak   |
| completionRate      | Float    | Percentage completed |
| weeklyTrend | Map | Trend counts by day |

    
### Networking
**Auth**
- `[POST] /register` - create acount
- `[POST] /login` - authenticate user
- `[POST] /logout` - end session

Habits
- `[GET] /habits` - fetch user's habits
- `[POST] /habits` - create new habit
- `[PUT] /habits/{id}` - edit habit
- `[DELETE] /habits/{id}` - delete habit

Entries
- `[POST] /entries` - add daily habit entry
- `[GET] /entries?date=` - fetch entries for a day
- `[GET] /entries/history` - view past logs

Dashboard / Analytics
- `[GET] /analytics/streaks` - compute streaks
- `[GET] /analytics/completion` - get completion %
- `[GET] /analytics/trends` - weekly/monthly chart data

Ai Suggestions
- `[POST] /ai/suggestions`
- `Body: {goals, recentEntries}`
- `Return: [tips]` from LLM

