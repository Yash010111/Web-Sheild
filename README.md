# Vulnerability Scanner for Web Applications

A comprehensive web-based vulnerability scanner designed to identify potential security issues in web applications. Built with Flask backend and a modern, responsive web frontend, this tool performs automated security assessments against target URLs and generates detailed PDF reports.

## 🎯 Features

### Security Vulnerability Detection
The scanner implements comprehensive checks for the following vulnerability types:

- **SQL Injection Detection** - Tests for SQL injection vulnerabilities using common payloads to detect improper input handling
- **Cross-Site Scripting (XSS)** - Identifies XSS vulnerabilities through payload injection and script execution detection
- **Broken Authentication** - Tests for weak credentials, default accounts, and session management issues
- **Broken Access Control** - Checks for unauthorized access to restricted resources and permission bypass
- **CSRF Protection** - Identifies Cross-Site Request Forgery vulnerabilities and missing anti-CSRF tokens
- **Security Misconfiguration** - Detects exposed configuration files, debug modes, default credentials, and missing security patches
- **Sensitive Data Exposure** - Warns about HTTP usage, plaintext data transmission, and unencrypted sensitive information
- **SSRF Vulnerabilities** - Tests for Server-Side Request Forgery issues
- **Cryptographic Failures** - Identifies improperly encrypted sensitive data and weak cryptographic implementations
- **Remote File Inclusion (RFI)** - Detects RFI vulnerabilities through file inclusion testing
- **Server Information Disclosure** - Server header analysis and version detection
- **HTTP Methods Enumeration** - Detects enabled HTTP methods and tests for dangerous configurations

### Additional Features
- **Nikto-style Checks**
  - Server header analysis and version detection
  - Common file discovery (.env, robots.txt, .git/config, phpinfo.php, etc.)
  - HTTP method enumeration
  - SSL/TLS certificate analysis
  - Directory path scanning using wordlists
  
- **User Interface**
  - Clean, responsive, and intuitive web interface
  - Real-time vulnerability scanning feedback
  - Interactive scanner page with detailed results display
  - About page with comprehensive documentation
  - Home page with project information and quick access

- **Reporting**
  - PDF report generation with scan results
  - Detailed vulnerability explanations in reports
  - Scan metadata and timestamps
  - Professional formatting and layout

## 📋 Requirements

- Python 3.x
- Flask 2.3.0+
- Flask-CORS 4.0.0+
- Requests library 2.31.0+
- ReportLab 4.0.7+ (for PDF report generation)

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Vulnerability-Scanner-for-Web-Applications
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```
   
   Or manually install:
   ```bash
   pip install Flask==2.3.0 Flask-CORS==4.0.0 requests==2.31.0 reportlab==4.0.7
   ```

## 🔧 Configuration

The application is configured to work out-of-the-box with the following default settings:

- **Development Server**: Flask development server running on `localhost:5000`
- **CORS Support**: Cross-Origin Resource Sharing (CORS) enabled for cross-domain requests
- **Template Directory**: HTML templates loaded from the current directory
- **Static Files**: Static assets (CSS, images) served from the `static/` folder
- **Request Timeout**: 5 seconds per HTTP request during scanning
- **Error Handling**: Comprehensive error handling with JSON responses

## ▶️ Running the Application

### Step 1: Start the Flask Server
```bash
python code/scanner.py
```

The server will start with output similar to:
```
 * Running on http://127.0.0.1:5000
 * Debug mode: off
```

### Step 2: Access the Application
Open your web browser and navigate to:
```
http://localhost:5000
```

### Step 3: Run a Vulnerability Scan
1. Navigate to the Scanner page using the navigation menu
2. Enter the target URL (e.g., `https://example.com` or `https://testsite.local`)
3. Click the **"Start Scan"** button to begin the vulnerability assessment
4. Wait for the scan to complete (typically 10-30 seconds depending on target responsiveness)
5. Review the detailed results showing all identified vulnerabilities
6. Optionally download the PDF report for documentation purposes

## 📁 Project Structure

```
Vulnerability-Scanner-for-Web-Applications/
├── code/
│   ├── scanner.py              # Flask backend application (main server)
│   ├── index.html              # Home page with scanner interface
│   ├── scanner.html            # Scanner results and reporting page
│   ├── about.html              # About page with documentation
│   ├── style.css               # Global stylesheet
│   ├── requirements.txt        # Python package dependencies
│   └── static/
│       └── style.css           # Additional styling
├── LICENSE                     # License file
├── README.md                   # This file
└── .gitignore                  # Git ignore file
```

## 🔍 How It Works

### Backend Architecture (scanner.py)
The Flask application provides a modular scanning framework:

1. **Route Handlers**
   - `GET /` - Serves the home page
   - `GET /about` - Serves the about/documentation page
   - `GET /scanner` - Serves the scanner interface
   - `POST /scan` - API endpoint for vulnerability scanning

