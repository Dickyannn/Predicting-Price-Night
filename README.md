# Predicting Night Prices Using Random Forest and Neural Network

This project focuses on predicting nightly rental prices of property listings using two machine learning models: **Random Forest Regressor** and **Neural Network (MLP Regressor)**. The analysis is based on a structured dataset of 41,365 property records, containing information on room types, guest satisfaction, host status, location, and more.

---

## Dataset Overview

The dataset consists of **41,365 rows** and **18 columns**:

| Attribute | Description |
|-----------|-------------|
| `property_id` | Unique identifier for each property listing |
| `room_type` | Type of room being rented |
| `room_shared` | Whether the room is shared or not |
| `room_private` | Whether the room is private or not |
| `person_capacity` | Maximum capacity of guests |
| `host_is_superhost` | Host's status (superhost or not) |
| `cleanliness_rating` | Rating for property cleanliness |
| `multi` | Indicates multiple rooms in the listing |
| `biz` | Indicates if for business use |
| `guest_satisfaction_overall` | Guest satisfaction score (1–100) |
| `bedrooms` | Number of bedrooms |
| `dist` | Distance from city center |
| `metro_dist` | Distance from the nearest metro station |
| `city` | City where the property is located |
| `country` | Country where the property is located |
| `weekends` | Whether the price is for the weekend |
| `last_update` | Date of last update |
| `price_night` | Target: Nightly rental price in Euros |

---

## Data Cleaning & Preprocessing

- Missing values imputed (e.g., room_type, country via city).
- Dropped irrelevant columns: `property_id`, `last_update`, `room_shared`, `room_private`.
- Applied Box-Cox transformation to normalize:
  - `price_night`, `dist`, `metro_dist`
- Winsorization on outliers in:
  - `guest_satisfaction_overall` (<80)
  - `bedrooms` (0 or >7)
- Added engineered features:
  - `price_per_person` = price_night / person_capacity
  - `price_per_bedroom` = price_night / bedrooms

---

## Exploratory Data Analysis

- **Skewness** fixed using Box-Cox:
  - `price_night`: λ = -0.345
  - `dist`: λ = 0.248
  - `metro_dist`: λ = -0.057
- **Target variable** (`price_night`) was right-skewed.
- `room_type`, `city`, and `dist` found to be key features.

---

## Modeling & Results

### Random Forest Regressor
- **MAE**: 0.028
- **RMSE**: 0.039
- **R²**: 0.7999

### Neural Network (MLP Regressor)
- **MAE**: 0.0408
- **RMSE**: 0.0537
- **R²**: 0.6266

| Model | MAE | RMSE | R² Score |
|-------|-----|------|----------|
| Random Forest | 0.028 | 0.039 | 0.7999 |
| Neural Network | 0.0408 | 0.0537 | 0.6266 |

**Random Forest performed better across all metrics.**

---

## Feature Importance (Random Forest)

1. `room_type` — 18.9%
2. `city` — 18.3%
3. `dist` — 16.0%
4. `guest_satisfaction_overall` — 8.6%
5. `price_per_person` — 6.3%
6. `cleanliness_rating` — 5.4%
7. Others — lower than 5%

---

## Conclusion

This study confirms that **location**, **room type**, and **distance from city center** are key determinants of nightly rental prices. The Random Forest model proves more accurate and reliable compared to the neural network approach, making it more suitable for real-world pricing predictions.

---

