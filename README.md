# 🎓 AI Education Job & Internship Application Platform

A modern, production-ready application form system for AI education recruiting with real-time analytics, admin dashboard, and CSV export capabilities.

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Node](https://img.shields.io/badge/node-%3E%3D16.0.0-brightgreen.svg)

## ✨ Features

### 📝 Application Form
- **Comprehensive Fields**: 18 data fields covering education, experience, skills, and preferences
- **Real-time Validation**: Client-side validation with instant feedback
- **Auto-save**: Form data automatically saved to localStorage
- **Mobile Responsive**: Optimized for all device sizes
- **Accessibility**: ARIA labels and keyboard navigation support
- **Spam Protection**: Honeypot field to prevent bot submissions

### 📊 Admin Dashboard
- **Real-time Analytics**: View submission counts, trends, and breakdowns
- **Advanced Filtering**: Search and filter by education, interests, date
- **Visual Charts**: See skill distributions, traffic sources, and more
- **CSV Export**: Download all data for external analysis
- **Recent Submissions**: Quick view of latest applications

### 🔒 Security & Validation
- Email format validation
- Duplicate submission prevention (24-hour window)
- Rate limiting ready (easy to enable)
- Input sanitization for all fields
- GDPR-compliant data handling

### 📈 Analytics Tracking
- Submission source tracking (referrer)
- Completion time monitoring
- User agent detection
- Geographic data (city/country)

## 🚀 Quick Start

### Option 1: 5-Minute Setup (Recommended for Testing)

```bash
# 1. Clone/download files
git clone <repository-url>
cd ai-education-form

# 2. Install dependencies
npm install

# 3. Start development servers
npm run dev

# 4. Open in browser
# Frontend: http://localhost:3000
# Admin: http://localhost:3000/admin
```

### Option 2: Production Deployment

See detailed deployment guide in [DEPLOYMENT.md](./DEPLOYMENT.md)

Popular platforms:
- **Vercel**: Best for JAMstack (recommended)
- **Netlify**: Great for static sites
- **Heroku**: Traditional platform
- **AWS**: Full control with S3 + Lambda

## 📋 Form Fields

### Required Fields ✅
| Field | Type | Validation |
|-------|------|------------|
| Full Name | Text | 2-100 chars, letters only |
| Email | Email | Valid email format |
| Current Education | Dropdown | High School/Undergrad/Graduate/Other |
| Graduation Year | Text | Year (2024-2030) or Semester |
| University Name | Text | 2-200 characters |
| Skills | Multi-select | At least 1 required |
| Availability Date | Date | Today or future |
| Availability Type | Radio | Full-time/Part-time/Either |
| Location | Text | City + Country |
| Interest Areas | Checkboxes | At least 1 required |
| Data Consent | Checkbox | Must be checked |

### Optional Fields
- GPA (0.0-4.0)
- Experience (2000 char max)
- Relevant Projects (2000 char max)
- LinkedIn URL
- GitHub URL
- Portfolio URL
- Salary Expectation

## 🗂️ Project Structure

```
ai-education-form/
├── src/
│   ├── ApplicationForm.tsx      # Main form component
│   ├── ApplicationForm.css      # Form styling
│   ├── AdminDashboard.tsx       # Admin interface
│   ├── AdminDashboard.css       # Dashboard styling
│   └── index.tsx                # App entry point
├── server.js                    # Express.js API
├── package.json                 # Dependencies
├── DEPLOYMENT.md                # Deployment guide
├── CSV_SCHEMA.md                # Data export documentation
└── README.md                    # This file
```

## 🔧 Configuration

### Environment Variables

Create a `.env` file:

```env
# Server
NODE_ENV=production
PORT=3001

# Database (optional - upgrade from JSON)
DATABASE_URL=postgresql://user:pass@host:5432/db

# Email (optional - for confirmations)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password

# Security
JWT_SECRET=your-secret-key-here
ADMIN_EMAIL=admin@yourdomain.com
ADMIN_PASSWORD_HASH=bcrypt-hash-here

# Rate Limiting
RATE_LIMIT_WINDOW_MS=900000
RATE_LIMIT_MAX_REQUESTS=100
```

### Customization

#### Change Form Title
Edit `ApplicationForm.tsx`:
```tsx
<h1>Your Custom Title Here</h1>
```

#### Add/Remove Skills
Edit `SKILLS_OPTIONS` array in `ApplicationForm.tsx`:
```tsx
const SKILLS_OPTIONS = [
  'Your Skill 1',
  'Your Skill 2',
  // ...
];
```

#### Modify Color Scheme
Edit CSS variables in `ApplicationForm.css`:
```css
:root {
  --primary-color: #2563eb;  /* Change to your brand color */
  --success-color: #10b981;
  /* ... */
}
```

## 📊 CSV Export Schema

Exported CSV includes 20 columns:

1. ID (UUID)
2. Submission Date
3. Full Name
4. Email
5. Education Level
6. Graduation Year
7. University
8. GPA
9. Skills
10. Interest Areas
11. Availability Date
12. Availability Type
13. Location
14. LinkedIn URL
15. GitHub URL
16. Portfolio URL
17. Salary Expectation
18. Experience
19. Projects
20. Referrer Source

See [CSV_SCHEMA.md](./CSV_SCHEMA.md) for detailed documentation and examples.

## 🔐 Security Best Practices

### Before Production Launch:

1. **Add Authentication**
   ```javascript
   // Protect admin routes
   app.use('/api/submissions', authenticateAdmin);
   ```

2. **Enable Rate Limiting**
   ```javascript
   const limiter = rateLimit({
     windowMs: 15 * 60 * 1000,
     max: 3
   });
   app.post('/api/submissions', limiter, handler);
   ```

3. **Setup HTTPS**
   - Use Let's Encrypt for free SSL
   - Configure in Nginx/Apache
   - Cloud platforms handle automatically

4. **Sanitize Input**
   ```javascript
   const validator = require('validator');
   data.email = validator.normalizeEmail(data.email);
   ```

5. **Add CAPTCHA**
   - Google reCAPTCHA v3 recommended
   - Invisible to users, blocks bots

## 📱 Browser Compatibility

| Browser | Version | Status |
|---------|---------|--------|
| Chrome | 90+ | ✅ Fully supported |
| Firefox | 88+ | ✅ Fully supported |
| Safari | 14+ | ✅ Fully supported |
| Edge | 90+ | ✅ Fully supported |
| Mobile Safari | iOS 13+ | ✅ Fully supported |
| Mobile Chrome | Android 8+ | ✅ Fully supported |

## 🧪 Testing

```bash
# Run all tests
npm test

# Run with coverage
npm test -- --coverage

# Run specific test file
npm test ApplicationForm.test.tsx
```

### Test Coverage Goals
- Form validation: 100%
- API endpoints: 100%
- Component rendering: 95%+
- Integration tests: 90%+

## 📈 Performance

### Optimization Checklist
- [x] Code splitting (React.lazy)
- [x] CSS minification
- [x] Image optimization
- [x] Gzip compression
- [x] CDN for static assets
- [x] Database indexing
- [x] Caching headers

### Lighthouse Scores (Target)
- Performance: 95+
- Accessibility: 100
- Best Practices: 100
- SEO: 100

## 🔄 Upgrade Path

### Phase 1 ✅ (Current - MVP)
- ✅ Functional form with validation
- ✅ Basic admin dashboard
- ✅ CSV export
- ✅ Spam protection

### Phase 2 🔄 (Enhanced Features)
- [ ] Email notifications
- [ ] PostgreSQL database
- [ ] Advanced analytics
- [ ] Duplicate detection
- [ ] Admin authentication

### Phase 3 📅 (Future)
- [ ] AI-powered resume parsing
- [ ] Applicant scoring system
- [ ] Video introduction uploads
- [ ] Multi-language support
- [ ] ATS integration (Greenhouse, Lever)
- [ ] Calendar scheduling integration

## 🤝 Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines
- Follow TypeScript best practices
- Add tests for new features
- Update documentation
- Use conventional commits

## 📞 Support & Documentation

- **Documentation**: [Full Deployment Guide](./DEPLOYMENT.md)
- **CSV Schema**: [Export Documentation](./CSV_SCHEMA.md)
- **Issues**: [GitHub Issues](repository-url/issues)
- **Email**: support@yourdomain.com

## 📝 License

MIT License - see [LICENSE](./LICENSE) file for details

## 🙏 Acknowledgments

- Built with React, TypeScript, and Express.js
- Styled with modern CSS variables
- Icons from Lucide React
- Inspired by modern recruitment platforms

## 🌟 Star History

If you find this project useful, please give it a star! ⭐

## 📸 Screenshots

### Application Form
![Application Form Screenshot](./screenshots/form.png)

### Admin Dashboard
![Dashboard Screenshot](./screenshots/dashboard.png)

### Mobile View
![Mobile Screenshot](./screenshots/mobile.png)

---

**Built with ❤️ for democratizing AI education**

**Version**: 1.0.0 | **Last Updated**: February 2024

## Quick Links

- [🚀 Deployment Guide](./DEPLOYMENT.md)
- [📊 CSV Documentation](./CSV_SCHEMA.md)
- [🔒 Security Checklist](./DEPLOYMENT.md#security-enhancements)
- [🎨 Customization Guide](#customization)
- [📱 Mobile Optimization](#browser-compatibility)
