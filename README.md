# Football Ticket Booking Database

## Links

✅ ERD Link (Public):  
https://drive.google.com/file/d/1yInpegCHkRDEaqnnGQfhX6NDgxyh-vPW/view?usp=sharing

✅ GitHub Repository Link (Public):  
https://github.com/Iam-Zarif/football-ticket-booking

✅ Interview Video Link (Public):  
https://drive.google.com/file/d/1uSG4_Mdyd2v5Z8Fn0KFWdtOuHv9rSflW/view?usp=sharing

---

## Database Design Approach

### Users Table
- Created `user_id` as Primary Key.
- Applied `UNIQUE` constraint on `email`.
- Used `CHECK` constraint to allow only:
  - Football Fan
  - Ticket Manager

### Matches Table
- Created `match_id` as Primary Key.
- Applied `CHECK` constraint to prevent negative ticket prices.
- Restricted `match_status` to:
  - Available
  - Selling Fast
  - Sold Out
  - Postponed

### Bookings Table
- Created `booking_id` as Primary Key.
- Added Foreign Key relationships:
  - `user_id` → Users
  - `match_id` → Matches
- Applied `CHECK` constraint for non-negative booking cost.
- Restricted `payment_status` values:
  - Pending
  - Confirmed
  - Cancelled
  - Refunded

---

## Query Approach

### Query 1
Retrieved all available matches from the Champions League category.

### Query 2
Used:
- `LIKE` for names starting with "Tanvir"
- `ILIKE` for case-insensitive search containing "Haque"

### Query 3
Used `COALESCE()` to replace NULL payment status with `Action Required`.

**Note:** The requirement mentions retrieving all booking records with missing payment status. Based on the provided sample output, only `booking_id`, `user_id`, `match_id`, and `payment_status` were selected.

### Query 4
Used `INNER JOIN` between:
- Bookings
- Users
- Matches

To retrieve:
- Booking ID
- User Name
- Match Fixture
- Total Cost

### Query 5
Used `LEFT JOIN` from Users to Bookings to ensure users without bookings are also included.

### Query 6
Used a subquery with `AVG(total_cost)` to find bookings whose total cost is higher than the average booking cost.

### Query 7
Used:
- `ORDER BY base_ticket_price DESC`
- `OFFSET 1`
- `LIMIT 2`

To retrieve the next two most expensive matches after skipping the highest-priced match.
