# Technical Documentation: Voucher Claim Application

## Overview
Aplikasi berbasis web untuk sistem klaim voucher melalui verifikasi aktivitas social media dengan fitur gamifikasi. Aplikasi terdiri dari 3 halaman utama: homepage produk, form klaim voucher, dan wheel of fortune untuk pemberian reward.

## Tech Stack
- Frontend: Vue.js
- Backend: Golang
- Database: PostgreSQL

## System Architecture

### Database Schema

#### Products Table
```sql
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    price DECIMAL(10,2) NOT NULL,
    discount_price DECIMAL(10,2),
    rating DECIMAL(3,2),
    image_url VARCHAR(255),
    stock INT NOT NULL DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Voucher Claims Table
```sql
CREATE TABLE voucher_claims (
    id SERIAL PRIMARY KEY,
    social_media_type VARCHAR(20) NOT NULL,
    username VARCHAR(255) NOT NULL,
    whatsapp VARCHAR(20) NOT NULL,
    email VARCHAR(255) NOT NULL,
    has_liked BOOLEAN DEFAULT false,
    has_commented BOOLEAN DEFAULT false,
    has_shared BOOLEAN DEFAULT false,
    is_verified BOOLEAN DEFAULT false,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Voucher Rewards Table
```sql
CREATE TABLE voucher_rewards (
    id SERIAL PRIMARY KEY,
    claim_id INT REFERENCES voucher_claims(id),
    discount_percentage INT NOT NULL,
    code VARCHAR(20) UNIQUE NOT NULL,
    is_used BOOLEAN DEFAULT false,
    valid_until TIMESTAMP NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Frontend Architecture

#### Project Structure
```
src/
├── assets/
├── components/
│   ├── common/
│   │   ├── BaseButton.vue
│   │   ├── BaseInput.vue
│   │   └── BaseSelect.vue
│   ├── home/
│   │   ├── ProductCard.vue
│   │   ├── ProductGrid.vue
│   │   └── HeroSection.vue
│   ├── voucher/
│   │   ├── ClaimForm.vue
│   │   └── SocialVerification.vue
│   └── wheel/
│       ├── WheelCanvas.vue
│       └── PrizeDisplay.vue
├── layouts/
├── pages/
├── services/
├── store/
└── router/
```

#### Key Pages
1. **HomePage.vue**
   - Display produk best seller
   - Rating dan harga produk
   - Navigasi ke form klaim voucher

2. **ClaimVoucherPage.vue**
   - Form input data user
   - Checklist verifikasi social media
   - Integrasi API verifikasi

3. **WheelOfFortunePage.vue**
   - Wheel of fortune animation
   - Display hasil voucher
   - Record data pemenang

### Backend Architecture

#### Project Structure
```
cmd/
├── main.go
└── server/
    └── server.go
internal/
├── config/
├── handlers/
├── middleware/
├── models/
├── repository/
└── services/
```

#### API Endpoints

##### Products
```
GET    /api/products           - Get all products
GET    /api/products/:id       - Get product detail
```

##### Voucher Claims
```
POST   /api/claims/verify      - Verify social media actions
POST   /api/claims/submit      - Submit claim form
GET    /api/claims/history     - Get claim history by email/wa
```

##### Social Media Verification
```
POST   /api/social/verify      - Verify social media engagement
GET    /api/social/status/:id  - Check verification status
```

##### Wheel of Fortune
```
POST   /api/wheel/spin         - Generate wheel result
GET    /api/wheel/voucher/:id  - Get voucher details
```

### Data Models

#### Social Verification
```golang
type SocialVerification struct {
    Platform    string `json:"platform"`    // instagram/tiktok
    Username    string `json:"username"`
    ActionType  string `json:"actionType"`  // like/comment/share
    PostID      string `json:"postId"`
    Status      string `json:"status"`
}
```

#### Claim Request
```golang
type ClaimRequest struct {
    SocialMediaType string `json:"socialMediaType"`
    Username        string `json:"username"`
    Whatsapp        string `json:"whatsapp"`
    Email           string `json:"email"`
    HasLiked        bool   `json:"hasLiked"`
    HasCommented    bool   `json:"hasCommented"`
    HasShared       bool   `json:"hasShared"`
}
```

#### Wheel Configuration
```golang
type WheelConfig struct {
    Prizes []Prize `json:"prizes"`
}

type Prize struct {
    DiscountPercentage int     `json:"discountPercentage"`
    Probability        float64 `json:"probability"`
    Color             string  `json:"color"`
}
```

## Development Guidelines

### Database
- Gunakan indexes untuk optimasi query
- Implement audit trails dengan timestamps
- Maintain referential integrity

### Frontend
- Implement component reusability
- Use Vuex untuk state management
- Implement proper form validation
- Handle loading states dan errors
- Optimize wheel animation performance

### Backend
- Follow clean architecture principles
- Implement proper error handling
- Use middleware untuk common operations
- Implement rate limiting
- Cache frequently accessed data

## MVP Requirements

### Minimum Features
1. Form klaim voucher dengan fields:
   - Social media type (IG/TikTok)
   - Username
   - Nomor WA
   - Email
   - Checklist verifikasi (like, comment, share)

2. Verifikasi social media:
   - Integrasi dengan API social media
   - Validasi aktivitas user
   - Error handling

3. Wheel of Fortune:
   - Animasi putar
   - Konfigurasi probabilitas hadiah
   - Generate & display kode voucher
   - Record hasil di database

### Data Tracking
- Track user berdasarkan nomor WA dan email
- Record semua attempts klaim voucher
- Track success rate verifikasi
- Monitor penggunaan voucher

## Next Steps
1. Setup development environment
2. Initialize database schema
3. Create basic API endpoints
4. Develop frontend components
5. Integrate social media APIs
6. Implement end-to-end testing
