# Nham Ey — Database Schema

This document describes the **database structure** for the Nham Ey food discovery and promotion platform.  
It covers **users, restaurants, dishes, spins, clicks, and tags** to support all features in the app.

---

## **Tables Overview**

### 1. `users`
Stores Telegram Mini App user information.

| Column | Type | Description |
|--------|------|-------------|
| telegram_id | bigint (PK) | Unique Telegram user ID |
| first_name | varchar | User first name |
| last_name | varchar | User last name |
| username | varchar | Telegram handle |
| photo_url | varchar | Profile picture |
| created_at | timestamp | User registration date |
| preferences | json | Optional user preferences (e.g., cuisine filters) |

---

### 2. `restaurants`
Stores restaurant information linked to owners.

| Column | Type | Description |
|--------|------|-------------|
| id | integer (PK) | Unique restaurant ID |
| owner_id | bigint (FK → users.telegram_id) | Owner of the restaurant |
| name | varchar | Restaurant name |
| address | varchar | Restaurant address |
| google_maps_url | varchar | Link to Google Maps location |
| image_url | varchar | Restaurant image |
| discount_percentage | float | Optional discount for promotions |
| created_at | timestamp | Record creation time |
| updated_at | timestamp | Last update time |

---

### 3. `dishs`
Stores dishes linked to restaurants.

| Column | Type | Description |
|--------|------|-------------|
| id | integer (PK) | Unique dish ID |
| restaurant_id | integer (FK → restaurants.id) | Restaurant it belongs to |
| name | varchar | Dish name |
| cuisine | varchar | Type of cuisine |
| tags | json | List of tags (e.g., spicy, vegetarian) |
| image_url | varchar | Dish image |
| is_boosted | boolean | Paid boost flag |
| boost_expiry | timestamp | Boost end time |
| created_at | timestamp | Record creation time |
| updated_at | timestamp | Last update time |

---

### 4. `spins`
Tracks each time a user spins for a random dish.

| Column | Type | Description |
|--------|------|-------------|
| id | integer (PK) | Unique spin ID |
| user_id | bigint (FK → users.telegram_id) | User who spun |
| dish_id | integer (FK → dishs.id) | Dish shown/selected |
| timestamp | timestamp | When spin occurred |

---

### 5. `clicks`
Tracks user interactions like dish details, map clicks, or shares.

| Column | Type | Description |
|--------|------|-------------|
| id | integer (PK) | Unique click ID |
| user_id | bigint (FK → users.telegram_id) | User who clicked |
| dish_id | integer (FK → dishs.id) | Dish interacted with |
| clicked_at | timestamp | Timestamp of click |
| type | varchar | Click type (`dish_detail`, `google_map`, `share_button`) |

---

### 6. `tags`
Stores unique tags for dishes.

| Column | Type | Description |
|--------|------|-------------|
| id | integer (PK) | Tag ID |
| name | varchar | Tag name |

---

### 7. `dish_tags`
Many-to-many relationship between dishes and tags.

| Column | Type | Description |
|--------|------|-------------|
| dish_id | integer (FK → dishs.id) | Dish ID |
| tag_id | integer (FK → tags.id) | Tag ID |

---

## **Notes**
- `users` are authenticated via **Telegram Mini App**, no separate login needed.  
- `restaurants` belong to a user (owner), and each dish belongs to a restaurant.  
- `spins` and `clicks` tables provide **analytics for engagement and promotions**.  
- `tags` and `dish_tags` support **filtering dishes by type or characteristics**.  
- Boosted dishes are tracked directly in `dishs` with `is_boosted` and `boost_expiry`.

---

This schema supports all key **user-side and owner-side features**:
- Random dish discovery  
- Filtering by cuisine or tags  
- Map integration  
- Boosted promotions and analytics tracking  
- Telegram sharing and engagement tracking