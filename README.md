# 🔹 Multi-Tenant SaaS Store Platform

A professional multi-tenant SaaS platform that allows store owners to create and manage their own independent stores. Each store has its own admin dashboard, public storefront, isolated data, and customizable themes.

## 🚀 Features

- **Multi-Tenant Architecture**: Complete data isolation between stores
- **Role-Based Access Control**: Owner, Editor, and Viewer roles
- **Store Management**: Full CRUD operations for products, categories, tags
- **Media Manager**: Per-store image storage with compression and organization
- **Activity Logging**: Complete audit trail of all store operations
- **Public Storefront**: Dynamic store URLs with i18n support (English + Arabic with RTL)
- **Promotional Banners**: Customizable promotional banners per store
- **Discount System**: Visual discount badges and pricing
- **Analytics**: Store visits, product views, and message statistics
- **Theme Customization**: Colors, fonts, display modes per store

## 📋 Prerequisites

- Node.js 18+ and npm/yarn
- PostgreSQL database (local or Railway)
- Git

## 🛠️ Local Setup

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd profesional-web-business
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

Copy `.env.example` to `.env` and fill in your values:

```bash
cp .env.example .env
```

Edit `.env`:
- `DATABASE_URL`: Your PostgreSQL connection string
- `JWT_SECRET`: Generate with `openssl rand -base64 32`
- `APP_URL`: `http://localhost:3000` for local development
- `STORAGE_PATH`: `./storage` for local file storage

### 4. Set up the database

```bash
# Generate Prisma client
npm run db:generate

# Run migrations
npm run db:migrate

# (Optional) Seed database with sample data
npm run db:seed
```

### 5. Create storage directory

```bash
mkdir -p storage
```

### 6. Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## 🚢 Deployment to Railway

### 1. Prepare Railway project

