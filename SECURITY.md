# Security Features

This static resume website implements modern security best practices.

## Implemented Security Measures

### 1. Content Security Policy (CSP)
- **Prevents XSS attacks** by restricting resource loading
- Only allows styles and resources from same origin
- Blocks inline scripts completely
- No external resource loading (except self-hosted)

### 2. HTTP Security Headers

#### X-Content-Type-Options: nosniff
- Prevents MIME-type sniffing attacks
- Forces browser to respect declared content types

#### X-Frame-Options: DENY
- Prevents clickjacking attacks
- Blocks embedding in iframes completely

#### X-XSS-Protection: 1; mode=block
- Enables browser's XSS filter
- Blocks page rendering if attack detected

#### Referrer-Policy: strict-origin-when-cross-origin
- Protects privacy by limiting referrer information
- Sends only origin for cross-origin requests

#### Permissions-Policy
- Disables unnecessary browser features:
  - Geolocation
  - Microphone
  - Camera
  - Payment APIs
  - USB access
  - Other sensors

#### Strict-Transport-Security (HSTS)
- Forces HTTPS connections only
- Includes subdomains
- 1-year duration
- Preload ready

### 3. Link Security
- All external links use `rel="noopener noreferrer"`
- Prevents tab-napping attacks
- Protects against window.opener exploitation

### 4. Azure Static Web Apps Security

#### Automatic HTTPS
- Free SSL/TLS certificates
- Automatic certificate renewal
- TLS 1.2+ only

#### DDoS Protection
- Built-in Azure DDoS protection
- Global CDN with rate limiting

#### No Server-Side Code
- Static files only = minimal attack surface
- No database = no SQL injection risk
- No backend = no server vulnerabilities

### 5. Cache Control
- Optimal caching headers for performance
- Static assets cached for 1 year
- HTML files revalidated every hour

### 6. MIME Type Security
- Explicit MIME type declarations
- Prevents content-type confusion attacks

## Security Scanning

### Recommended Tools:
1. **Mozilla Observatory** - https://observatory.mozilla.org
2. **Security Headers** - https://securityheaders.com
3. **SSL Labs** - https://www.ssllabs.com/ssltest/

### Run a security scan:
```powershell
# Using Mozilla Observatory API
curl "https://http-observatory.security.mozilla.org/api/v1/analyze?host=your-site.azurestaticapps.net"

# Check SSL/TLS configuration
curl "https://api.ssllabs.com/api/v3/analyze?host=your-site.azurestaticapps.net"
```

## What This Site Does NOT Collect

✅ No cookies  
✅ No analytics/tracking  
✅ No user input forms  
✅ No JavaScript execution  
✅ No third-party resources  
✅ No personal data collection  

This is a **pure static, read-only resume** with zero data collection.

## Compliance

This site follows:
- **OWASP Top 10** web security standards
- **GDPR** (no data collection = compliant)
- **WCAG 2.1** accessibility guidelines
- **Azure Well-Architected Framework** security pillar

## Security Score Targets

When deployed, expect these scores:

| Tool | Expected Score |
|------|---------------|
| Mozilla Observatory | A+ |
| SecurityHeaders.com | A+ |
| SSL Labs | A+ |
| Lighthouse Security | 100 |

## Reporting Security Issues

If you discover a security vulnerability:
1. **Do NOT** open a public issue
2. Email: bryan@cabillan.com
3. Include detailed description and reproduction steps

## Updates

Security headers and configurations are reviewed quarterly and updated as new best practices emerge.

**Last Security Review:** October 15, 2026
