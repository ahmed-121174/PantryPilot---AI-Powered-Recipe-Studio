# PantryPilot - AI-Powered Recipe Studio

PantryPilot is an AI-powered recipe web application that helps users turn the ingredients they have into meal ideas. Choose ingredients and dietary preferences to generate recipes, explore AI-created food images, listen to recipe narration, and ask questions about individual recipes.

The application is built with Next.js, React, TypeScript, MongoDB, and OpenAI services. It also includes Google authentication and tools for discovering and managing recipes.

## Features

- **AI recipe generation** — create recipes from selected ingredients and dietary preferences.
- **AI-generated recipe images** — generate a visual for each recipe using OpenAI image generation.
- **Recipe narration** — listen to generated recipe narration with text-to-speech.
- **Recipe chat assistant** — ask follow-up questions about a recipe, such as ingredient substitutions or preparation details.
- **Ingredient validation and recipe tags** — validate custom ingredients and automatically tag generated recipes.
- **Google sign-in** — authenticate users with Google OAuth through NextAuth.js.
- **Recipe discovery** — search using recipe tags, browse popular tags, and sort by newest or most popular.
- **Recipe interactions** — like, save, and share recipes, with activity notifications.
- **Responsive interface** — use the application on desktop and mobile-sized screens.

## Technology Stack

| Area | Technologies |
| --- | --- |
| Frontend | Next.js 14, React 18, TypeScript, Tailwind CSS |
| Backend / API | Next.js API routes, Node.js |
| Database | MongoDB, Mongoose, MongoDB Adapter |
| Authentication | NextAuth.js, Google OAuth |
| AI | OpenAI API (GPT-4o, DALL·E 3, and TTS-1 in the current implementation) |
| Cloud storage | AWS S3 |
| Unit and component testing | Jest, React Testing Library |
| End-to-end testing | Cypress |
| Local database option | Docker Compose |
| Deployment configuration | Vercel |

## Getting Started

### Prerequisites

Install the following before running the project:

- Node.js 18.17 or later (Node.js 20 LTS is recommended)
- npm
- Git
- A MongoDB database (MongoDB Atlas or the included local Docker setup)
- An OpenAI API key
- Google OAuth credentials
- AWS credentials and an S3 bucket for the application's cloud-storage features
- Docker Desktop, only if you want to run MongoDB with Docker Compose

### 1. Clone the repository

```bash
git clone https://github.com/ahmed-121174/nexium-final-project.git
cd nexium-final-project
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a file named `.env.local` in the project root. Add your own values for the variables below:

```env
# Application URLs
NEXT_PUBLIC_API_BASE_URL=http://localhost:3000
NEXTAUTH_URL=http://localhost:3000

# NextAuth session secret (use a long, random value)
NEXTAUTH_SECRET=replace_with_a_secure_random_secret

# Google OAuth credentials
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

# OpenAI API
OPENAI_API_KEY=your_openai_api_key

# AWS S3 credentials and bucket
AWS_ACCESS_KEY_ID=your_aws_access_key_id
AWS_SECRET_ACCESS_KEY=your_aws_secret_access_key
S3_BUCKET_NAME=your_s3_bucket_name

# Application request limit
API_REQUEST_LIMIT=1000

# MongoDB connection string
MONGO_URI=your_mongodb_connection_string
```

**Important:** Do not commit `.env.local` or put real credentials in source control. Keep the file local and use a separate `.env.example` containing placeholder values if you want to document the required settings. The repository currently contains a tracked `.env.local` file; remove it from Git tracking with `git rm --cached .env.local` and commit that change. If any real API keys, passwords, or cloud credentials have ever been pushed, revoke or rotate them.

#### Where to obtain the credentials

- **OpenAI:** Create an API key in your OpenAI account.
- **Google OAuth:** Create OAuth 2.0 credentials in Google Cloud Console. Add `http://localhost:3000/api/auth/callback/google` as an authorized redirect URI for local development.
- **MongoDB:** Use a MongoDB Atlas connection string, or start the local MongoDB service described below.
- **AWS S3:** Create an S3 bucket and an IAM identity with only the permissions the application requires. Use the bucket name in `S3_BUCKET_NAME`.
- **NextAuth secret:** Generate a long, random secret. Do not reuse a password or publish this value.

### 4. Start MongoDB locally (optional)

The repository includes a `docker-compose.yml` that starts MongoDB and maps container port `27017` to host port `27018`.

```bash
docker compose up -d
```

For the current local Compose configuration, the connection string is:

```env
MONGO_URI=mongodb://root:123456@localhost:27018/?authSource=admin
```

The Compose file currently uses a simple development password. Change it before using this setup outside a private local development environment, and keep the Compose credentials consistent with `MONGO_URI`.

