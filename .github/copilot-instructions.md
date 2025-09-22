# Ficha Ordem Foda - Character Sheet and Combat Tracker
A single-page HTML application for managing character sheets and combat rounds in tabletop RPGs. The application is built with React 18, uses TailwindCSS for styling, and runs entirely in the browser without a backend server.

**ALWAYS reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.**

## Working Effectively

### Prerequisites and Dependencies
- **CRITICAL**: This application requires internet access to load external CDN resources
- External dependencies loaded from CDNs:
  - TailwindCSS (`https://cdn.tailwindcss.com`)
  - React 18 (`https://unpkg.com/react@18/umd/react.development.js`)
  - React DOM 18 (`https://unpkg.com/react-dom@18/umd/react-dom.development.js`)
  - Babel Standalone (`https://unpkg.com/@babel/standalone/babel.min.js`)
- **No build system required** - this is a pure HTML/JavaScript application
- **No package.json or dependency management** - all dependencies are loaded via CDN

### Running the Application
1. **Start a local HTTP server** (required due to CORS restrictions):
   ```bash
   cd /home/runner/work/Ficha-Ordem-Foda/Ficha-Ordem-Foda
   python3 -m http.server 8080
   ```
   - **Server starts instantly** (< 1 second) - NEVER CANCEL this command
   - **Runs in background** - use `&` to continue working: `python3 -m http.server 8080 &`
   - Access at: `http://localhost:8080/contador-rodadas.html`
   - **Stop server**: `pkill -f "python3 -m http.server"`

2. **Alternative HTTP servers**:
   ```bash
   # Node.js (if available)
   npx serve .
   # PHP (if available)  
   php -S localhost:8080
   ```

### Application Structure
- **Single file**: `contador-rodadas.html` (47KB, 661 lines)
- **No build process** - edit the HTML file directly
- **React components** written in JSX using Babel transpilation in the browser
- **State management** uses React hooks (useState, useEffect)
- **Styling** via inline TailwindCSS classes and embedded CSS

### Core Functionality
The application has two main tabs:
1. **Ficha (Character Sheet)** - Manage player characters, NPCs, and enemies with:
   - Basic stats (HP, PE, Stability, Initiative)
   - Character attributes and equipment
   - Effects and status tracking
2. **Cena (Scene/Combat)** - Combat round management with:
   - Turn order and initiative tracking
   - Round counter
   - Combat log
   - Real-time HP/status updates

### Development Workflow
- **Edit directly**: Modify `contador-rodadas.html` 
- **Test changes**: Refresh browser page - changes are immediate
- **No compilation needed** - JavaScript is transpiled by Babel in the browser

## Timing and Performance

### Command Execution Times
- **File operations**: < 100ms (file is only 47KB)
- **HTTP server startup**: < 1 second - NEVER CANCEL
- **Page load**: < 500ms (without CDN dependencies)
- **With CDN access**: 2-5 seconds for full application load
- **Edit-to-test cycle**: < 1 second (just refresh browser)

### Expected File Sizes
- `contador-rodadas.html`: 47,922 bytes (47KB)
- **No build artifacts** - single file application
- **No dependency downloads** - all external CDN resources

### Performance Characteristics
- **Memory usage**: Minimal (single HTML page)
- **No build time** - zero compilation required
- **No install time** - no package managers or dependencies
- **Browser rendering**: Depends on CDN availability

## Validation

### CRITICAL - External Dependency Check
**ALWAYS verify external CDN access before testing functionality:**
```bash
curl -I https://cdn.tailwindcss.com
curl -I https://unpkg.com/react@18/umd/react.development.js
curl -I https://unpkg.com/react-dom@18/umd/react-dom.development.js
curl -I https://unpkg.com/@babel/standalone/babel.min.js
```
- **Expected in sandboxed environments**: `curl: (6) Could not resolve host` errors
- If any CDN is blocked, the application will not function
- Browser console will show exactly 4 "Failed to load resource: net::ERR_BLOCKED_BY_CLIENT" errors
- **This is normal and expected behavior** in restricted environments

### Manual Validation Scenarios
**ALWAYS run these scenarios after making changes:**

1. **Basic Application Load**:
   - Start HTTP server
   - Open `http://localhost:8080/contador-rodadas.html`
   - Verify no console errors (except blocked CDN resources)
   - Confirm application interface loads with dark theme

2. **Character Management Test**:
   - Click "Ficha" tab (should be active by default)
   - Test all sub-tabs: "Players", "NPCs", "Desafios"
   - Add a new character in each category
   - Edit character attributes (nome, PV, PE, initiatives)
   - Verify data persists when switching between tabs

3. **Combat Scene Test**:
   - Click "Cena" tab
   - Verify characters from Ficha appear in combat list
   - Test initiative ordering
   - Advance turns and rounds
   - Modify HP/PE values in combat
   - Verify changes reflect back in Ficha tab

