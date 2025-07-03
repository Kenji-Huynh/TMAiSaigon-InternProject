# TMAi Saigon - Intern Project

Website chính thức của TMAi Saigon (Technology Management and AI Institute Saigon) - Viện Quản lý Công nghệ và Trí tuệ Nhân tạo Sài Gòn.

## 📋 Mô tả dự án

Đây là dự án intern phát triển website tổng thể cho TMAi Saigon, bao gồm:

- **Frontend**: Website hiển thị thông tin tổ chức, sản phẩm, sự kiện
- **Backend Admin**: Hệ thống quản lý nội dung (CMS) để quản lý dữ liệu

### ✨ Tính năng chính

- 🏢 Giới thiệu về tổ chức TMAi Saigon
- 🤝 Quản lý thông tin đối tác hợp tác
- 📱 Hiển thị sản phẩm đầu tư và websites
- 📚 Quản lý dự án sách xuất bản
- 🌍 Tổ chức sự kiện quốc tế và trong nước
- 🔍 Chức năng tìm kiếm thông minh
- 📍 Bản đồ vị trí văn phòng với Google Maps
- 📱 Thiết kế responsive, tương thích đa thiết bị

## 🛠️ Công nghệ sử dụng

### Frontend
- **[Svelte](https://svelte.dev)** - Framework JavaScript hiệu năng cao
- **[Rollup](https://rollupjs.org)** - Module bundler
- **HTML5/CSS3** - Cấu trúc và giao diện
- **JavaScript ES6+** - Logic ứng dụng

### Backend Admin
- **[Symfony 6.0](https://symfony.com)** - PHP Framework
- **[Doctrine ORM](https://www.doctrine-project.org)** - Quản lý cơ sở dữ liệu
- **[Twig](https://twig.symfony.com)** - Template engine
- **SQLite** - Cơ sở dữ liệu phát triển
- **[VichUploaderBundle](https://github.com/dustin10/VichUploaderBundle)** - Upload files

## 📁 Cấu trúc dự án

```
TMAiSaigon-InternProject/
├── 📁 src/                    # Frontend Svelte source code
│   ├── App.svelte            # Component chính
│   ├── main.js               # Entry point
│   └── components/           # Các component UI
│       ├── Header.svelte     # Header với menu và search
│       ├── Footer.svelte     # Footer thông tin liên hệ
│       └── Slider.svelte     # Image slider component
├── 📁 public/                # Static files & build output
│   ├── index.html           # HTML template
│   ├── global.css           # Global styles
│   ├── build/               # Build output
│   └── images/              # Hình ảnh website
├── 📁 tmai-admin/           # Symfony Admin Backend
│   ├── src/                 # PHP source code
│   ├── templates/           # Twig templates
│   ├── config/              # Configuration files
│   ├── migrations/          # Database migrations
│   └── public/              # Public admin assets
├── package.json             # Frontend dependencies
├── rollup.config.js        # Rollup configuration
└── README.md               # Documentation
```

## 🚀 Cài đặt và chạy dự án

### Yêu cầu hệ thống

- **Node.js** >= 14.0.0
- **PHP** >= 8.0.2
- **Composer** (for PHP dependencies)
- **Git**

### 1. Clone repository

```bash
git clone <repository-url>
cd TMAiSaigon-InternProject
```

### 2. Cài đặt Frontend (Svelte)

```bash
# Cài đặt dependencies
npm install

# Chạy development server
npm run dev
```

Website sẽ chạy tại: `http://localhost:8080`

### 3. Cài đặt Backend Admin (Symfony)

```bash
# Di chuyển vào thư mục admin
cd tmai-admin

# Cài đặt PHP dependencies
composer install

# Tạo database và chạy migrations
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate

# Load sample data (optional)
php bin/console doctrine:fixtures:load

# Chạy Symfony development server
symfony serve
```

Backend admin sẽ chạy tại: `http://localhost:8000`

## 📜 Scripts có sẵn

### Frontend Scripts

```bash
# Development với hot reload
npm run dev

# Build cho production
npm run build

# Serve production build
npm start
```

### Backend Scripts

```bash
# Chạy development server
symfony serve

# Tạo migration mới
php bin/console make:migration

# Chạy migrations
php bin/console doctrine:migrations:migrate

# Clear cache
php bin/console cache:clear
```

## 🔧 Configuration

### Frontend Configuration

Cấu hình chính trong `rollup.config.js`:
- Development/Production modes
- Live reload setup
- CSS extraction
- Asset optimization

### Backend Configuration

Các file cấu hình quan trọng:
- `config/packages/` - Symfony package configurations
- `config/routes.yaml` - API routes definition
- `.env` - Environment variables

### API Endpoints

Backend cung cấp các API endpoints:

```
GET /api/partners          # Danh sách đối tác
GET /api/products          # Sản phẩm đầu tư
GET /api/book-projects     # Dự án sách
GET /api/events            # Sự kiện quốc tế
GET /api/business-events   # Sự kiện kinh doanh
GET /api/website-products  # Sản phẩm websites
```

## 🎨 Customization

### Thêm sections mới

1. Tạo component Svelte mới trong `src/components/`
2. Import và sử dụng trong `App.svelte`
3. Thêm API endpoint tương ứng trong Symfony admin

### Thay đổi styling

- Global styles: `public/global.css`
- Component styles: Trong từng file `.svelte`

### Quản lý hình ảnh

Hình ảnh được tổ chức trong `public/images/`:
- `general/` - Background images
- `events/` - Event photos  
- `human/` - Team member photos
- `internal/` - Internal activity photos
- `logo/` - Brand logos

## 🌐 Deployment

### Production Build

```bash
# Build frontend
npm run build

# Optimize backend
cd tmai-admin
composer install --no-dev --optimize-autoloader
php bin/console cache:clear --env=prod
```

### Environment Variables

Cấu hình các biến môi trường cần thiết:

```env
# Google Maps API
GOOGLE_MAPS_API_KEY=your_api_key_here

# Database (production)
DATABASE_URL=mysql://user:password@host:port/database
```

## 🤝 Contributing

1. Fork repository
2. Tạo feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Tạo Pull Request

## 📞 Liên hệ

- **Website**: [TMAi Saigon](https://tmaisaigon.com)
- **Email**: contact@tmaisaigon.com
- **Địa chỉ**: TP. Hồ Chí Minh, Việt Nam

## 📄 License

This project is proprietary software of TMAi Saigon.

---

*Phát triển bởi TMAi Saigon Intern Team - 2025*
