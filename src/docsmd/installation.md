# Installation

Follow these steps to install Platform Akademik on your local machine.

## Clone the Repository

```bash
git clone https://github.com/your-repo/platform-akademik.git
cd platform-akademik
```

## Install Dependencies

Using npm:

```bash
npm install
```

Or using pnpm (recommended):

```bash
pnpm install
```

## Environment Setup

Create a `.env` file in the root directory:

```env
VITE_API_URL=https://api.platform-akademik.dev
VITE_APP_NAME=Platform Akademik
VITE_DEBUG_MODE=false
```

## Start Development Server

```bash
npm run dev
```

The application will be available at `http://localhost:5173`

## Build for Production

```bash
npm run build
npm run preview
```

> **Tip:** Make sure you have Node.js version 18 or higher installed. You can check your version by running `node -v`

## Troubleshooting

### Common Issues

**Port already in use:**
```bash
# Kill the process using port 5173
npx kill-port 5173
```

**Dependencies not installing:**
```bash
# Clear npm cache and reinstall
rm -rf node_modules package-lock.json
npm install
```

## Docker Installation (Optional)

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 5173
CMD ["npm", "run", "dev"]
```

```bash
docker build -t platform-akademik .
docker run -p 5173:5173 platform-akademik
```
