# Nham Ey

## Project Overview
**Nham Ey** (“What to Eat?”) is a food discovery and promotion platform for Phnom Penh.  
Users can spin a to randomly discover local dishes, while restaurant owners upload and promote their dishes directly.  
Fully integrated with **Telegram Mini App** — no app download required, instant and shareable experience.

---

## Problem We Solve
- Meal time indecision among people in phnom penh.  
- Small vendors struggle to reach new customers efficiently.  

---

## Features

**User Side:**
- Spin to discover nearby dishes.  
- Filter by cuisine type, tags, or location.  
- Dynamic links to dish/vendor on Google Maps.  
- Share results in Telegram chats with friends.

**Owner Side:**
- Upload and manage dishes and promotions.  
- Boost dishes to increase visibility in roulette (paid).  
- Track analytics: spins, clicks, conversions.

---

## Revenue Stream
- Paid dish promotion (boost visibility in roulette).  
- Optional future revenue:  
  - Featured listings  
  - Sponsored campaigns or events.

---

## Cost Structure
- Hosting and backend infrastructure (DigitalOcean).  
- Database (PostgreSQL).  
- Media storage (Cloudinary).  

---

## Technology Stack

**Frontend:**  
- React + TypeScript  
- TailwindCSS  
- Telegram Mini App integration

**Backend:**  
- Django + Django REST Framework  
- PostgreSQL database  
- Uvicorn (ASGI server for async endpoints)

**Dev & Deployment:**  
- Docker + docker-compose  
- Poetry (Python dependency management)  
- Cloudinary (image hosting)