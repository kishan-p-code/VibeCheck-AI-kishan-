# VibeCheck AI

> **Brand governance, made intelligent.**

VibeCheck AI is an AI-powered brand-governance platform that helps teams review content before publication. It checks content against brand guidelines, highlights potential issues with clear explanations, and suggests improvements while keeping final decisions in human hands.

**Live Demo:** https://vibe-check-ai-ecru.vercel.app/

---

## Overview

Organisations publish content through multiple employees, agencies, and AI tools. This makes it difficult to maintain a consistent brand voice, use approved terminology, and avoid unsupported claims or off-brand visuals.

VibeCheck AI brings content review and brand governance into one workspace. It combines AI-assisted checks, explainable issue reporting, correction suggestions, team workflows, and governance insights.

## Key Features

### 1. AI-Powered Content Review
- Review text and supported document or image inputs.
- Check tone and brand-voice consistency.
- Identify terminology and language issues.
- Flag potentially unsupported claims and competitor mentions.
- Review images against brand guidance.
- Generate suggested rewrites while preserving the creator's intent.

### 2. Explainable Issue Detection
- Classify findings by severity: **Critical**, **Warning**, or **Suggestion**.
- Explain why an item was flagged.
- Connect findings to the relevant brand rule where available.
- Compare original content with suggested changes.

### 3. Human-Controlled Corrections
- Review suggestions individually.
- Accept, reject, or modify suggested changes.
- Keep the original content under the creator's control; suggestions are not automatically applied.

### 4. Brand Guidelines & Asset Management
- Define brand rules and terminology.
- Manage approved brand assets such as logos, colours, fonts, and imagery.
- Use the Brand Guidelines Builder to configure brand preferences.

### 5. Team Review & Approval Workflow
VibeCheck AI includes four role-based workspace views:

| Role | Main responsibilities |
| --- | --- |
| Creator | Prepare content, run reviews, and submit drafts |
| Reviewer | Inspect submissions, review findings, and provide feedback |
| Manager | Review submissions and make approval decisions |
| Admin | Manage the organisation, team, guidelines, and governance settings |

Submission statuses include Draft, In Review, Approved, and Rejected (with revision-request states used in the workflow).

### 6. Governance Insights & Audit Logs
- View content review and compliance insights.
- Track recurring violation categories.
- Review submission history and audit activity.
- Export an audit report as JSON.

---

## Tech Stack

| Area | Technologies |
| --- | --- |
| Framework | Next.js 14, React 18 |
| Language | TypeScript |
| Styling | Tailwind CSS 3 |
| Icons | Lucide React |
| AI content review | OpenRouter |
| DOCX text extraction | Mammoth.js |
| Image and asset handling | Cloudinary integration |
| Email notifications | Resend integration |
| UI state persistence | Browser localStorage in the current client implementation |

The project also includes a Supabase publishable-key setting in its environment template. Review the current deployment and backend configuration before assuming that database persistence or Supabase authentication is enabled.

---

## Getting Started

### Prerequisites

- Node.js 18 or later
- npm
- API credentials for the external services you want to enable

### 1. Clone the repository

```bash
git clone https://github.com/kishan-p-code/kishan-p-code-vibecheck-ai-kishan-.git
cd kishan-p-code-vibecheck-ai-kishan-
```

If your repository URL or folder name is different, use the corresponding URL and directory.

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a local environment file from the example:

**Windows PowerShell**
```powershell
Copy-Item .env.example .env.local
```

**macOS / Linux**
```bash
cp .env.example .env.local
```

Add the credentials for the services you use:

```env
OPENROUTER_API_KEY=your_openrouter_api_key_here

SUPABASE_PUBLISHABLE_KEY=your_supabase_publishable_key_here

CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret
CLOUDINARY_URL=cloudinary://your_key:your_secret@your_cloud_name

RESEND_API_KEY=your_resend_api_key_here

NEXT_PUBLIC_APP_NAME="VibeCheck AI"
```

Keep private API keys in `.env.local` and in your hosting provider's server-side environment settings. **Do not commit `.env.local` or expose secret keys in client-side code.**

Some features may require their corresponding service credentials. Do not add placeholder values expecting the integrations to work.

