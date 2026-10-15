# Bryan Cabillan - Resume Website

A professional, mobile-responsive static resume website designed for Azure Static Web Apps deployment.

## Features

- **Responsive Design**: Optimized for desktop, tablet, and mobile (QR code scanning)
- **Print-Friendly**: Clean print layout for PDF generation
- **Modern UI**: Professional gradient design with clean typography
- **Fast Loading**: Pure HTML/CSS with no dependencies
- **SEO Optimized**: Proper meta tags and semantic HTML

## Deployment Options

### Option 1: Deploy via GitHub (Recommended)

This method provides automatic CI/CD deployment whenever you push changes.

#### Step 1: Create GitHub Repository

```powershell
# Initialize git repository
cd "c:\Users\Bryan Skyline\Documents\Kiro\BryanResume"
git init
git add .
git commit -m "Initial commit: Professional resume website"

# Create GitHub repo (requires GitHub CLI)
gh repo create bryan-resume --public --source=. --remote=origin --push
```

If you don't have GitHub CLI installed:
1. Go to [GitHub.com](https://github.com/new)
2. Create a new repository named `bryan-resume`
3. Follow the push instructions shown

#### Step 2: Create Azure Static Web App via Azure Portal

1. Go to [Azure Portal](https://portal.azure.com)
2. Click **Create a resource** → Search for **Static Web App**
3. Click **Create**
4. Fill in the details:
   - **Subscription**: Your Azure subscription
   - **Resource Group**: Create new or select existing
   - **Name**: `bryan-resume` (or your preferred name)
   - **Plan type**: **Free** (perfect for resume sites)
   - **Region**: Choose closest to your target audience
   - **Source**: **GitHub**
   - **Sign in** to GitHub when prompted
   - **Organization**: Your GitHub username
   - **Repository**: `bryan-resume`
   - **Branch**: `main` or `master`
   - **Build Presets**: Choose **Custom**
   - **App location**: `/` (root directory)
   - **API location**: Leave empty
   - **Output location**: Leave empty
5. Click **Review + create** → **Create**

Azure will automatically:
- Create a GitHub Actions workflow
- Deploy your site
- Provide you with a URL like: `https://your-site.azurestaticapps.net`

### Option 2: Deploy via Azure CLI

This is faster if you prefer command-line deployment.

#### Prerequisites

```powershell
# Install Azure CLI if not already installed
# Download from: https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows

# Login to Azure
az login

# Install Static Web Apps CLI extension
az extension add --name staticwebapp
```

#### Deploy

```powershell
# Set variables
$RESOURCE_GROUP = "resume-rg"
$LOCATION = "centralus"
$APP_NAME = "bryan-resume"

# Create resource group
az group create --name $RESOURCE_GROUP --location $LOCATION

# Create Static Web App with manual deployment
az staticwebapp create `
  --name $APP_NAME `
  --resource-group $RESOURCE_GROUP `
  --location $LOCATION `
  --sku Free

# Get deployment token
$TOKEN = az staticwebapp secrets list `
  --name $APP_NAME `
  --resource-group $RESOURCE_GROUP `
  --query "properties.apiKey" `
  --output tsv

# Deploy the site
cd "c:\Users\Bryan Skyline\Documents\Kiro\BryanResume"
npx @azure/static-web-apps-cli deploy `
  --app-location . `
  --deployment-token $TOKEN

# Get the URL
az staticwebapp show `
  --name $APP_NAME `
  --resource-group $RESOURCE_GROUP `
  --query "defaultHostname" `
  --output tsv
```

### Option 3: Deploy via VS Code Extension

1. Install [Azure Static Web Apps extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestaticwebapps)
2. Right-click on the `BryanResume` folder
3. Select **Deploy to Static Web App**
4. Follow the prompts

## Custom Domain (Optional)

Once deployed, you can add a custom domain:

1. In Azure Portal, go to your Static Web App
2. Click **Custom domains** in the left menu
3. Click **Add** → **On other DNS**
4. Follow instructions to add CNAME record to your DNS provider
5. Your resume will be available at `resume.cabillan.com` or similar

## Generate QR Code

Once your site is deployed, create a QR code:

### Online QR Code Generators:
- [QR Code Generator](https://www.qr-code-generator.com/)
- [QR Code Monkey](https://www.qrcode-monkey.com/)
- [Adobe Express](https://www.adobe.com/express/feature/image/qr-code-generator)

### Using PowerShell:
```powershell
# Install QR Code module
Install-Module -Name QRCodeGenerator -Scope CurrentUser

# Generate QR Code
$url = "https://your-site.azurestaticapps.net"
New-QRCode -Data $url -OutPath "resume-qr-code.png" -Width 300
```

### Tips for QR Code:
- **Size**: At least 300x300 pixels for business cards
- **Error Correction**: Use High (H) level for durability
- **Test**: Scan from multiple devices before printing
- **Shortened URL**: Consider using Azure Custom Domain or bit.ly for cleaner URLs

## Testing Locally

To test locally before deployment:

```powershell
# Option 1: Using Python
cd "c:\Users\Bryan Skyline\Documents\Kiro\BryanResume"
python -m http.server 8000
# Visit: http://localhost:8000

# Option 2: Using VS Code Live Server extension
# Install "Live Server" extension in VS Code
# Right-click index.html → "Open with Live Server"

# Option 3: Using Static Web Apps CLI
npx @azure/static-web-apps-cli start
```

## Updating Your Resume

1. Edit `index.html` to update content
2. Modify `style.css` to change styling
3. Commit and push changes (if using GitHub deployment):
   ```powershell
   git add .
   git commit -m "Update resume content"
   git push
   ```
4. GitHub Actions will automatically redeploy

## Cost

- **Azure Static Web Apps Free Tier**:
  - 100 GB bandwidth per month
  - Custom domains with free SSL
  - No credit card required for trial
  - Perfect for personal resume sites

## Support

For issues or questions:
- [Azure Static Web Apps Documentation](https://learn.microsoft.com/en-us/azure/static-web-apps/)
- [GitHub Discussions](https://github.com/Azure/static-web-apps/discussions)

---

**Your resume URL will be**: `https://<your-app-name>.azurestaticapps.net`

Print this or generate a QR code to share easily!
