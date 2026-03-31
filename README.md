# 🏨 Hotel Room Reservation System

A smart, single-page hotel room reservation system built with pure HTML, CSS, and JavaScript. Dynamically allocates rooms based on optimal travel time calculations across 10 floors and 97 rooms.

---

## 🚀 Live Demo

👉 **[View Live App](https://prismatic-dodol-c066ec.netlify.app/)**

---

## 📋 Problem Statement

A hotel has **97 rooms** across **10 floors**:

| Floor  | Rooms | Room Numbers |
|------- |-------|--------------|
| Floor1 | 10    | 101 – 110    |
| Floor2 | 10    | 201 – 210    |
| ...    | ..    |...           |
| Floor9 | 10    | 901–910      |
| Floor10| 7     |  1001 – 1007 |

**Building Layout:**
- Staircase/lift is on the **left side** of the building
- Rooms are arranged **left to right**, with Room X01 closest to the lift

**Travel Time Rules:**
- Horizontal (same floor): **1 minute** per room
- Vertical (between floors): **2 minutes** per floor

**Booking Rules:**
- A guest can book **1 to 5 rooms** at a time
- **Priority 1:** Book rooms on the **same floor** first
- **Priority 2:** If not possible, book rooms that **minimize total travel time** across floors

---

## ⚙️ Algorithm

### Travel Time Formula
```
travelTime(A, B) = |A.position - B.position| + |A.floor - B.floor| × 2
```
Total travel time = distance between the **first and last room** in the booking (sorted by floor → position).

### Booking Logic

```
1. Group all available rooms by floor
2. Check if any single floor has enough available rooms
   → YES: Use sliding window to find tightest group (min travel time)
   → NO:  Generate all combinations across floors, pick min travel time combo
3. Mark selected rooms as booked
4. Display result with travel time
```

**Why this works:**
- Same-floor priority is always checked first ✅
- Multi-floor fallback is exhaustive but efficient (max 5 rooms = small search space) ✅
- Handles all edge cases: partial floors, floor 10's 7-room limit, sparse availability ✅

---

## ✨ Features

- 🏷️ **Room Input** — Enter 1–5 rooms and click Book (or press Enter)
- 🎨 **Visual Grid** — Color-coded hotel map with all 10 floors
  - ⬜ Gray = Available
  - 🟦 Blue = Occupied
  - 🟩 Green = Just Booked ✓
- 🎲 **Randomize Button** — Generate random occupancy (~40% filled)
- ↺ **Reset Button** — Clear all bookings instantly
- 📊 **Booking Summary** — Shows booked rooms, floors, type (single/multi), travel time
- 📈 **Live Stats** — Total / Available / Occupied / Occupancy %
- 🏗️ **Lift Visualization** — Lift column on left of each floor

---

## 🛠️ Tech Stack

| Technology | Usage |
|------------|-------|
| HTML5 | Structure |
| CSS3 | Styling, animations, layout |
| Vanilla JavaScript | Booking algorithm, state management |
| Google Fonts (Syne + DM Mono) | Typography |

> Zero dependencies. Zero frameworks. Single file. 

---

## 📁 Project Structure

```
hotel-room-reservation/
│
└── index.html        ← Everything lives here (HTML + CSS + JS)
```

---

## 🖥️ Run Locally

No build step needed. Just open the file:

```bash
# Clone the repo
git clone https://github.com/shaikasadahmed2k23/hotel-room-reservation.git

# Open in browser
cd hotel-room-reservation
open index.html
```

Or just double-click `index.html` — it works instantly in any browser.

---

## 📸 Screenshots

> Hotel grid showing available, occupied, and just-booked rooms with live stats.

- ![Fresh and Empty Grid](screenshots/01__Fresh%20and%20Empty%20Grid%20(All%20rooms%20available).png)
- ![4 rooms booked](screenshots/02__4%20rooms%20booked%20(Green%20colour%20booked,%20Without%20Randomizing).png)
- ![Randomized Grid](screenshots/03__Randomized%20Grid.png)
- ![5 rooms booked](screenshots/04__5%20rooms%20booked%20in%20Randomized%20Grid.png)
---

## 📌 Example Scenario

**Available rooms:**
- Floor 1: 101, 102, 105, 106
- Floor 2: 201, 202, 203, 210

**Guest books 4 rooms:**
→ System picks **101, 102, 105, 106** (all Floor 1, travel time = 5 min)

**If only 101, 102 available on Floor 1:**
→ System picks **201, 202** from Floor 2 (travel time = 1 min, minimized)

---

## 👨‍💻 Author

Built as part of the **SDE 3 Assessment — Unstop**

---

## 📄 License

This project is for assessment purposes only.
