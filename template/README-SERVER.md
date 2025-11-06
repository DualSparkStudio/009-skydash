# How to Fix 404 Errors

## Common Causes of 404 Errors

1. **Opening HTML file directly** - Don't open `index.html` directly in the browser (file:// protocol)
2. **Wrong server directory** - Server must run from the `template` directory
3. **Missing dependencies** - Run `npm install` first

## Solution

### Step 1: Install Dependencies
```bash
cd template
npm install
```

### Step 2: Start the Server
Run one of these commands from the `template` directory:

**Option A: Using Gulp (Recommended)**
```bash
gulp serve
```

**Option B: Using the batch file**
```bash
start-server.bat
```

**Option C: Using Python (if installed)**
```bash
python -m http.server 8000
```
Then open: http://localhost:8000

**Option D: Using Node.js http-server**
```bash
npx http-server -p 8000
```

### Step 3: Access the Application
- Gulp server: http://localhost:3000
- Python/Node server: http://localhost:8000

## Important Notes

- **Always run the server from the `template` directory** (where `index.html` is located)
- The server must be running - don't open the HTML file directly
- All resource paths in `index.html` are relative to the `template` directory