### 4. Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### 5. Create a production build

```bash
npm run build
npm run start
```

---

## Demo Access

The sign-in screen provides one-click demo access for the available roles:

| Role | Demo account |
| --- | --- |
| Admin | `admin@luminahealth.org` |
| Manager | `elena@luminahealth.org` |
| Reviewer | `julian@luminahealth.org` |
| Creator | `maya@luminahealth.org` |

Choose the corresponding demo option on the sign-in screen. These are demo identities included in the project; do not use them for real or confidential data.

You can also create an organisation with an Admin account and invite other roles using the organisation key flow.

---

## API Routes

The application includes the following Next.js API routes:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `POST` | `/api/review` | Analyse text content using the AI review service |
| `POST` | `/api/review-image` | Analyse an image against brand guidelines |
| `POST` | `/api/extract-docx` | Extract raw text from an uploaded DOCX file |
| `POST` | `/api/upload` | Upload an asset through Cloudinary |
| `POST` | `/api/notify` | Send a workflow email notification |

### Example: Review text

```bash
curl -X POST http://localhost:3000/api/review \
  -H "Content-Type: application/json" \
  -d '{
    "content": "Your content to review goes here.",
    "format": "text",
    "channel": "Website"
  }'
```

The review endpoint accepts `content` and can also receive `guidelines`, `format`, `channel`, and an optional `apiKey`. If guidelines are omitted, the route uses the application's default brand guidelines.

---

## Project Structure

```text
kishan-p-code-vibecheck-ai-kishan-/
├── feature list.txt
├── how to run.md
├── package.json
├── .env.example
├── tailwind.config.js
├── tsconfig.json
├── src/
│   ├── app/
│   │   ├── globals.css
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   └── api/
│   │       ├── extract-docx/route.ts
│   │       ├── notify/route.ts
│   │       ├── review/route.ts
│   │       ├── review-image/route.ts
│   │       └── upload/route.ts
│   ├── components/
│   │   ├── AnalyticsInsights.tsx
│   │   ├── AssetLibrary.tsx
│   │   ├── AuditLogs.tsx
│   │   ├── AuthScreen.tsx
│   │   ├── BrandGuidelinesBuilder.tsx
│   │   ├── DiffViewer.tsx
│   │   ├── DocumentEditor.tsx
│   │   ├── LandingPage.tsx
│   │   ├── Navbar.tsx
│   │   ├── ReviewEngine.tsx
│   │   ├── RoleDashboard.tsx
│   │   ├── SettingsModal.tsx
│   │   ├── Sidebar.tsx
│   │   └── SubmissionQueue.tsx
│   └── lib/
│       ├── accessibility-cv.ts
│       ├── cloudinary.ts
│       ├── default-data.ts
│       ├── image-analysis.ts
│       ├── openrouter.ts
│       ├── resend.ts
│       └── types.ts
└── README.md
```

---

## Design Direction

The interface uses a sandstone-inspired neutral palette with warm beige surfaces, dark ink text, and restrained accent colours. Tailwind theme tokens are configured in `tailwind.config.js`.

## Important Notes

- AI findings are intended to assist review and should be checked by a human before publication.
- Demo accounts and sample dashboard data are for demonstration only.
- The current main page persists its client-side organisation, account, and session state in browser `localStorage`. This is not a substitute for production-grade authentication or a shared database.
- Configure and verify each external integration before relying on it in production.
- Never commit API keys, secrets, private brand documents, or real customer content.

## Roadmap Ideas

Potential future extensions described in the product requirements include:
- Deeper organisation-level persistence and access controls.
- More comprehensive visual and accessibility checks.
- CMS, collaboration, and design-tool integrations.
- Brand-voice training using approved content.
- Localisation and regional compliance support.

These are roadmap ideas and should not be interpreted as completed features unless implemented in the codebase.

---

## Contributing

Contributions, bug reports, and feature suggestions are welcome.

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature`.
3. Commit your changes: `git commit -m "Add your feature"`.
4. Push the branch: `git push origin feature/your-feature`.
5. Open a Pull Request.

## License

No license file was included in the provided project structure. Add a `LICENSE` file before distributing or reusing this project under an open-source license.