2. **Vulnerability Detection Engine**
   - Modular design with separate functions for each vulnerability type
   - SQL injection payload testing with common injection patterns
   - XSS payload injection and response analysis
   - HTTP method enumeration and analysis
   - SSL/TLS certificate validation
   - Server header fingerprinting
   - Common file discovery using wordlists
   - Authentication testing with default credentials

3. **Error Handling**
   - Graceful exception handling for network errors
   - Request timeouts to prevent hanging
   - JSON error responses for API consistency
   - Detailed logging for debugging

### Frontend Architecture
The web interface provides:

1. **Interactive Forms**
   - URL input validation
   - AJAX-based form submission
   - Real-time scan status updates
   - Error message display

2. **Results Display**
   - Formatted vulnerability listing
   - Color-coded severity indicators
   - Scrollable results container
   - Download PDF report functionality

3. **Responsive Design**
   - Mobile-friendly layout
   - Desktop optimization
   - Touch-friendly buttons and controls

### Vulnerability Detection Methods

Each vulnerability check follows this process:

1. **Payload Generation** - Creates test payloads specific to the vulnerability type
2. **Request Execution** - Sends HTTP requests to target with payloads
3. **Response Analysis** - Examines responses for vulnerability indicators
4. **Result Aggregation** - Collects findings with descriptions
5. **Error Handling** - Manages network errors without stopping the scan

## ⚙️ API Endpoints

### GET `/`
Returns the home page with the scanner interface.

**Response**: HTML home page

### GET `/about`
Returns the about page with documentation and information.

**Response**: HTML about page

### GET `/scanner`
Returns the scanner interface page.

**Response**: HTML scanner page

### POST `/scan`
Performs a comprehensive vulnerability scan on the target URL.

**Request:**
```json
{
  "url": "https://target-website.com"
}
```

**Response (Success):**
```json
{
  "results": [
    "[+] SQL Injection vulnerability detected with payload: 1=1",
    "[+] XSS vulnerability found: <script>alert('XSS')</script>",
    "Server: Apache/2.4.41 (Ubuntu)",
    "[+] Found: /robots.txt",
    "[-] Forbidden: /admin/",
    "Allowed HTTP methods: GET, HEAD, OPTIONS"
  ]
}
```

**Response (Error):**
```json
{
  "error": "Error message describing the issue"
}
```

## ⚠️ Important Notes

### Legal and Ethical Use

**⚠️ CRITICAL: Only use this tool on systems you own or have explicit written permission to test.**

- Unauthorized security scanning of systems you do not own is **illegal** in most jurisdictions
- This tool is intended for **educational and authorized penetration testing purposes only**
- Always obtain **written permission** from the system owner before testing
- Comply with all local laws and regulations regarding security testing
- Violations may result in criminal and/or civil penalties

### Limitations

- This is a **basic scanner** designed for educational purposes
- Detection methods are **signature-based** and may produce false positives or false negatives
- Real-world penetration testing requires more sophisticated tools and manual analysis
- The scanner may not detect all vulnerability types or obfuscated attacks
- Results should be verified manually and with professional security tools
- Does not perform deep code analysis or advanced exploitation

### Performance Considerations

- **Scan Duration**: Typically 10-30 seconds depending on target responsiveness
- **Request Timeout**: 5 seconds per request (prevents hanging on unresponsive targets)
- **Network Dependency**: Requires stable internet connection to target
- **Target Availability**: Target must be online and accessible
- **Rate Limiting**: Some targets may have rate limiting that could affect results

### Browser Compatibility

- Modern browsers with JavaScript enabled (Chrome, Firefox, Safari, Edge)
- Requires cookies and local storage enabled
- WebSocket support recommended for real-time updates

## 🛠️ Customization

### Adding Custom Payloads

Edit the payload lists in [scanner.py](code/scanner.py) to add custom test payloads:

```python
# SQL injection test payloads
SQL_PAYLOADS = ['1=1', "' OR '1'='1", "' AND 1=0--", "'; DROP TABLE users;--"]

# XSS test payloads
XSS_PAYLOADS = [
    '<script>alert("XSS")</script>',
    '<img src="x" onerror="alert(1)">',
    '<svg onload=alert(1)>',
    'javascript:alert(1)'
]

# Default credentials to test
COMMON_CREDENTIALS = [
    ('admin', 'admin'),
    ('root', 'root'),
    ('user', 'password'),
    ('guest', 'guest'),
    ('test', 'test123')
]

# Common files and directories to search for
WORDLIST = ["admin", "backup", "config", "login", "test", "users", "uploads", "api"]
```

### Customizing the User Interface

Modify [code/style.css](code/style.css) and [code/static/style.css](code/static/style.css) to customize:

- Color scheme and branding
- Layout and spacing
- Font styles
- Button appearance
- Animation effects

