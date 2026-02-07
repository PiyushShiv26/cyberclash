# CyberClash

A secure blog platform built with Express.js, EJS, and SQLite.

## Features

- User authentication with sessions
- Create, view, and delete blog posts
- Admin dashboard
- Role-based access control
- Responsive design with Bootstrap

## Prerequisites

- Node.js >= 16.0.0
- npm >= 8.0.0

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd cyberclash
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```bash
cp .env.example .env
```

4. Edit `.env` and configure your settings:
   - **IMPORTANT**: Change `SESSION_SECRET` to a strong random string in production
   - Generate a secure secret: `node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"`

## Running the Application

### Development Mode
```bash
npm run dev
```

### Production Mode
```bash
npm run prod
```

The application will be available at `http://localhost:3000` (or the port specified in `.env`)

## Default Users

The application creates default users on first run:
- **Admin**: username: `admin`, password: `admin123`
- **User**: username: `alice`, password: `alice123`

**⚠️ IMPORTANT**: Change these default credentials immediately in production!

## Deployment

### Environment Variables

Ensure these environment variables are set in production:

- `PORT` - The port to run the server on (default: 3000)
- `NODE_ENV` - Set to `production` for production deployments
- `SESSION_SECRET` - A strong random string for session security

### Production Deployment Steps

1. **Update dependencies**:
```bash
npm ci --production
```

2. **Set environment variables**:
   - Set `NODE_ENV=production`
   - Set a strong `SESSION_SECRET`
   - Configure `PORT` if needed

3. **Start the application**:
```bash
npm start
```

### Recommended: Using PM2 for Production

For production deployments, use a process manager like PM2:

```bash
# Install PM2 globally
npm install -g pm2

# Start the application
pm2 start app.js --name cyberclash

# Setup auto-restart on server reboot
pm2 startup
pm2 save
```

### Docker Deployment (Optional)

Create a `Dockerfile`:
```dockerfile
FROM node:16-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --production

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

Build and run:
```bash
docker build -t cyberclash .
docker run -p 3000:3000 -e SESSION_SECRET=your-secret-here cyberclash
```

### Deployment Platforms

This application can be deployed to:
- **Heroku**: Add a `Procfile` with `web: npm start`
- **Railway**: Automatic detection, just set environment variables
- **Render**: Set build command to `npm install` and start command to `npm start`
- **DigitalOcean App Platform**: Configure via their UI
- **AWS EC2/Elastic Beanstalk**: Use PM2 or systemd for process management

## Security Considerations

✅ SQL Injection protection using parameterized queries  
✅ Session security with httpOnly cookies  
✅ Environment-based configuration  
⚠️ **TODO**: Implement password hashing (bcryptjs is installed but not used)  
⚠️ **TODO**: Add HTTPS in production  
⚠️ **TODO**: Implement CSRF protection  
⚠️ **TODO**: Add rate limiting for login attempts  

## Project Structure

```
cyberclash/
├── app.js              # Main application file
├── package.json        # Dependencies and scripts
├── .env.example        # Environment variables template
├── app.db              # SQLite database (auto-created)
└── views/              # EJS templates
    ├── index.ejs
    ├── login.ejs
    ├── posts.ejs
    ├── new.ejs
    ├── edit.ejs
    └── admin.ejs
```

## License

ISC