1. Create a new project on [Railway](https://railway.app)
2. Add a PostgreSQL service
3. Copy the `DATABASE_URL` from the PostgreSQL service

### 2. Configure environment variables

In Railway, add these environment variables:
- `DATABASE_URL`: From PostgreSQL service
- `JWT_SECRET`: Generate a strong secret
- `APP_URL`: Your Railway app URL (e.g., `https://your-app.railway.app`)
- `STORAGE_PATH`: `/app/storage` or use S3

### 3. Connect GitHub repository

1. In Railway, click "New" → "GitHub Repo"
2. Select your repository
3. Railway will auto-detect Next.js and build

### 4. Auto-migration setup

The `build` script in `package.json` includes:
```json
"build": "prisma generate && prisma migrate deploy && next build"
```

This ensures migrations run automatically on each deployment.

### 5. Deploy

Railway will automatically:
- Build your app
- Run migrations
- Deploy to production

## 📁 Project Structure

```
├── app/                    # Next.js App Router
│   ├── (auth)/            # Authentication routes
│   ├── (dashboard)/       # Admin dashboard routes
│   ├── store/[slug]/      # Public storefront routes
│   └── api/               # API routes
├── components/            # React components
├── lib/                   # Utilities and helpers
│   ├── prisma.ts         # Prisma client
│   ├── auth.ts           # Authentication utilities
│   ├── store-access.ts   # Store access control
│   └── activity-log.ts   # Activity logging
├── prisma/               # Prisma schema and migrations
├── storage/              # File storage (images, media)
└── public/               # Static assets
```

## 🔐 Creating a New Store

### Via API (for development)

1. Register/Login as a user
2. Create a store through the dashboard or API
3. Store will be assigned a unique slug
4. Access admin at `/dashboard/stores/[storeId]`
5. Public store at `/store/[slug]`

### First Store Setup

1. After creating a store, you'll be redirected to the store dashboard
2. Configure store settings (name, description, logo)
3. Customize theme (colors, fonts)
4. Add products, categories, and tags
5. Set up promotional banners
6. Share your public store link: `/store/[your-slug]`

## 🔗 Accessing Stores

### Admin Dashboard
- URL: `https://your-domain.com/dashboard/stores/[storeId]`
- Requires authentication
- Role-based access control

### Public Storefront
- URL: `https://your-domain.com/store/[store-slug]`
- No authentication required
- Supports English and Arabic (RTL)
- Customers can browse products and send messages

## 👥 User Roles

- **Owner**: Full access to store (create, edit, delete, manage users)
- **Editor**: Can create/edit products, categories, tags, upload images
- **Viewer**: Read-only access to store data

## 📊 Environment Variables Reference

| Variable | Description | Example |
|----------|-------------|---------|
| `DATABASE_URL` | PostgreSQL connection string | `postgresql://user:pass@host:5432/db?sslmode=require` |
| `JWT_SECRET` | Secret key for JWT tokens | Generated random string |
| `APP_URL` | Base URL of your application | `https://your-app.railway.app` |
| `STORAGE_PATH` | Path for file storage | `./storage` or `/app/storage` |
| `MAX_FILE_SIZE_MB` | Maximum file upload size | `10` |
| `MAX_IMAGE_SIZE_MB` | Maximum image upload size | `5` |

## 🧪 Testing

### Demo Store Account

After deployment, you can create a demo store:
1. Register a new account
2. Create a store
3. Add sample products
4. Customize theme and banners
5. Share the public link

## 📝 API Routes

- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/logout` - Logout user
- `GET /api/stores` - List user's stores
- `POST /api/stores` - Create new store
- `GET /api/stores/[id]` - Get store details
- `PUT /api/stores/[id]` - Update store
- `GET /api/stores/[id]/products` - List products
- `POST /api/stores/[id]/products` - Create product
- ... (more routes in development)

## 🔒 Security Features

- JWT-based authentication
- Password hashing with bcrypt
- Role-based access control (RBAC)
- Store data isolation
- CSRF protection
- Input validation with Zod
- File upload size limits

## 🌐 Internationalization

- Admin dashboard: English only
- Public storefront: English (default) + Arabic (optional)
- Automatic RTL layout when Arabic is selected
- Language preference stored per store

## 📦 Tech Stack

- **Framework**: Next.js 14 (App Router)
- **Database**: PostgreSQL with Prisma ORM
- **Authentication**: JWT with HTTP-only cookies
- **Styling**: Tailwind CSS
- **UI Components**: Custom components with Tailwind
- **Image Processing**: Sharp for compression and optimization
- **Deployment**: Railway (with auto-migrations)
- **File Storage**: Local filesystem (can be extended to S3)

## 🎯 Key Features Implemented

✅ **Multi-Tenant Architecture**
- Complete data isolation between stores
- Store-specific slugs for public URLs
- Per-store settings and themes

✅ **Authentication & Authorization**
- JWT-based authentication
- Role-based access control (Owner, Editor, Viewer)
- Secure password hashing with bcrypt

✅ **Store Management**
- Create and manage multiple stores
- Store settings and customization
- Logo and cover image support

✅ **Product Management**
- Full CRUD operations for products
- Multiple images per product
- Categories and tags
- SKU management
- Stock tracking
- Active/Inactive status

✅ **Discount System**
- Original and discounted pricing
- Visual discount badges
- Discount validation (discounted price must be less than original)

✅ **Promotional Banners**
- Create multiple promotional banners
- Image and text support
- Display order control
- Active/Inactive toggle

✅ **Media Manager**
- Per-store image storage
- Automatic image compression
- File size limits
- Image optimization with Sharp

✅ **Public Storefront**
- Dynamic store URLs: `/store/[slug]`
- English and Arabic language support
- Automatic RTL layout for Arabic
- Product browsing and filtering
- Product detail pages
- Contact form

✅ **Activity Logging**
- Complete audit trail
- Tracks all store operations
- User, action, entity, and timestamp

✅ **Analytics**
- Store visit tracking
- Product view statistics
- Top products
- Message counts

✅ **Customer Management**
- Customer directory
- Message/inquiry system
- Contact form on public storefront

## 🚀 Quick Start

### Local Development

1. **Clone and install**:
   ```bash
   git clone <your-repo-url>
   cd profesional-web-business
   npm install
   ```

2. **Set up environment**:
   ```bash
   cp .env.example .env
   # Edit .env with your database URL and secrets
   ```

3. **Set up database**:
   ```bash
   npm run db:generate
   npm run db:migrate
   npm run db:seed  # Optional: seed demo data
   ```

4. **Create storage directory**:
   ```bash
   mkdir -p storage
   ```

5. **Run development server**:
   ```bash
   npm run dev
   ```

6. **Access the app**:
   - Open [http://localhost:3000](http://localhost:3000)
   - Register a new account
   - Create your first store

### Demo Account

After seeding, you can login with:
- Email: `demo@example.com`
- Password: `demo123456`

## 📁 Project Structure

```
├── app/
│   ├── (auth)/              # Authentication pages
│   │   ├── login/
│   │   └── register/
│   ├── (dashboard)/         # Admin dashboard
│   │   └── dashboard/
│   │       └── stores/
│   │           └── [id]/
│   │               ├── products/
│   │               ├── settings/
│   │               └── media/
│   ├── store/               # Public storefront
│   │   └── [slug]/
│   │       ├── page.tsx     # Store homepage
│   │       └── product/
│   │           └── [productSlug]/
│   └── api/                 # API routes
│       ├── auth/
│       └── stores/
│           └── [id]/
│               ├── products/
│               ├── categories/
│               ├── tags/
│               ├── settings/
│               ├── banners/
│               ├── messages/
│               ├── upload/
│               └── stats/
├── components/             # React components
│   ├── store-frontend.tsx
│   ├── product-detail-page.tsx
│   ├── products-list.tsx
│   └── logout-button.tsx
├── lib/                    # Utilities
│   ├── prisma.ts          # Prisma client
│   ├── auth.ts            # Authentication
│   ├── store-access.ts    # Access control
│   ├── activity-log.ts    # Activity logging
│   └── utils.ts           # Helper functions
├── prisma/
│   ├── schema.prisma      # Database schema
│   └── seed.ts            # Seed script
└── storage/               # File storage (per store)
```

## 🔐 Security Features

- **JWT Authentication**: Secure token-based authentication
- **Password Hashing**: bcrypt with salt rounds
- **Role-Based Access Control**: Owner, Editor, Viewer roles
- **Data Isolation**: Complete separation between stores
- **Input Validation**: Server-side validation on all inputs
- **File Upload Limits**: Size and type restrictions
- **CSRF Protection**: Built-in Next.js protection

## 🌐 Internationalization

- **Admin Dashboard**: English only
- **Public Storefront**: English (default) + Arabic
- **RTL Support**: Automatic RTL layout when Arabic is selected
- **Language Toggle**: Easy switching between languages

## 📊 Database Schema

Key models:
- `User`: Platform users
- `Store`: Store/tenant instances
- `StoreMember`: User roles within stores
- `StoreSettings`: Theme and customization
- `Product`: Products with pricing and discounts
- `ProductImage`: Product images
- `Category`: Product categories
- `Tag`: Product tags
- `Customer`: Customer directory
- `Message`: Customer inquiries
- `ViewsStats`: Analytics tracking
- `ActivityLog`: Audit trail
- `PromotionalBanner`: Promotional content

## 🚢 Deployment

See [DEPLOYMENT.md](./DEPLOYMENT.md) for detailed deployment instructions to Railway.

### Railway Deployment Steps

1. Push code to GitHub
2. Create Railway project
3. Add PostgreSQL database
4. Set environment variables
5. Deploy (auto-build and migrations)

## 📝 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/logout` - Logout user
- `GET /api/auth/me` - Get current user

### Stores
- `GET /api/stores` - List user's stores
- `POST /api/stores` - Create new store
- `GET /api/stores/[id]` - Get store details
- `PUT /api/stores/[id]` - Update store
- `DELETE /api/stores/[id]` - Delete store

### Products
- `GET /api/stores/[id]/products` - List products
- `POST /api/stores/[id]/products` - Create product
- `GET /api/stores/[id]/products/[productId]` - Get product
- `PUT /api/stores/[id]/products/[productId]` - Update product
- `DELETE /api/stores/[id]/products/[productId]` - Delete product

### Categories & Tags
- `GET /api/stores/[id]/categories` - List categories
- `POST /api/stores/[id]/categories` - Create category
- `GET /api/stores/[id]/tags` - List tags
- `POST /api/stores/[id]/tags` - Create tag

### Settings & Customization
- `GET /api/stores/[id]/settings` - Get store settings
- `PUT /api/stores/[id]/settings` - Update settings
- `GET /api/stores/[id]/banners` - List banners
- `POST /api/stores/[id]/banners` - Create banner
- `PUT /api/stores/[id]/banners/[bannerId]` - Update banner
- `DELETE /api/stores/[id]/banners/[bannerId]` - Delete banner

### Media & Analytics
- `POST /api/stores/[id]/upload` - Upload image
- `GET /api/stores/[id]/messages` - List messages
- `POST /api/stores/[id]/messages` - Create message (public)
- `GET /api/stores/[id]/stats` - Get statistics
- `GET /api/stores/[id]/activity` - Get activity logs

## 🎨 Customization

### Store Themes
- Primary and secondary colors
- Font family selection
- Display mode (grid/cards)
- Language preference

### Promotional Banners
- Multiple banners per store
- Image and text content
- Custom ordering
- Active/inactive toggle

## 📈 Future Enhancements

Potential features to add:
- Order management system
- Payment gateway integration
- Email notifications
- Advanced analytics dashboard
- Multi-currency support
- Inventory management
- Shipping integration
- Customer reviews
- Wishlist functionality
- Search functionality
- Product variants (size, color, etc.)

## 🤝 Contributing

This is a proprietary project. For issues or questions, please contact the project maintainer.

## 📄 License

Proprietary - All rights reserved

---

**Built with ❤️ for professional multi-tenant store management**

## 📄 License

This project is proprietary and confidential.

## 🤝 Support

For issues and questions, please open an issue in the repository.

---

**Built with ❤️ for professional multi-tenant store management**

