# Microsoft Teams Activity Monitor

A comprehensive web-based tool for monitoring Microsoft Teams user activity and detecting potentially retired or inactive users in your organization. Built with Next.js, React, and Microsoft Graph API integration.

## 🌟 Features

### 1. **Teams Activity Lookup Tool**
- Check individual user's Teams presence and activity status
- Real-time presence detection (Available, Away, Busy, Offline)
- Last activity timestamp tracking
- History of recent lookups
- Export results to clipboard

### 2. **Retired User Detector**
- Advanced scoring algorithm to identify potentially retired employees
- Single user or bulk analysis (up to 50 users)
- Multi-factor retirement risk assessment including:
  - Account status (enabled/disabled)
  - Last sign-in activity
  - Teams presence and activity
  - License assignments
  - Group memberships
- Risk levels: High, Medium, Low, Active
- Export results to CSV
- Actionable recommendations for each risk level

### 3. **PowerShell Guide**
- Comprehensive step-by-step instructions for Teams management via PowerShell
- Code snippets with copy functionality
- Permission requirements and setup
- Troubleshooting tips
- Best practices for bulk operations

## 📋 Prerequisites

- Node.js 14.0 or higher
- npm or yarn package manager
- Microsoft 365 organization
- Microsoft Graph API access with appropriate permissions

## 🚀 Quick Start

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/TeamsActivityMonitor.git
cd TeamsActivityMonitor
```

### 2. Install Dependencies
```bash
npm install
# or
yarn install
```

### 3. Configure Environment Variables
Copy the `.env.example` file to `.env`:
```bash
cp .env.example .env
```

Edit the `.env` file and add your Microsoft Graph API credentials:
```env
MICROSOFT_CLIENT_ID=your_client_id_here
MICROSOFT_CLIENT_SECRET=your_client_secret_here
MICROSOFT_TENANT_ID=your_tenant_id_here
```

### 4. Run the Development Server
```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## 🔐 Setting Up Microsoft Graph API Access

### Step 1: Register an App in Azure Portal

1. Go to [Azure Portal](https://portal.azure.com)
2. Navigate to **Azure Active Directory** → **App registrations**
3. Click **New registration**
4. Configure your app:
   - **Name**: Teams Activity Monitor
   - **Supported account types**: Accounts in this organizational directory only
   - **Redirect URI**: Leave blank for now
5. Click **Register**

### Step 2: Configure API Permissions

1. In your app registration, go to **API permissions**
2. Click **Add a permission** → **Microsoft Graph**
3. Choose **Application permissions**
4. Add these permissions:
   - `User.Read.All` - Read all users' profiles
   - `Presence.Read.All` - Read presence information
   - `Reports.Read.All` - Read usage reports
   - `Directory.Read.All` - Read directory data
5. Click **Grant admin consent** (requires admin privileges)

### Step 3: Create Client Secret

1. Go to **Certificates & secrets**
2. Click **New client secret**
3. Add a description and select expiry period
4. Click **Add**
5. **Copy the secret value immediately** (it won't be shown again)

### Step 4: Get Your Credentials

From the app overview page, copy:
- **Application (client) ID** → `MICROSOFT_CLIENT_ID`
- **Directory (tenant) ID** → `MICROSOFT_TENANT_ID`
- Your copied secret → `MICROSOFT_CLIENT_SECRET`

## 📱 Usage Guide

### Teams Activity Lookup
1. Navigate to `/teams-activity-lookup`
2. Enter a username or email address
3. Click "Lookup" to check their current Teams status
4. View presence, activity, and last activity time
5. Copy results or check history of recent lookups

### Retired User Detector
1. Navigate to `/retired-user-detector`
2. Choose between:
   - **Single User**: Enter one email address
   - **Bulk Analysis**: Paste up to 50 email addresses (one per line)
3. Click "Analyze" to run the detection algorithm
4. Review retirement risk scores and recommendations
5. Export results to CSV for reporting

### PowerShell Guide
1. Navigate to `/powershell-guide`
2. Follow the step-by-step instructions
3. Copy code snippets as needed
4. Use for advanced Teams management tasks

## 🎯 Retirement Detection Algorithm

The tool uses a weighted scoring system to assess retirement risk:

| Indicator | Weight | Description |
|-----------|--------|-------------|
| Account Status | 30% | Checks if account is disabled or blocked |
| Last Sign-in | 25% | Days since last authentication |
| Teams Activity | 20% | Recent Teams presence and activity |
| License Status | 15% | Active licenses and usage |
| Group Membership | 10% | Active directory and security groups |

### Risk Levels
- **80-100%**: High Risk - Immediate action recommended
- **60-79%**: Medium Risk - Investigation recommended
- **30-59%**: Low Risk - Monitor for changes
- **0-29%**: Active User - No action needed

## 🛠️ Development

### Project Structure
```
├── src/
│   ├── app/
│   │   ├── teams-activity-lookup/    # Activity lookup tool
│   │   ├── retired-user-detector/    # Retirement detection tool
│   │   └── powershell-guide/         # PowerShell documentation
│   ├── api/
│   │   └── teams-activity/           # API routes for Teams data
│   └── components/                   # Reusable React components
├── public/                           # Static assets
└── package.json                      # Dependencies and scripts
```

### Available Scripts
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run start` - Start production server
- `npm run lint` - Run ESLint

### Technology Stack
- **Frontend**: Next.js 14, React 18, TailwindCSS
- **API Integration**: Microsoft Graph API
- **Styling**: TailwindCSS, FontAwesome icons
- **Deployment**: Vercel-ready

## 📊 API Endpoints

### POST `/api/teams-activity`
Check Teams activity for a specific user.

**Request Body:**
```json
{
  "username": "user@domain.com"
}
```

**Response:**
```json
{
  "username": "user@domain.com",
  "displayName": "John Doe",
  "lastActivity": "2024-01-27T10:30:00Z",
  "presence": {
    "availability": "Available",
    "activity": "Available"
  },
  "timestamp": "2024-01-27T10:35:00Z"
}
```

## 🐛 Troubleshooting

### Common Issues

#### "Failed to authenticate with Microsoft Graph API"
- Verify your environment variables are set correctly
- Check that your client secret hasn't expired
- Ensure admin consent has been granted for API permissions

#### "User not found"
- Verify the email address is correct
- Check that the user exists in your Microsoft 365 tenant
- Ensure you have `User.Read.All` permission

#### Rate Limiting
- The tool includes built-in rate limiting for bulk operations
- If you encounter throttling, reduce batch sizes or add delays

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with [Next.js](https://nextjs.org/)
- Styled with [TailwindCSS](https://tailwindcss.com/)
- Icons from [FontAwesome](https://fontawesome.com/)
- Microsoft Graph API integration

## 📧 Support

For issues, questions, or suggestions, please:
- Open an issue on GitHub
- Contact your organization's IT administrator
- Review the [Microsoft Graph documentation](https://docs.microsoft.com/en-us/graph/)

## ⚠️ Disclaimer

This tool is designed for legitimate administrative purposes only. Ensure you have proper authorization before monitoring user activity in your organization. Always comply with your organization's privacy policies and local regulations regarding employee monitoring.

---

**Note**: Currently, the tool displays simulated data for demonstration purposes. Connect your Microsoft Graph API credentials to enable real-time Teams activity monitoring.