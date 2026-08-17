# 🏠 Property Dealer App — Android

A complete Android application for property dealers to manage property listings, track seller & buyer details, calculate distances, and share property information with masked seller details.

---

## ✨ Features

### 📋 Property Management
- Add / Edit / Delete properties with full details
- Property types: Residential, Commercial, Plot, Office, Shop, Industrial, etc.
- Track **status**: Available, Sold, Pending, Under Negotiation
- Area with units (sq.ft, sq.m, Bigha, Acre, etc.)
- Floor, facing direction, furnished status, parking

### 💰 White & Black Price Tracking
- Total price, White (official) amount, Black (unofficial) amount
- Each buyer's offer also tracks White + Black split

### 👤 Seller Details (Confidential)
- Seller name, primary & alternate mobile, email
- Stored securely in local database
- Phone number **automatically masked** when sharing with buyers  
  e.g. `98765XXXXX` (first 5 digits shown only)

### 🧑‍💼 Buyer Tracking
- Multiple interested buyers per property
- Each buyer: name, phone, email, offered price (with W/B split), status, notes
- Status: Interested → Negotiating → Accepted / Rejected
- Direct call button per buyer
- Highest offer shown prominently

### 📏 Distance Calculator
- Enter GPS coordinates or use current phone GPS location
- Calculates distance using **Haversine formula** (no API key needed)
- Shows result in km or meters
- One-tap Google Maps directions
- Share distance + property map link

### 📤 Smart Sharing
- **Share to Buyer** — Seller phone masked, formatted WhatsApp-ready message
- **Full Dealer Report** — Complete unmasked details + all buyer info
- Share distance from any location to the property

### 🔍 Search & Filter
- Search by property name, address, seller name
- Filter by status (Available / Sold / Pending / Under Negotiation)
- Filter by property type
- Dashboard stats: Total / Available / Sold counts

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|------------|
| Language | Kotlin |
| Architecture | MVVM + Repository |
| Database | Room (SQLite) |
| UI | Material Design 3 |
| Async | Coroutines + LiveData |
| Navigation | Intent-based |
| Distance | Haversine formula (no Maps API needed) |
| Location | FusedLocationProviderClient |

---

## 📁 Project Structure

```
app/src/main/
├── java/com/propertydealer/app/
│   ├── data/
│   │   ├── model/
│   │   │   ├── Property.kt       ← Property entity with all fields
│   │   │   └── Buyer.kt          ← Buyer entity linked to Property
│   │   └── db/
│   │       ├── AppDatabase.kt    ← Room database
│   │       ├── PropertyDao.kt    ← Property queries
│   │       ├── BuyerDao.kt       ← Buyer queries
│   │       └── PropertyRepository.kt
│   ├── ui/
│   │   ├── property/
│   │   │   ├── SplashActivity.kt
│   │   │   ├── MainActivity.kt           ← Home with list, search, filter
│   │   │   ├── AddEditPropertyActivity.kt ← Full property form
│   │   │   ├── PropertyDetailActivity.kt  ← Detail + buyers + share
│   │   │   ├── DistanceCalculatorActivity.kt
│   │   │   └── PropertyViewModel.kt
│   │   ├── buyer/
│   │   │   └── AddBuyerActivity.kt
│   │   └── adapters/
│   │       ├── PropertyAdapter.kt
│   │       └── BuyerAdapter.kt
│   └── utils/
│       ├── DistanceCalculator.kt  ← Haversine formula + map URLs
│       ├── FormatUtils.kt         ← Currency, phone masking, dates
│       └── ShareUtils.kt          ← Generate share text (buyer/dealer)
└── res/
    ├── layout/   ← 6 layout XML files
    ├── values/   ← colors, strings, themes
    ├── drawable/ ← vector icons
    ├── menu/     ← action bar menus
    └── xml/      ← backup rules
```

---

## 🚀 How to Build

### Prerequisites
- Android Studio Giraffe or newer
- JDK 17
- Android SDK 34
- Minimum device: Android 7.0 (API 24)

### Steps

1. **Open in Android Studio**
   ```
   File → Open → Select the PropertyDealerApp folder
   ```

2. **Sync Gradle**
   - Click "Sync Now" when prompted, or
   - Build → Sync Project with Gradle Files

3. **Add Google Play Services** (for GPS location)
   - Already included via `com.google.android.gms:play-services-location`
   - No Google Maps API key required (uses Haversine formula for distance)

4. **Run the app**
   - Connect an Android device or start an emulator
   - Click Run ▶️

---

## 📱 How to Use

### Add a Property
1. Tap **"Add Property"** FAB button
2. Fill in: Name, Address, GPS coordinates (optional — tap "Use Current GPS" to auto-fill)
3. Enter: Total Price, White Price, Black Price
4. Fill property details: type, area, floor, facing, parking, furnished
5. Enter **Seller details** (kept private — never shared without masking)
6. Set status (Available / Sold / etc.)
7. Add description & private notes
8. Tap **"SAVE PROPERTY"**

### Track Buyers
1. Open any property
2. Tap **"Add Buyer"** button
3. Enter buyer's name, phone, offered price
4. Set status: Interested → Negotiating → Accepted / Rejected

### Calculate Distance
1. Open a property → Tap **"📏 Distance"**
2. Option A: Tap "Use My Current GPS Location"
3. Option B: Enter coordinates manually (e.g. `26.8505, 75.8069`)
4. Tap "Calculate Distance" → see result in km/meters
5. Tap "🗺️ Directions" to open Google Maps turn-by-turn navigation
6. Tap "📤 Share" to share distance info with anyone

### Share with Buyer (Masked)
1. Open a property → Menu (⋮) → **"Share to Buyer"**
2. Seller phone is automatically masked: `98765XXXXX`
3. All property details, price, and map link are included

### Share Full Report (Dealer)
1. Open a property → Menu (⋮) → **"Full Report"**
2. All details including unmasked seller info + all buyer details

---

## 🔒 Privacy Design

| Data | Buyer Share | Dealer Report |
|------|-------------|---------------|
| Property name | ✅ Full | ✅ Full |
| Address | ✅ Full | ✅ Full |
| Price | ✅ Full | ✅ Full |
| Seller name | ✅ Full | ✅ Full |
| Seller phone | ⚠️ Masked (98765XXXXX) | ✅ Full |
| Seller email | ❌ Hidden | ✅ Full |
| Buyers list | ❌ Hidden | ✅ Full |
| Private notes | ❌ Hidden | ✅ Full |

---

## 💡 Tips

- **GPS Coordinates for Jaipur**: You can find coordinates by opening Google Maps, long-press a location, and copy the lat/lon shown. Example: Akshaya Patra, Jagatpura ≈ `26.7752, 75.8461`
- **WhatsApp Ready**: The share text is formatted with bold/emojis for clean display in WhatsApp
- **Offline First**: All data is stored locally on the device. No internet required (except for opening Google Maps links)

---

## 📦 Dependencies

```gradle
// Material Design 3
com.google.android.material:material:1.11.0

// Room Database
androidx.room:room-runtime:2.6.1
androidx.room:room-ktx:2.6.1

// ViewModel + LiveData
androidx.lifecycle:lifecycle-viewmodel-ktx:2.7.0
androidx.lifecycle:lifecycle-livedata-ktx:2.7.0

// Location
com.google.android.gms:play-services-location:21.0.1

// Kotlin Coroutines
org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.3
```

---

*Built with ❤️ for property dealers. All seller data is stored securely on-device and never uploaded anywhere.*