To stop the database container:

```bash
docker compose down
```

You can use MongoDB Atlas instead; in that case, put your Atlas connection string in `MONGO_URI` and skip the Docker step.

### 5. Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## How to Use

1. Open the application and sign in with your Google account.
2. Select ingredients that you have available. You can also enter a custom ingredient where supported.
3. Choose the dietary preferences that should guide the recipe suggestions.
4. Generate recipes and review the ingredients and preparation instructions.
5. View the generated recipe images or play the audio narration.
6. Use the recipe chat assistant to ask recipe-specific follow-up questions.
7. Browse recipes, search with tags, and sort the feed by popularity or recency.
8. Like, save, or share recipes to help manage your favourites.

## Available npm Scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Start the Next.js development server. |
| `npm run build` | Create an optimized production build. |
| `npm start` | Run the production server after building. |
| `npm run lint` | Run the Next.js lint command. |
| `npm run compileTS` | Check TypeScript in the application and Cypress project. |
| `npm test` | Run Jest in watch mode. |
| `npm run all_tests` | Run the Jest test suite once in test mode. |
| `npm run coverage` | Run Jest and generate a coverage report. |
| `npm run cy:run` | Run Cypress end-to-end tests in the terminal. |
| `npm run test:e2e` | Start the development server and then run Cypress tests. |
| `npx cypress open` | Open the Cypress interactive test runner. |

Some tests may require the environment variables and services described above. Configure those before running integration or end-to-end tests.

## Project Structure

```text
nexium-final-project/
├── .github/              # GitHub workflows
├── cypress/              # Cypress end-to-end tests and configuration
├── public/               # Static assets
├── src/
│   ├── components/       # Reusable React components
│   ├── lib/              # Database, API, and AI service helpers
│   ├── models/           # MongoDB/Mongoose models
│   ├── pages/             # Next.js pages and API routes
│   ├── types/             # Shared TypeScript types
│   └── ...                # Other application modules
├── tests/                 # Jest tests
├── docker-compose.yml     # Local MongoDB service
├── cypress.config.ts      # Cypress configuration
├── jest.config.ts         # Jest configuration
├── next.config.mjs        # Next.js configuration
├── package.json           # Dependencies and npm scripts
├── tailwind.config.ts     # Tailwind CSS configuration
└── tsconfig.json          # TypeScript configuration
```

## Production Build and Deployment

To create and test a production build locally:

```bash
npm run build
npm start
```

The repository includes Vercel configuration, so it can be deployed through Vercel:

1. Import the GitHub repository into Vercel.
2. Add the required environment variables in the Vercel project settings. Use production database, OpenAI, Google OAuth, and AWS S3 credentials rather than local development values.
3. Make sure the production MongoDB database accepts connections from the deployment environment.
4. Add your production domain to the Google OAuth authorized redirect URIs, using `https://YOUR_DOMAIN/api/auth/callback/google`.
5. Set `NEXTAUTH_URL` to the production application URL and deploy.

Do not place secrets in client-side variables prefixed with `NEXT_PUBLIC_`. Only non-sensitive values should use that prefix.

## Troubleshooting

- **MongoDB connection fails:** Check `MONGO_URI`, confirm the database is running, and verify the username, password, database permissions, and network access rules.
- **Google sign-in fails:** Confirm the client ID and secret, and make sure the OAuth redirect URI exactly matches the local or production callback URL.
- **Recipe or image generation fails:** Check `OPENAI_API_KEY`, API access, account billing, and usage limits.
- **S3 upload or media access fails:** Verify the bucket name, AWS credentials, bucket region, and IAM permissions.
- **The application cannot start:** Confirm the required environment variables are present, then reinstall dependencies with `npm install` if necessary.
- **Tests fail:** Check that the relevant environment variables and dependent services are configured before running the test suite.

## Security and Responsible Use

- Never publish API keys, OAuth secrets, database credentials, or AWS credentials.
- Use least-privilege IAM permissions for AWS resources.
- Use a strong MongoDB password and restrict database network access.
- Keep development credentials separate from production credentials.
- AI-generated recipes are suggestions. Review ingredient information and cooking instructions, especially when allergies, food safety, or dietary restrictions are involved.

## Contributing

Contributions, bug reports, and suggestions are welcome. For significant changes, open an issue first to discuss the proposed update. When submitting a pull request, include a clear description of the change and relevant test results.

## Acknowledgements

- [Next.js](https://nextjs.org/)
- [React](https://react.dev/)
- [MongoDB](https://www.mongodb.com/)
- [OpenAI](https://openai.com/)
- [NextAuth.js](https://next-auth.js.org/)
- [Vercel](https://vercel.com/)

---
