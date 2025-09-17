# CulinAry 🍳

A modern, AI-powered recipe management and nutrition tracking platform built with Swift for iOs

## Features

### 🤖 AI-Powered Recipe Generation
- **Dual-model AI system**: OpenRouter API integration
  - Primary: `openai/gpt-oss-20b:free` model
  - Fallback: `deepseek/deepseek-chat-v3.1:free` model
- **Google Nano Banana** image generation integration (https://ai.google.dev/gemini-api/docs/image-generation)
- **Smart Recipe Suggestions**: Based on ingredients and preferences
- **Beverages & Cocktails**: Specialized AI prompts for drinks, cocktails, smoothies, and juices
- **Advanced Mixing Techniques**: Glassware recommendations, and garnish suggestions
- **Alcohol Content Considerations**: Proper temperature guidelines
- **Tier-Based Beverage Access**:
  - Free tier: Basic non-alcoholic beverages (5 recipes/month)
  - Pro tier: Advanced cocktails, wine pairings (unlimited with daily limits)
- **Content Safety & Security**:
  - Pre-AI prompt validation prevents harmful or abusive content
  - Food/beverage relevance checking blocks non-culinary requests
  - Multi-language content filtering (English/Indonesian)
  - Local validation before AI processing saves costs and ensures safety
  - **Real-time Web Worker Validation**: Non-blocking client-side content safety checks
  - **Background Content Moderation**: Automated batch processing for community content
- **Rate Limiting & Abuse Prevention**:
  - Free: 5 recipes/month total
  - Pro: 50 recipes/day, 10/hour, 20 images/day, 30 PDFs/day
  - **Automated Usage Tracking**: Background workers for monthly resets and cleanup
  - **Real-time Limit Enforcement**: Distributed rate limiting with Redis caching
- **Comprehensive Error Handling**: Fallback mechanisms
- **Technical Implementation**: Complete AI integration details in [TIER_AND_FEATURES_PLAN.md](./TIER_AND_FEATURES_PLAN.md)

### 👨‍🍳 Recipe Management
- **Create, Edit, and Organize**: Recipe management
- **Public/Private Visibility**: Recipe sharing controls
- **Recipe Favorites**: Likes system
- **Advanced Search**: Filtering capabilities
- **Recipe Categories**: Difficulty levels
- **Nutritional Information**: Tracking system
- **Smart Meal Planning** (Pro tier): AI-generated weekly meal plans
- **Recipe Image Generation** (Pro tier): AI-generated recipe photos with batch processing
- **PDF Export** (Pro tier): Professional recipe formatting with background generation
- **Offline Recipe Access**: PWA capabilities with service worker caching
- **Background Sync**: Automatic data synchronization when connection resumes

### 📊 Nutrition Tracking
- **AI-Powered Photo Analysis**: Food logging capabilities
- **Manual Nutrition Entry**: Comprehensive database
- **Daily and Weekly Summaries**: Nutrition tracking
- **Personalized Nutrition Goals**: Custom targets
- **Macro and Micronutrient Tracking**: Complete analysis

### 👥 Social Features
- **User Profiles**: Bio and avatar customization
- **Follow/Unfollow System**: Social connections
- **Recipe Comments**: Discussions and interactions
- **Social Activity Feed**: Community updates
- **Popular Users Discovery**: Community engagement

### 🔐 Authentication & Authorization
- **JWT-Based Authentication**: Secure cookies
- **Role-Based Access Control**: User/Admin system
- **Enhanced Tier System**: Free/Pro with beverage-specific feature gating
- **Advanced Rate Limiting**: Daily/hourly caps (50 recipes/day, 10/hour for Pro)
- **Detailed Usage Limits**: Pro tier includes 20 images/day, 30 PDFs/day
- **Abuse Prevention**: IP-based monitoring, Redis caching, fair usage policies
- **Session Management**: Security protocols
- **Implementation Details**: See [TIER_AND_FEATURES_PLAN.md](./TIER_AND_FEATURES_PLAN.md) for complete technical specifications

### ⚙️ Admin Management
- **Comprehensive Admin Dashboard**: Management interface
- **User and Recipe CRUD**: Complete operations
- **Bulk Operations Support**: Efficiency tools
- **Analytics and Statistics**: Data insights
- **Content Moderation Tools**: Quality control
- **Worker Management Dashboard**: Real-time monitoring of background jobs
- **Queue Health Monitoring**: Performance metrics and error tracking
- **Automated System Maintenance**: Self-healing background processes

### 📱 Progressive Web App (PWA)
- **Offline Recipe Viewing**: Full recipe access without internet connection
- **Background Synchronization**: Automatic sync when connection resumes
- **Push Notifications**: Meal reminders and cooking timers
- **App-like Experience**: Install on mobile devices and desktop
- **Optimized Caching**: Smart caching strategies for better performance
- **Real-time Updates**: Live content updates with service worker coordination

## Tech Stack

### Frontend
- **Next.js 15** - React framework with App Router
- **React 19** - Latest React with concurrent features
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first styling
- **ShadCN/UI** - Modern component library

### Backend
- **Bun** - Primary runtime and package manager
- **Drizzle ORM** - Type-safe database operations
- **PostgreSQL** - Primary database
- **JWT with Jose** - Authentication tokens
- **Argon2** - Password hashing (security best practice)
- **SWR** - Global state management and data fetching

### Background Processing & Workers
- **Node.js Worker Threads** - Background job queue with Bun runtime
- **Web Workers** - Client-side non-blocking operations (content validation, image processing)
- **Service Workers** - PWA capabilities, offline caching, push notifications
- **Redis Queue System** - Distributed job processing and rate limiting
- **Automated Maintenance** - Monthly usage resets, data cleanup, notifications

### Payments & Subscriptions
- **Lemon Squeezy** - Payment processing and subscription management
- **Subscription Options**:
  - Pro Monthly: $9.99/month
  - Pro Yearly: Available with discount
- **Payment Integration**: Complete implementation in [TIER_AND_FEATURES_PLAN.md](./TIER_AND_FEATURES_PLAN.md)

### AI & External Services
- **openai/gpt-oss-20b:free** - Primary AI model using openrouter.ai
- **deepseek/deepseek-chat-v3.1:free** - Fallback AI model using openrouter.ai
- **Google Nano Banana** - Image generation
- **Food Database APIs** - Nutrition data

### Additional Libraries
- **SWR** - Data fetching and global state management
- **React Hook Form** with **Zod validation** - Form handling
- **CKEditor 5** - Rich text editor (planned)
- **React Dropzone** - File upload (planned)
- **Sonner** - Toast notifications
- **Lucide React** - Icons

## Project Structure

```
├── app/                      # Next.js App Router
│   ├── adm/                 # Admin area (protected)
│   ├── api/                 # API routes
│   ├── auth/                # User authentication
│   ├── d/                   # User dashboard (protected)
│   └── globals.css          # Global styles
├── components/
│   ├── context/            # React Context providers
│   ├── forms/              # Reusable form components
│   ├── hooks/              # Custom hooks
│   └── ui/                 # Shadcn/UI components
├── db/                     # Database layer
├── docs/                   # Technical documentation
└── lib/                    # Utility functions
    ├── validation/         # Zod schemas
    ├── jwt.ts              # JWT utilities
    ├── cookie.ts           # Cookie management
    ├── response.ts         # API response helpers
    └── handle-api-err.ts   # Error handling
```

## Getting Started

### Prerequisites
- **Bun** (JavaScript runtime and package manager) - **REQUIRED**
- **PostgreSQL Database**: Primary data storage
- **OpenAI API Key**: Required for AI features
- **DeepSeek API Key**: Optional fallback model
- **Google Nano Banana API Key**: Optional for image generation

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd CulinAIry
   ```

2. **Install dependencies**
   ```bash
   # ✅ ALWAYS use Bun - this project requires Bun
   bun install
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env.local
   ```

   Configure the following variables:
   ```env
   # Database
   DATABASE_URL="postgresql://username:password@localhost:5432/culinairy"

   # Authentication (Dual JWT secrets as per CLAUDE.md)
   JWT_SECRET="your-super-secret-jwt-key"
   ADM_JWT_SECRET="your-admin-secret-key"

   # AI Services
   OPENAI_API_KEY="your-openai-api-key"
   DEEPSEEK_API_KEY="your-deepseek-api-key"
   GOOGLE_NANO_BANANA_API_KEY="your-google-api-key"

   # External APIs
   NUTRITION_API_KEY="your-nutrition-api-key"

   # Payment Processing
   LEMONSQUEEZY_API_KEY="your-lemonsqueezy-api-key"
   LEMONSQUEEZY_STORE_ID="your-store-id"
   LEMONSQUEEZY_WEBHOOK_SECRET="your-webhook-secret"
   LEMONSQUEEZY_VARIANT_ID_PRO_MONTHLY="your-monthly-variant-id"
   LEMONSQUEEZY_VARIANT_ID_PRO_YEARLY="your-yearly-variant-id"
   ```

4. **Set up the database**
   ```bash
   # ✅ ALWAYS use Bun commands
   bun run db:migrate
   bun run db:seed
   ```

5. **Start the development server**
   ```bash
   # ✅ ALWAYS use Bun - this project requires Bun
   bun dev
   ```

   Open [http://localhost:3000](http://localhost:3000) in your browser.

## Database Schema

**Database Technology**: PostgreSQL with Drizzle ORM (following RULES.md conventions)

### Schema Patterns (RULES.md Compliance)
- **Table Naming**: `camelCase` + `Table` suffix (e.g., `usersTable`)
- **Column Naming**: `camelCase`
- **Foreign Keys**: `snake_case` + `_id` suffix (e.g., `user_id`)
- **Primary Keys**: `integer().primaryKey().generatedAlwaysAsIdentity()`
- **Timestamps**: `createdAt`, `updatedAt`
- **Boolean Fields**: `is` prefix (e.g., `isActive`)

### Main Tables
- **usersTable** - User accounts and profiles
- **subscriptionsTable** - User subscription management
- **categoriesTable** - Recipe categories
- **recipesTable** - Recipe data and metadata
- **recipeFavoritesTable** - User recipe favorites
- **recipeLikesTable** - Recipe like system
- **recipeCommentsTable** - Recipe comments and discussions
- **userFollowsTable** - User follow relationships
- **nutritionEntriesTable** - Nutrition tracking data
- **notificationsTable** - User notifications
- **recipeRemindersTable** - Recipe cooking reminders
- **aiGenerationLogsTable** - AI usage tracking
- **rateLimitCacheTable** - Rate limiting and abuse prevention
- **userUsageTable** - Enhanced usage tracking with IP and user agent data

### Example Schema (Drizzle ORM)
```typescript
// Following RULES.md patterns
export const usersTable = pgTable('users', {
  id: integer().primaryKey().generatedAlwaysAsIdentity(),
  email: varchar({ length: 255 }).unique().notNull(),
  tier: varchar({ length: 10 }).default('free').notNull(),
  isActive: boolean().default(true).notNull(),
  createdAt: timestamp().defaultNow().notNull(),
  updatedAt: timestamp().defaultNow().notNull(),
});

export const userUsageTable = pgTable('user_usage', {
  id: integer().primaryKey().generatedAlwaysAsIdentity(),
  userId: integer().references(() => usersTable.id, { onDelete: 'cascade' }).notNull(),
  featureType: varchar({ length: 50 }).notNull(),
  createdAt: timestamp().defaultNow().notNull(),
  updatedAt: timestamp().defaultNow().notNull(),
});
```

**Migration Commands**:
```bash
bun run db:migrate   # Run migrations
bun run db:studio    # Launch Drizzle Studio
```

## API Architecture

### Core Modules

#### Authentication (`/lib/auth/`)
- **JWT Token Management**: Authentication tokens
- **Cookie-Based Sessions**: Secure session handling
- **Role and Tier Verification**: Access control
- **Password Hashing and Validation**: Security protocols

#### AI Integration (`/lib/ai/`)
- **Recipe Generation**: Multiple AI models (food and beverages)
- **Specialized Beverage Generation**: Cocktails, wine pairings, mixing techniques
- **Image Generation**: For recipes
- **Content Safety Validation**: Pre-AI prompt filtering for security and relevance
- **Prompt Abuse Prevention**: Local validation before AI processing to block harmful content
- **Food/Beverage Relevance Checking**: Ensures prompts are strictly food/drink related
- **Multi-language Safety**: English and Indonesian content filtering
- **Tier-Based Access Control**: Feature gating for advanced beverage recipes
- **Advanced Rate Limiting**: Daily/hourly caps with Redis caching
- **Abuse Prevention**: IP monitoring, usage analytics, fair usage enforcement
- **Fallback Mechanisms**: Comprehensive error handling
- **Complete Implementation Guide**: [TIER_AND_FEATURES_PLAN.md](./TIER_AND_FEATURES_PLAN.md) Phase 4

#### Recipe Management (`/lib/recipes/`)
- **CRUD Operations**: Recipe management
- **Search and Filtering**: Discovery features
- **Favorites and Likes**: User interactions
- **Visibility Controls**: Public/private settings

#### Nutrition Tracking (`/lib/nutrition/`)
- **Food Logging**: AI photo analysis
- **Manual Nutrition Entry**: Comprehensive tracking
- **Goal Setting**: Progress tracking
- **Daily/Weekly Summaries**: Nutrition insights

#### Social Features (`/lib/social/`)
- **User Profiles**: Relationships management
- **Follow/Unfollow System**: Social connections
- **Comments and Interactions**: Social engagement
- **Activity Feeds**: Community updates

#### Admin Management (`/lib/admin/`)
- **User and Content Moderation**: Quality control
- **Analytics and Reporting**: Data insights
- **Bulk Operations**: Efficiency tools
- **System Administration**: Platform management

## Development Guidelines

### Styling Guidelines

#### CSS Variables vs Utility Classes
**REQUIRED**: Always use ShadCN CSS variables instead of Tailwind utility classes for theming.

##### ✅ Correct Usage (CSS Variables)
```tsx
// Use ShadCN CSS variables
<div className="bg-background text-foreground" />
<div className="bg-muted text-muted-foreground" />
<div className="bg-primary text-primary-foreground" />
<div className="hover:bg-muted/50" />
<div className="bg-card text-card-foreground" />
```

##### ❌ Incorrect Usage (Utility Classes)
```tsx
// DO NOT use Tailwind utility classes with dark mode variants
<div className="bg-gray-100 dark:bg-gray-800 text-gray-900 dark:text-gray-100" />
<div className="bg-zinc-50 dark:bg-zinc-900" />
<div className="hover:bg-gray-50 dark:hover:bg-gray-800" />
```

##### Available ShadCN CSS Variables
- `bg-background` / `text-foreground` - Main background and text
- `bg-card` / `text-card-foreground` - Card backgrounds
- `bg-muted` / `text-muted-foreground` - Muted/secondary content
- `bg-primary` / `text-primary-foreground` - Primary actions
- `bg-secondary` / `text-secondary-foreground` - Secondary actions
- `bg-accent` / `text-accent-foreground` - Accent elements
- `border-border` - Border colors
- `bg-destructive` / `text-destructive-foreground` - Error states

##### Benefits
1. **Automatic theme support** - No need for `dark:` variants
2. **Consistent theming** - All components use the same color system
3. **Easy customization** - Change themes by updating CSS variables
4. **Better maintainability** - Single source of truth for colors

### API Development Rules

#### API Route Pattern
```tsx
export async function POST(req: NextRequest) {
  // 1. Check authentication
  const [user, error] = await getLogin();
  if (error) return error;

  // 2. Validate request body
  const { data, errors } = await reqValidateBody(req, schema);
  if (errors) return toRes({ status: 400, errors });

  try {
    // 3. Business logic
    const result = await processData(data);

    // 4. Return success response
    return toRes({ data: result, msg: 'Success' });
  } catch (error) {
    return toRes({ status: 500, msg: 'Internal server error' });
  }
}
```

#### Response Format (toRes Function)
```tsx
// Success with data
return toRes({ data: result, msg: 'Success' });

// Simple success
return toRes({ msg: 'ok' });

// Validation Error
return toRes({ status: 400, errors: { field: 'Error message' } });

// Not Found
return toRes({ status: 404, msg: 'Resource not found' });

// Unauthorized (automatic)
return toRes({ status: 401, msg: 'Unauthorized' });
```

### API Call Rules (CLAUDE.md Compliance)

#### Core API Patterns
**IMPORTANT**: Never use `/api` prefix when calling APIs with `useApi()` or `useSWR()`:

```tsx
// ✅ CORRECT - No /api prefix (SWRConfig handles this)
const api = useApi();
await api.get('/auth/login');
await api.post('/users', data);
const { data } = useSWR('/auth/me');

// ❌ INCORRECT - Don't use /api prefix
await api.get('/api/auth/login');    // DON'T DO THIS
const { data } = useSWR('/api/auth/me');  // DON'T DO THIS
```

#### SWR Configuration Rules
**SWR Fetcher Rule**: Never pass fetcher as second parameter to `useSWR()` because it's already configured in `<SWRConfig />`:

```tsx
// ✅ CORRECT - No fetcher parameter (global config)
const { data } = useSWR('/users');
const { data } = useSWR('/auth/me');

// ❌ INCORRECT - Don't pass fetcher
const { data } = useSWR('/users', api.get);     // DON'T DO THIS
const { data } = useSWR('/users', fetcher);     // DON'T DO THIS
```

#### API Route Patterns (CLAUDE.md)
```tsx
export async function POST(req: NextRequest) {
  // 1. Check authentication
  const [user, error] = await getLogin();
  if (error) return error;

  // 2. Validate request body
  const { data, errors } = await reqValidateBody(req, schema);
  if (errors) return toRes({ status: 400, errors });

  try {
    // 3. Business logic
    const result = await processData(data);

    // 4. Return success response
    return toRes({ data: result, msg: 'Success' });
  } catch (error) {
    return toRes({ status: 500, msg: 'Internal server error' });
  }
}
```

#### Response Format (toRes Function)
```tsx
// Success with data
return toRes({ data: result, msg: 'Success' });

// Simple success
return toRes({ msg: 'ok' });

// Validation Error
return toRes({ status: 400, errors: { field: 'Error message' } });

// Not Found
return toRes({ status: 404, msg: 'Resource not found' });

// Unauthorized (automatic)
return toRes({ status: 401, msg: 'Unauthorized' });
```

### Code Style (CLAUDE.md Standards)
- **TypeScript strict mode** - Required for all code
- **Follow ESLint and Prettier** configurations
- **Use meaningful variable and function names**
- **Implement proper error handling** with tuple patterns
- **No comments unless asked** (CLAUDE.md rule)
- **Prefer Functions Over Classes**: Use function-based patterns for modern JavaScript development

### Function vs Class Guidelines
- **✅ USE Functions**: For all utilities, services, API routes, and React components
- **❌ AVOID Classes**: Unless absolutely necessary for complex state management
- **Preferred Patterns**:
  ```typescript
  // ✅ CORRECT - Function-based service
  export async function trackUsage(userId: number, type: string) {
    // implementation
  }

  // ✅ CORRECT - Named export functions for utilities
  export function calculateTierLimits(tier: UserTier) {
    // implementation
  }

  // ❌ AVOID - Class-based services
  export class UsageTracker {
    static async trackUsage() { }  // Use function instead
  }
  ```

### Database Operations (RULES.md Compliance)
- **Use Drizzle ORM** for all database interactions (no raw SQL)
- **Primary Keys**: `integer().primaryKey().generatedAlwaysAsIdentity()`
- **Timestamps**: Always add `createdAt` and `updatedAt`
- **String Fields**: Use `varchar({ length: 255 })` format
- **Security**: Separate password tables for security
- **Foreign Keys**: Use `onDelete: 'cascade'` for relationships
- **Table Names**: `camelCase` + `Table` suffix (usersTable, etc.)

### Authentication System (CLAUDE.md Patterns)
- **Dual JWT Secrets**: `JWT_SECRET` for users, `ADM_JWT_SECRET` for admins
- **Cookie Management**: HttpOnly, Secure, SameSite=Lax
- **Authentication Checks**: Use `getLogin()` tuple pattern
- **Password Hashing**: Argon2 (security best practice)

```tsx
// ✅ CORRECT Authentication Pattern
const [user, error] = await getLogin();
if (error) return error;

// ❌ INCORRECT - Don't throw errors
const user = await getLogin();  // WRONG - might throw
if (!user) throw new Error();   // WRONG
```

### Security Best Practices
- **Input Validation**: All inputs with Zod schemas
- **Content Safety Validation**: Pre-AI prompt filtering prevents harmful, abusive, or non-food content from being processed
- **Prompt Security System**: Local validation ensures only food/beverage-related requests reach AI models
- **Multi-layer Content Filtering**: Blocks prohibited keywords, dangerous patterns, and irrelevant content
- **Error Handling**: Use `handleApiErr()` utility
- **Token Refresh**: Automatic refresh on 401 errors
- **Rate Limiting**: Comprehensive abuse prevention
- **OWASP Guidelines**: Security best practices

### Form Handling (RULES.md Patterns)
- **React Hook Form** + **Zod validation**
- **ShadCN Form** components
- **Field-level error handling**

```tsx
// ✅ CORRECT Form Pattern
const form = useForm({
  resolver: zodResolver(schema),
  values: { username: data?.data?.username || '' },
});

const onSubmit = async (formData: any) => {
  try {
    await api.post('/accounts', formData);
    toast.success('Success!');
  } catch (error) {
    handleApiErr(error, { setError: form.setError });
  }
};
```

## Deployment

### Environment Setup
```bash
# 1. Database setup
bun run db:migrate
bun run db:seed

# 2. Environment variables (CLAUDE.md compliant)
DATABASE_URL="postgresql://..."
JWT_SECRET="your-jwt-secret"
ADM_JWT_SECRET="your-admin-secret"  # Dual JWT system
OPENROUTER_API_KEY="your-openrouter-key"

# 3. Production build
bun run build
bun start
```

### Production Considerations
- **Database**: Connection pooling with Drizzle
- **Monitoring**: Proper logging and error tracking
- **Rate Limiting**: Redis-based abuse prevention
- **Caching**: SWR client-side + server-side strategies
- **Security**: Argon2 password hashing, secure cookies
- **Backup**: Automated PostgreSQL backups
- **Performance**: Image optimization, code splitting

### Deployment Checklist
- [ ] Environment variables configured
- [ ] Database migrations applied
- [ ] AI services (OpenRouter, Google Nano Banana) configured
- [ ] Payment system (Lemon Squeezy) integrated
- [ ] Rate limiting and abuse prevention active
- [ ] Monitoring and alerting set up
- [ ] Backup procedures implemented

## 🤖 AI Agent Support

For AI agents working with this project, see [**CLAUDE.md**](./CLAUDE.md) for detailed development rules and conventions:

### Core Development Patterns
- **Package Manager**: Bun only (never npm/yarn/pnpm)
- **API Patterns**: NextRequest, tuple responses, toRes() format
- **Database**: Drizzle ORM with proper table naming (usersTable, etc.)
- **Authentication**: getLogin() tuple pattern, dual JWT secrets
- **Form Handling**: React Hook Form + Zod + ShadCN components
- **Error Handling**: handleApiErr() utility for consistency
- **Styling**: ShadCN CSS variables (bg-background, text-foreground)
- **File Structure**: Following CLAUDE.md conventions

### Key Rules for AI Agents
```tsx
// ✅ ALWAYS follow these patterns
const [user, error] = await getLogin();        // Authentication
return toRes({ data, msg: 'Success' });        // API responses
const { data } = useSWR('/endpoint');           // Data fetching
handleApiErr(error, { setError });             // Error handling
```

### Implementation Reference
Complete technical implementation details are available in:
- **[TIER_AND_FEATURES_PLAN.md](./TIER_AND_FEATURES_PLAN.md)** - Full development roadmap
- **[CLAUDE.md](./CLAUDE.md)** - AI agent development guidelines
- **[RULES.md](./RULES.md)** - Technical standards and conventions

## 📚 Documentation

### Technical Documentation
Technical documentation in `/docs/` folder:

- **[setup.md](./docs/setup.md)** - Project setup and installation
- **[database.md](./docs/database.md)** - Database operations with Drizzle ORM
- **[auth.md](./docs/auth.md)** - Authentication functions and patterns
- **[api.md](./docs/api.md)** - API route patterns and responses
- **[hooks.md](./docs/hooks.md)** - React hooks usage
- **[components.md](./docs/components.md)** - UI component patterns
- **[forms.md](./docs/forms.md)** - Form handling patterns

Each doc is function-focused with copy-paste ready examples.

### Implementation Plans
- **[TIER_AND_FEATURES_PLAN.md](./TIER_AND_FEATURES_PLAN.md)** - Complete tier system implementation guide
- **[AI_PROMPTS.md](./AI_PROMPTS.md)** - AI prompt specifications and guidelines

### Key Development Utilities (CLAUDE.md Patterns)

#### Core Utilities (`/lib`)
```typescript
// lib/response.ts - Standardized API responses
import { toRes } from '@/lib/response';
return toRes({ data: result, msg: 'Success' });
return toRes({ status: 400, errors: { field: 'Error message' } });

// lib/handle-api-err.ts - Consistent error handling
import { handleApiErr } from '@/lib/handle-api-err';
try {
  await api.post('/endpoint', data);
} catch (error) {
  handleApiErr(error, { setError });  // For forms
  handleApiErr(error);                // For general errors
}

// lib/cookie.ts - Authentication management
import { getLogin, getLoginAdm } from '@/lib/cookie';
const [user, error] = await getLogin();      // User auth
const [admin, error] = await getLoginAdm();  // Admin auth
```

#### Custom Hooks (`/components/hooks`)
```typescript
// hooks/useApi.tsx - HTTP client with auto token refresh
const api = useApi();
await api.get('/auth/me');     // No /api prefix needed
await api.post('/recipes', data);

// SWR usage - No fetcher parameter needed
const { data } = useSWR('/auth/me');           // Global config handles fetcher
const { data } = useSWR('/recipes');           // Automatic base path
```

#### Form Components (`/components/forms`)
```typescript
// Reusable form components with ShadCN + Zod
import { Form, FormField, FormItem, FormLabel, FormControl } from '@/components/ui/form';
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';

const form = useForm({
  resolver: zodResolver(schema),
  values: { username: data?.data?.username || '' },
});
```

## ✅ Do's and Don'ts (README.md Format)

### ✅ DO

#### Package Management
```bash
# ✅ Always use Bun (Project Requirement)
bun install
bun add package-name
bun dev
bun run build
bun run db:migrate
```

#### API Calls (CLAUDE.md Patterns)
```tsx
// ✅ No /api prefix (SWRConfig handles this)
const api = useApi();
await api.get('/auth/me');
const { data } = useSWR('/auth/me');

// ✅ Use proper error handling
try {
  await api.post('/recipes', data);
} catch (error) {
  handleApiErr(error, { setError });
}
```

#### Authentication Checks (CLAUDE.md Compliance)
```tsx
// ✅ Use tuple pattern
const [user, error] = await getLogin();
if (error) return error;

// ✅ Proper API response format
return toRes({ data: result, msg: 'Success' });
```

#### Database Operations (RULES.md Patterns)
```tsx
// ✅ Use Drizzle ORM with proper naming
const [user] = await db.select().from(usersTable)
  .where(eq(usersTable.id, 1)).limit(1);

// ✅ Proper table schema
export const usersTable = pgTable('users', {
  id: integer().primaryKey().generatedAlwaysAsIdentity(),
  createdAt: timestamp().defaultNow().notNull(),
});
```

#### Form Handling (RULES.md Standards)
```tsx
// ✅ React Hook Form + Zod validation
const form = useForm({
  resolver: zodResolver(schema),
  values: { email: data?.data?.email || '' },
});

const onSubmit = async (formData: any) => {
  try {
    await api.post('/auth/register', formData);
    toast.success('Registration successful!');
  } catch (error) {
    handleApiErr(error, { setError: form.setError });
  }
};
```

### ❌ DON'T

#### Package Management
```bash
# ❌ Never use other package managers
npm install    # DON'T USE
yarn add       # DON'T USE
pnpm install   # DON'T USE
```

#### API Calls
```tsx
// ❌ Don't add /api prefix
await api.get('/api/auth/me');           // WRONG
const { data } = useSWR('/api/users');   // WRONG

// ❌ Don't pass fetcher to useSWR (already configured)
useSWR('/users', api.get);               // WRONG
useSWR('/users', fetcher);               // WRONG

// ❌ Don't use generic Response.json
return Response.json({ data });          // WRONG
```

#### Database Operations
```tsx
// ❌ Don't write raw SQL
await db.execute('SELECT * FROM users WHERE id = ?', [1]);  // WRONG

// ❌ Don't use generic table names
export const users = pgTable('users', {});                  // WRONG
// Use: usersTable, recipesTable, etc.
```

#### Code Organization
```tsx
// ❌ Don't use classes for services and utilities
export class UsageTracker {
  static async trackUsage() { }  // WRONG
}

export class SubscriptionService {
  static async createSubscription() { }  // WRONG
}

// ✅ Use functions instead
export async function trackUsage() { }  // CORRECT
export async function createSubscription() { }  // CORRECT
```

#### Authentication
```tsx
// ❌ Don't throw errors, use tuple pattern
const user = await getLogin();  // WRONG - might throw
if (!user) throw new Error();   // WRONG

// ❌ Don't use inconsistent error formats
return Response.json({ error }, { status: 400 }); // WRONG
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes following project guidelines
4. Test with `bun run lint` and `bun run type-check`
5. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📦 Available Scripts

**IMPORTANT**: This project uses **Bun** as the primary package manager and runtime.

```bash
# Development
bun dev              # Start development server
bun run build        # Build for production
bun start            # Start production server

# Database
bun run db:migrate   # Run migrations
bun run db:studio    # Launch Drizzle Studio
bun run db:seed      # Seed database

# Code Quality
bun run lint         # Run ESLint
bun run type-check   # TypeScript check
bun test             # Run test suite

# Package Management
bun install          # Install dependencies
bun add package-name # Add new package
bun remove package   # Remove package

# ❌ NEVER use other package managers
# npm install    # DON'T USE
# yarn install   # DON'T USE
# pnpm install   # DON'T USE
```

## Support

For support and questions, please open an issue on GitHub or contact the development team.

## 🔗 Related Documentation

### Core Documentation
- **[TIER_AND_FEATURES_PLAN.md](./TIER_AND_FEATURES_PLAN.md)** - Detailed implementation plan for subscription tiers and features
- **[WORKERSPLAN.md](./workersplan.md)** - Comprehensive workers implementation strategy for background processing
- **[AI_PROMPTS.md](./AI_PROMPTS.md)** - AI prompt specifications for recipe and image generation
- **[CLAUDE.md](./CLAUDE.md)** - Development guidelines for AI agents
- **[README.md](./README.md)** - Project overview and quick start guide
- **[RULES.md](./RULES.md)** - Technical standards and conventions

### Standards Compliance Summary

This document now follows all project standards:

#### ✅ **README.md Compliance**
- Available Scripts section with Bun commands
- Do's and Don'ts with examples
- Tech stack alignment
- AI agent support reference

#### ✅ **RULES.md Compliance**
- Database schema with proper table naming
- API response format patterns
- Form handling with React Hook Form + Zod
- Authentication dual system

#### ✅ **CLAUDE.md Compliance**
- API call rules (no /api prefix)
- Authentication tuple patterns
- Error handling with handleApiErr
- TypeScript strict mode
- SWR configuration details

**Development Workflow**: Always reference [TIER_AND_FEATURES_PLAN.md](./TIER_AND_FEATURES_PLAN.md) for implementation details and [CLAUDE.md](./CLAUDE.md) for coding patterns.

---

**CulinAIry** - Where AI meets culinary creativity! 🍳✨