### Adding New Vulnerability Checks

Create new scanning functions following the existing pattern:

```python
def check_new_vulnerability(url, results):
    """
    Check for a new type of vulnerability.
    
    Args:
        url: The target URL to scan
        results: List to append findings to
    """
    try:
        response = requests.get(url, timeout=5)
        
        # Your detection logic here
        if some_vulnerability_detected:
            results.append("[+] New vulnerability found!")
        else:
            results.append("[-] No vulnerability detected")
            
    except requests.RequestException as e:
        results.append(f"[-] Error checking: {str(e)}")
    except Exception as e:
        results.append(f"[-] Unexpected error: {str(e)}")

# Add to perform_scan function
def perform_scan(target_url):
    results = initialize_results()
    check_new_vulnerability(target_url, results)  # Add your check
    # ... other checks
    return results
```

## 📊 Sample Output

A typical scan produces results like:

```
[+] Nikto Scan Results:
Server: Apache/2.4.41 (Ubuntu)
Found: /robots.txt
Forbidden: /admin/
Not Found: /config.php
X-Frame-Options: SAMEORIGIN
Allowed HTTP methods: GET, HEAD, OPTIONS

[+] SQL Injection Vulnerabilities:
[+] SQL Injection detected with payload: 1=1
[+] SQL Injection detected with payload: ' OR '1'='1

[+] XSS Vulnerabilities:
[+] XSS vulnerability detected with payload: <script>alert("XSS")</script>

[+] Security Issues:
[+] Security Misconfiguration detected: Exposed .env file
[+] Sensitive Data Exposure: Using HTTP instead of HTTPS

[-] No broken authentication detected
[-] No access control issues found
[-] No CSRF vulnerabilities found
```

## 🐛 Troubleshooting

### Issue: "Server won't start" or "Address already in use"
**Solution:**
- Ensure Python 3.x is installed: `python --version`
- Check that port 5000 is not in use: `netstat -ano | findstr :5000` (Windows)
- Install all dependencies: `pip install -r requirements.txt`
- Try running on a different port by modifying `app.run(port=5001)` in scanner.py

### Issue: "Module not found" or "ImportError"
**Solution:**
- Ensure all dependencies are installed: `pip install -r requirements.txt`
- Check Python version compatibility (requires Python 3.6+)
- Use virtual environment: `python -m venv venv` then activate it

### Issue: CORS errors in browser console
**Solution:**
- CORS is enabled by default via Flask-CORS
- Clear browser cache and cookies
- Try accessing from `http://localhost:5000` (not 127.0.0.1)
- Check browser console for detailed error messages

### Issue: Scan times out or hangs
**Solution:**
- Target may be unresponsive or blocking requests
- Check internet connection stability
- Verify the target URL is correct and accessible
- Increase request timeout in scanner.py if needed
- Check if target has rate limiting or WAF blocking requests

### Issue: False positives in results
**Solution:**
- Some results may be false positives due to signature-based detection
- Always manually verify findings on the actual target
- Use additional security tools for confirmation
- Review error messages carefully (prefixed with `[-]`)

### Issue: PDF report download fails
**Solution:**
- Ensure ReportLab is installed: `pip install reportlab`
- Check browser's download settings
- Verify adequate disk space
- Try in a different browser

## 📚 References

- [OWASP Top 10](https://owasp.org/www-project-top-ten/) - Most critical web application security risks
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/) - Comprehensive security testing methodology
- [Flask Documentation](https://flask.palletsprojects.com/) - Flask framework reference
- [Requests Library](https://requests.readthedocs.io/) - HTTP library documentation
- [OWASP API Security](https://owasp.org/www-project-api-security/) - API-specific security guidance
- [CWE/SANS Top 25](https://cwe.mitre.org/top25/) - Software weakness rankings

## 📄 License

This project is provided as-is for educational and authorized testing purposes. See [LICENSE](LICENSE) file for details.

## 👨‍💻 Contributing

Contributions are welcome! To contribute:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/new-feature`
3. **Make your changes** and test thoroughly
4. **Follow existing code style** and conventions
5. **Add appropriate error handling** for reliability
6. **Update documentation** if adding new features
7. **Submit a pull request** with a clear description

### Development Guidelines

- Maintain code readability and consistency
- Add docstrings to new functions
- Test changes on multiple URLs
- Ensure no hardcoded paths or credentials
- Handle exceptions gracefully
- Follow Flask and Python best practices

## 🔒 Security Disclaimer

**This tool is provided strictly for authorized security testing and educational purposes.**

- **Unauthorized access** to computer systems without permission is illegal
- The authors are **not responsible** for misuse or illegal activity
- Always obtain **written permission** before testing any system
- Understand and follow **all applicable laws and regulations**
- Use responsibly and ethically

---

**Last Updated**: December 2024  
**Developed for**: Educational and Authorized Penetration Testing
