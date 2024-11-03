# Python Virtual Environment & Uvicorn Deployment Guide

## Prerequisites
- Python 3.8 or higher
- pip (Python package installer)

## Setting Up a Virtual Environment

### 1. Create a Virtual Environment
```bash
# Windows
python -m venv venv

# Linux/MacOS
python3 -m venv venv
```

### 2. Activate the Virtual Environment

```bash
# Windows
venv\Scripts\activate

# Linux/MacOS
source venv/bin/activate
```

You'll know it's activated when you see `(venv)` in your terminal prompt.

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

If you don't have a requirements.txt, create one:
```bash
pip freeze > requirements.txt
```

## Running with Uvicorn

### 1. Install Uvicorn
```bash
pip install uvicorn
```

### 2. Basic Running Commands
```bash
# Development
uvicorn main:app --reload

# Production
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
```

Key parameters:
- `--reload`: Enable auto-reload on code changes (development only)
- `--workers`: Number of worker processes (recommended: 2 * CPU cores + 1)
- `--host`: Bind socket to this host
- `--port`: Bind socket to this port

## Deployment Best Practices

### 1. Project Structure
```
your_project/
├── venv/
├── app/
│   ├── __init__.py
│   ├── main.py
│   └── routers/
├── requirements.txt
└── README.md
```

### 2. Production Configuration
```bash
# Production settings
export PYTHONPATH="${PYTHONPATH}:${PWD}"
export ENVIRONMENT="production"
```

### 3. Using a Process Manager (e.g., Supervisor)

Example supervisor configuration (/etc/supervisor/conf.d/myapp.conf):
```ini
[program:myapp]
command=/path/to/venv/bin/uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
directory=/path/to/your/app
user=youruser
autostart=true
autorestart=true
stderr_logfile=/var/log/myapp.err.log
stdout_logfile=/var/log/myapp.out.log
```

### 4. Environment Variables
Create a `.env` file for environment variables:
```env
ENVIRONMENT=production
DEBUG=0
DATABASE_URL=postgresql://user:password@localhost/dbname
```

### 5. Security Considerations
- Never commit `.env` files or sensitive credentials
- Use HTTPS in production
- Set secure headers
- Implement rate limiting
- Keep dependencies updated

## Common Commands

### Virtual Environment
```bash
# Create new virtual environment
python -m venv venv

# Activate
source venv/bin/activate  # Linux/MacOS
venv\Scripts\activate     # Windows

# Deactivate
deactivate

# Update pip
pip install --upgrade pip
```

### Dependencies
```bash
# Install packages
pip install package_name

# Install from requirements
pip install -r requirements.txt

# Update requirements file
pip freeze > requirements.txt
```

### Uvicorn
```bash
# Development with reload
uvicorn main:app --reload

# Production with multiple workers
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4

# SSL/TLS support
uvicorn main:app --ssl-keyfile=./key.pem --ssl-certfile=./cert.pem
```

## Troubleshooting

### Common Issues
1. **Port already in use**
   ```bash
   # Find process using port
   lsof -i :8000    # Linux/MacOS
   netstat -ano | findstr :8000  # Windows
   ```

2. **Permission denied**
   - Check file permissions
   - Ensure virtual environment is activated
   - Use sudo when required (system-level operations only)

3. **Module not found**
   - Verify virtual environment is activated
   - Check requirements.txt
   - Confirm PYTHONPATH includes project root

### Logs
- Check uvicorn logs: Usually printed to stdout
- Supervisor logs: `/var/log/supervisor/`
- Application logs: Configure based on your logging setup

## Additional Resources
- [Uvicorn Documentation](https://www.uvicorn.org/)
- [Python venv documentation](https://docs.python.org/3/library/venv.html)
- [Supervisor Documentation](http://supervisord.org/)
