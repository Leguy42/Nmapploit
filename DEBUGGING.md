# Nmap Exploit Analyzer - Node.js Debugging Guide

## Debugging Core Logic with Node.js

### Option 1: Test Suite Debugging (No Dependencies)

The project includes `nmap-exploit-analyzer.test.js` with a complete test suite that extracts and tests the core logic without React/Vite dependencies.

**Run the test suite:**
```bash
node nmap-exploit-analyzer.test.js
```

This tests:
- ✓ Nmap results parsing
- ✓ Host/port extraction
- ✓ Multi-host parsing
- ✓ Exploit matching logic
- ✓ Service detection

### Option 2: VS Code Node.js Debugger

To debug the core logic with breakpoints:

1. **Open the test file:**
   - Open `nmap-exploit-analyzer.test.js` in VS Code

2. **Set breakpoints:**
   - Click line numbers to place breakpoints
   - Example: Set breakpoint on line 96 in `parseNmapResults()` function

3. **Start debugging:**
   - Press `Cmd+Shift+D` (Mac) or `Ctrl+Shift+D` (Windows/Linux)
   - Select "Debug Test File" configuration
   - OR run: `node --inspect-brk nmap-exploit-analyzer.test.js`

4. **Debug commands:**
   - F10: Step over
   - F11: Step into
   - F5: Continue
   - Shift+F5: Stop
   - View variables in Debug Sidebar

### Option 3: Step Through with Chrome DevTools

1. Run with Node.js inspector:
```bash
node --inspect nmap-exploit-analyzer.test.js
```

2. Open Chrome and navigate to: `chrome://inspect`

3. Click "inspect" on the target process

4. Set breakpoints and debug interactively

## Debugging the React Component

For React debugging in the browser:

1. **Install dependencies first:**
```bash
npm install
```

2. **Start dev server:**
```bash
npm run dev
```

3. **Open browser DevTools:** Press F12

4. **React Developer Tools:**
   - Install "React Developer Tools" extension
   - Debug component state and props
   - Performance profiling available

## Key Functions to Debug

### 1. `parseNmapResults(text)`
Parses Nmap scan output and extracts hosts/ports.

**Add debug output:**
```javascript
const parsed = parseNmapResults(sampleNmapData);
console.log('Parsed hosts:', parsed);
console.log('First host ports:', parsed[0].ports);
```

### 2. `findExploits(service, version)`
Matches services to known vulnerabilities.

**Add debug output:**
```javascript
const exploit = findExploits('ftp', 'vsftpd 2.3.4');
console.log('Found exploit:', exploit);
```

### 3. `analyzeScan()`
Main analysis flow combining parsing and exploit matching.

## Sample Nmap Input for Testing

```
Starting Nmap 7.94 ( https://nmap.org )
Nmap scan report for target.mentormaze.local (172.20.0.5)
Host is up (0.00023s latency).
Not shown: 993 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.2
80/tcp   open  http        Apache httpd 2.4.7
139/tcp  open  netbios-ssn Samba smbd 3.0.20-Debian
445/tcp  open  netbios-ssn Samba smbd 3.0.20-Debian
3306/tcp open  mysql       MySQL 5.5.62-0ubuntu0.14.04.1
8080/tcp open  http        Apache Tomcat 5.5.36
```

## Debugging Tips

1. **Add console.log statements** at key points
2. **Check variable types:** Use `typeof` and `instanceof` 
3. **Test regex patterns:** Verify parsing regex independently
4. **Isolate functions:** Test functions separately with known inputs
5. **Use debugger statement:** Add `debugger;` to pause execution

## Project Structure

```
nmap-exploit-analyzer.tsx      # Main React component
nmap-exploit-analyzer.test.js  # Extracted logic + test suite
main.tsx                        # React entry point
vite.config.ts                 # Vite configuration
package.json                   # Dependencies
.vscode/launch.json            # VS Code debug config
```