4. **Data Persistence Test**:
   - Create characters and combat scenario
   - Use "Export" button to download JSON file
   - Clear data or refresh page
   - Use "Import" button to restore from JSON
   - Verify all data restored correctly

5. **Local Storage Test**:
   - Create test data
   - Click "Salvar Local" (Save Local)
   - Refresh browser page  
   - Click "Carregar Local" (Load Local)
   - Verify data restored from browser localStorage

### Expected Behavior When CDNs Are Blocked
- Application title appears: "Contador Rodadas App — Revisado (Stable)"
- Page background is dark (#202632)
- **React components do NOT render** - blank page with just title
- Console shows exactly 4 CDN loading errors:
  - `Failed to load resource: net::ERR_BLOCKED_BY_CLIENT.Inspector @ https://unpkg.com/react@18/u...`
  - `Failed to load resource: net::ERR_BLOCKED_BY_CLIENT.Inspector @ https://unpkg.com/react-dom@...`
  - `Failed to load resource: net::ERR_BLOCKED_BY_CLIENT.Inspector @ https://cdn.tailwindcss.com/...`
  - `Failed to load resource: net::ERR_BLOCKED_BY_CLIENT.Inspector @ https://unpkg.com/@babel/sta...`
- **This is normal in restricted environments** - the app requires internet access to function

## Common Development Tasks

### Adding New Features
1. **For UI components**: Edit the JSX inside `<script type="text/babel">` section
2. **For styling**: Add CSS rules in the `<style>` section (lines 8-59)  
3. **For state management**: Use existing React hooks patterns (useState, useEffect)

### Key Code Sections
- **Lines 1-62**: HTML head with external dependencies and CSS
- **Lines 63-661**: React application code in JSX
- **Lines 68-143**: Utility functions (dice rolling, stability calculations)
- **Lines 144-233**: FichaPlayer component (player character sheet)
- **Lines 234-260**: FichaNPC component (NPC/enemy sheet)
- **Lines 261-543**: Scene component (combat management)
- **Lines 544-660**: Main App component with tab management

### Data Model Understanding
- **Players**: Full RPG character sheets with PE, stability, equipment
- **NPCs**: Simplified characters (people/animals) with basic stats  
- **Desafios**: Enemy/challenge creatures for combat
- **Scene State**: Combat rounds, turn order, effects, combat log

### localStorage Integration
- **Key**: `contador_rodadas_app_v1`
- **Data**: Complete application state as JSON
- **Functions**: `handleSaveLocal()`, `handleLoadLocal()`, `handleClearLocal()`

## Troubleshooting

### CDN Access Issues (Most Common)
- **Problem**: Application shows blank page with title only
- **Cause**: External CDN resources blocked (firewall/network restrictions)
- **Diagnostic**: Check browser console for 4 specific CDN errors
- **Solution**: This is expected in sandboxed environments - document as "requires internet access"
- **Workaround**: Not applicable - application requires CDN access to function

### Application Won't Load
- **Check internet connection** for CDN access
- **Verify HTTP server** is running (not file:// protocol)  
- **Check browser console** for specific errors
- **Try different port**: `python3 -m http.server 8081`

### Changes Not Appearing  
- **Hard refresh browser** (Ctrl+F5 or Cmd+Shift+R)
- **Check for JavaScript syntax errors** in console
- **Verify file saved correctly** with `head -5 contador-rodadas.html`

### Data Not Persisting
- **Test localStorage**: Check browser settings allow localStorage
- **Export/Import broken**: Verify JSON file format with `jq` or JSON validator
- **Characters missing in Scene**: Check Ficha tab data first

### Performance Issues
- File size: 47KB loads instantly (< 100ms)
- **No build optimization needed** - already minified CDN resources
- **Large character data**: Export and analyze JSON size if > 1MB

### Quick Validation Commands
```bash
# Validate file structure and size
ls -la                                    # Should show: contador-rodadas.html (47,922 bytes)
wc -c contador-rodadas.html              # Should output: 47922
wc -l contador-rodadas.html              # Should output: 661

# Test server responsiveness  
curl -I http://localhost:8080/contador-rodadas.html   # Should return: HTTP/1.0 200 OK

# Verify no build system files
find . -name "package*.json" -o -name "webpack*" -o -name "*.lock" | wc -l   # Should output: 0
```

## Repository Structure
```
.
├── contador-rodadas.html    # Single-page application (47KB)
├── .git/                   # Git repository 
└── .github/                # GitHub configuration
    └── copilot-instructions.md  # This file
```

### No Build System Files
This repository intentionally has NO:
- package.json / yarn.lock / pnpm-lock.yaml
- webpack.config.js / vite.config.js / rollup.config.js  
- Dockerfile / docker-compose.yml
- Makefile / build scripts
- Source directories (src/, dist/, build/)

**This is by design** - it's a self-contained HTML application.