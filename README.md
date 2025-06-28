# ETF Screener Gateway

A load-balancing nginx gateway that distributes requests between multiple ETF backend services.

## Backends

- **Backend 1**: https://etf-scanner-backend.onrender.com/
- **Backend 2**: https://etf-screener-backend-production.up.railway.app/

## Features

- Round-robin load balancing (50/50 distribution)
- SSL termination and proper SNI handling
- Rate limiting (10 requests/second per IP)
- Health check endpoint at `/health`
- Debug headers showing which backend handled each request

## Test Endpoints

- `/health` - Health check
- `/test/backend1` - Test Render backend directly
- `/test/backend2` - Test Railway backend directly
- `/api/prices` - Load balanced API endpoint

## Deployment

### Fly.io

```bash
# Install flyctl if not already installed
# https://fly.io/docs/hands-on/install-flyctl/

# Login to Fly.io
flyctl auth login

# Deploy the application
flyctl deploy

# Check status
flyctl status

# View logs
flyctl logs
```

## Configuration

The nginx configuration includes:
- Load balancing using microsecond-based distribution
- SSL verification disabled for upstream connections
- Proper host headers for each backend
- Rate limiting and security headers
- Comprehensive logging for debugging