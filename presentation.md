# Monetising & Distributing Software

**Turning your code into a product people can find, use, and pay for**

> From open-source libraries to SaaS platforms -- every path from code to revenue

`Build` -> `Package` -> `Distribute` -> `Monetise` -> `Scale`

---

## Table of Contents

1. [Topics](#topics)
2. [Free vs Paid Distribution](#free-vs-paid-distribution)
3. [Open Source Licensing](#open-source-licensing)
4. [Package Managers & Libraries](#package-managers--libraries)
5. [App Stores & Marketplaces](#app-stores--marketplaces)
6. [Software-as-a-Service (SaaS)](#software-as-a-service-saas)
7. [Building a SaaS -- The Tech Stack](#building-a-saas--the-tech-stack)
8. [Payment Integration](#payment-integration)
9. [Subscription Models & Pricing Psychology](#subscription-models--pricing-psychology)
10. [Licensing & License Keys](#licensing--license-keys)
11. [Desktop App Distribution](#desktop-app-distribution)
12. [API Monetisation](#api-monetisation)
13. [Marketplace & Platform Distribution](#marketplace--platform-distribution)
14. [Landing Pages & Marketing Basics](#landing-pages--marketing-basics)
15. [Analytics & Metrics That Matter](#analytics--metrics-that-matter)
16. [Legal Considerations](#legal-considerations)
17. [Scaling from Free to Paid](#scaling-from-free-to-paid)
18. [Common Mistakes Indie Developers Make](#common-mistakes-indie-developers-make)
19. [Summary & Further Reading](#summary--further-reading)

---

## Topics

### Distribution Models
- Free vs paid -- the spectrum
- Open source licensing
- Package managers & libraries
- App stores & marketplaces
- Desktop app distribution

### Monetisation Strategies
- SaaS & recurring revenue
- Payment integration (Stripe, Paddle)
- Subscription & pricing tiers
- API monetisation
- Licensing & license keys

### Building the Business
- Building a SaaS (auth, billing, multi-tenancy)
- Landing pages & marketing basics
- Analytics & metrics (MRR, churn, LTV)
- Marketplace & platform distribution

### Practical Concerns
- Legal: ToS, privacy, GDPR, tax
- Scaling from free to paid
- Common indie developer mistakes
- Summary & further reading

---

## Free vs Paid Distribution

Software distribution exists on a **spectrum** -- from fully open to fully proprietary.

`Fully Open Source` -> `Open Core` -> `Freemium` -> `Free Trial` -> `Paid Only`

### Open Source
- Code is public, anyone can use/modify
- Revenue via support, hosting, consulting
- Examples: Linux, PostgreSQL, Redis
- Builds trust and community

### Freemium / Open Core
- Core product free, premium features paid
- Most popular SaaS model today
- Examples: Slack, Notion, GitLab
- Conversion rates typically 2-5%

### Paid Only
- No free tier -- pay to access
- Higher quality signal, lower volume
- Examples: Sublime Text, JetBrains IDEs
- Works when value is clear and proven

### Key Insight

Free distribution builds **top of funnel**. Paid features capture **value**. The best businesses combine both -- give away what creates trust, charge for what creates ROI.

---

## Open Source Licensing

Your license determines how others can use, modify, and redistribute your code.

| License | Permissions | Conditions | Copyleft? | Commercial Use |
|---------|------------|------------|-----------|----------------|
| **MIT** | Use, modify, distribute | Include license text | No | Yes |
| **Apache 2.0** | Use, modify, distribute, patent grant | Include license, state changes | No | Yes |
| **GPL v3** | Use, modify, distribute | Derivatives must also be GPL | **Strong** | Yes (with conditions) |
| **AGPL v3** | Use, modify, distribute | Network use = distribution | **Strongest** | Yes (with conditions) |
| **BSL / SSPL** | Use, modify (non-production) | No competing hosted service | N/A | Restricted |

### Permissive (MIT / Apache)

Maximum adoption. Companies can use your code without legal fear. Best for libraries and tools you want widely used.

### Copyleft (GPL / AGPL)

Protects the commons. Forces derivatives to remain open. AGPL closes the "SaaS loophole" -- used by MongoDB (before SSPL), Grafana.

### Example: MIT License

```
MIT License

Copyright (c) 2026 Your Name

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software... [the standard MIT text]
```

---

## Package Managers & Libraries

The simplest way to distribute code for free: publish to a **package registry**.

| Ecosystem | Registry | CLI | Packages |
|-----------|----------|-----|----------|
| **JavaScript** | npmjs.com | `npm publish` | ~3M |
| **Python** | pypi.org | `twine upload` | ~500K |
| **Rust** | crates.io | `cargo publish` | ~150K |
| **Go** | pkg.go.dev | `go mod` | Decentralised |
| **Ruby** | rubygems.org | `gem push` | ~180K |

### Publishing Checklist
- Choose a clear, unique package name
- Semantic versioning (semver)
- Write a good README
- Include TypeScript types / type hints
- Set up CI to auto-publish on tag
- Add a LICENSE file

### Example: `package.json` for publishing an npm library

```json
{
  "name": "@yourorg/utils",
  "version": "1.2.0",
  "description": "Utility functions for data processing",
  "main": "dist/index.js",
  "types": "dist/index.d.ts",
  "files": ["dist"],
  "license": "MIT",
  "repository": { "type": "git", "url": "https://github.com/yourorg/utils" },
  "scripts": {
    "build": "tsc",
    "prepublishOnly": "npm run build"
  },
  "publishConfig": { "access": "public" }
}
```

---

## App Stores & Marketplaces

Walled gardens give you **discovery** and **trust**, but take a cut and impose rules.

| Store | Fee | Annual Cost | Review Process | Key Rules |
|-------|-----|-------------|----------------|-----------|
| **Apple App Store** | 15-30% | $99/yr | Manual, 1-7 days | Must use Apple IAP for digital goods |
| **Google Play** | 15-30% | $25 one-time | Automated + manual | Sideloading allowed on Android |
| **Steam** | 20-30% | $100/game | Steam Direct | Revenue split improves at $10M+ |
| **Chrome Web Store** | Free (5% for paid) | $5 one-time | Automated | Manifest V3 required |
| **VS Code Marketplace** | Free | Free | Automated | Open marketplace, can monetise externally |

### The 30% Problem

Apple and Google taking 30% of digital goods has driven lawsuits (Epic v. Apple) and pushed developers towards **web-based payment** flows. The EU Digital Markets Act is forcing changes.

### Alternatives to App Stores
- PWAs (Progressive Web Apps) -- no store needed
- Direct download with code signing
- Homebrew / apt repositories for CLI tools
- Sideloading on Android

---

## Software-as-a-Service (SaaS)

SaaS is the **dominant model** for monetising software. Users pay recurring fees; you host and maintain the service.

### Why SaaS Won
- **Recurring revenue** -- predictable cash flow
- No piracy -- you control access
- Continuous updates without user action
- Usage data drives product decisions
- Lower barrier to entry for users
- Easier to upsell and expand revenue

### SaaS Metrics
- **ARR** = Annual Recurring Revenue
- **MRR** = Monthly Recurring Revenue
- **Churn** = % customers lost per period
- **NRR** = Net Revenue Retention (>100% is great)

### Typical SaaS Architecture

```
Browser / App  ->  CDN / LB
                      |
                      v
               API Gateway  ->  Auth Service
                      |
                      v
               App Server(s)  ->  Database
                      |
                      v
               Billing / Stripe  ->  Email / Notifications
```

---

## Building a SaaS -- The Tech Stack

### Authentication
- **Clerk** -- drop-in auth UI
- **Auth.js** (NextAuth) -- open source
- **Supabase Auth** -- with DB
- **Firebase Auth** -- Google
- OAuth 2.0 / OIDC standard
- Magic links, passkeys, SSO

### Multi-tenancy
- **Shared DB** -- tenant_id column
- **Schema per tenant** -- isolation
- **DB per tenant** -- max isolation
- Row-Level Security (RLS) in Postgres
- Middleware to inject tenant context

### Billing
- **Stripe** -- industry standard
- **Paddle** -- merchant of record
- **LemonSqueezy** -- simpler Paddle
- Webhooks for payment events
- Subscription lifecycle management

### Modern SaaS Starter Stacks

| Stack | Components |
|-------|-----------|
| **Next.js + Vercel** | React, Prisma, Stripe, Clerk |
| **Django + Railway** | Python, Postgres, Stripe, django-allauth |
| **Rails + Fly.io** | Ruby, Postgres, Stripe, Devise |
| **Go + Hetzner** | HTMX, SQLite/Postgres, Stripe |

### Multi-tenancy with RLS

```sql
-- Postgres Row-Level Security
ALTER TABLE projects ENABLE ROW LEVEL SECURITY;

CREATE POLICY tenant_isolation ON projects
  USING (tenant_id = current_setting('app.tenant_id')::uuid);

-- Set in middleware before each request
SET app.tenant_id = 'abc-123-def';
```

---

## Payment Integration

### Stripe
- Payment processor -- you are merchant
- You handle tax, invoicing, compliance
- 2.9% + 30c per transaction
- Best API, most flexibility
- Stripe Tax, Billing, Connect

### Paddle / LemonSqueezy
- **Merchant of Record** (MoR)
- They handle tax, VAT, invoicing
- 5% + 50c per transaction
- Simpler -- ideal for solo devs
- They are the seller, you are the vendor

### When to Use Which
- **Stripe**: full control, scale, complex billing
- **Paddle**: don't want to deal with tax
- **Gumroad**: one-off digital products
- MoR simplifies global sales tax enormously

### Stripe Checkout -- create a payment session in ~20 lines

```javascript
// Server: Create Stripe Checkout session
import Stripe from 'stripe';
const stripe = new Stripe(process.env.STRIPE_SECRET_KEY);

app.post('/api/checkout', async (req, res) => {
  const session = await stripe.checkout.sessions.create({
    mode: 'subscription',
    line_items: [{
      price: 'price_1234abc',  // from Stripe dashboard
      quantity: 1,
    }],
    success_url: 'https://app.example.com/success',
    cancel_url: 'https://app.example.com/pricing',
    customer_email: req.user.email,
  });
  res.json({ url: session.url });
});
```

```javascript
// Server: Handle Stripe webhooks
app.post('/webhooks/stripe', async (req, res) => {
  const event = stripe.webhooks.constructEvent(
    req.body,
    req.headers['stripe-signature'],
    process.env.STRIPE_WEBHOOK_SECRET
  );

  switch (event.type) {
    case 'checkout.session.completed':
      await activateSubscription(event.data.object);
      break;
    case 'invoice.payment_failed':
      await handleFailedPayment(event.data.object);
      break;
    case 'customer.subscription.deleted':
      await deactivateSubscription(event.data.object);
      break;
  }
  res.json({ received: true });
});
```

---

## Subscription Models & Pricing Psychology

| Tier | Price | Target | Purpose |
|------|-------|--------|---------|
| **Free** | $0 | Everyone | Top of funnel, virality |
| **Individual** | $9-29/mo | Prosumers | Core revenue |
| **Team** | $15-49/seat/mo | Small teams | Expansion revenue |
| **Enterprise** | Custom | Large orgs | High ACV, SSO, SLAs |

### Pricing Psychology
- **Anchor high** -- show enterprise first, then mid-tier feels cheap
- **3-tier rule** -- most people pick the middle
- **Annual discount** -- offer 2 months free (17% off)
- **Price on value**, not cost -- if you save them $10K, charge $1K
- **Avoid $0** for B2B -- free plans attract the wrong users

### The Free Tier Trap

Free users cost you money (hosting, support) but rarely convert. Limit free tiers carefully:

- Rate limits (100 API calls/day)
- Storage caps (500MB)
- Team size limits (up to 3 members)
- Remove branding only on paid plans
- Data retention limits (30 days)

### Usage-Based vs Seat-Based
- **Seat-based**: predictable, easy to understand (Slack, Jira)
- **Usage-based**: aligns cost with value (AWS, Twilio, OpenAI)
- **Hybrid**: base fee + usage (Vercel, PlanetScale)
- Usage-based has higher NRR but harder forecasting

---

## Licensing & License Keys

For desktop software, CLI tools, and self-hosted products, **license keys** gate access without requiring a full SaaS backend.

### How License Keys Work

`Purchase` -> `Generate Key` -> `Validate`

- **Offline**: cryptographically signed tokens (JWT-like)
- **Online**: phone-home to licensing server
- **Hybrid**: validate online, cache locally, periodic re-check

### Licensing Platforms

| Platform | Model | Best For |
|----------|-------|----------|
| **Keygen** | API-first licensing | Developer tools |
| **Gumroad** | Simple digital sales | Indie products |
| **LicenseSpring** | Enterprise licensing | B2B desktop software |
| **Polar.sh** | OSS monetisation | Open-source maintainers |

### Example: Keygen License Validation

```javascript
// Validate a license key against Keygen API
async function validateLicense(key) {
  const res = await fetch(
    `https://api.keygen.sh/v1/accounts/${ACCOUNT_ID}/licenses/actions/validate-key`,
    {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        meta: { key },
      }),
    }
  );
  const { meta, data } = await res.json();

  if (meta.valid) {
    console.log('License valid:', data.attributes.name);
    return { valid: true, expiry: data.attributes.expiry };
  } else {
    console.error('Invalid:', meta.code);
    return { valid: false, reason: meta.code };
  }
}

// On app startup
const license = await validateLicense(storedKey);
if (!license.valid) showUpgradeModal();
```

---

## Desktop App Distribution

| Framework | Language | Bundle Size | Trade-offs |
|-----------|----------|-------------|------------|
| **Electron** | JS/TS | ~150MB+ | Mature, heavy, Chromium |
| **Tauri** | Rust + JS/TS | ~5-10MB | Lightweight, native webview |
| **Flutter Desktop** | Dart | ~20MB | Cross-platform, growing |
| **Qt / GTK** | C++ / Python | ~30MB | Native feel, complex build |

### Code Signing
- **macOS**: Apple Developer ID + notarisation ($99/yr)
- **Windows**: EV Code Signing Certificate (~$300-500/yr)
- **Linux**: GPG signing for packages
- Without signing: "unidentified developer" warnings = low install rate

### Auto-updates
- **electron-updater** -- auto-update via GitHub Releases
- **Tauri updater** -- built-in, lightweight
- **Sparkle** (macOS) / **WinSparkle** (Windows)
- Delta updates to reduce download size

### Distribution Channels

`Build` -> `Sign` -> `Notarise` -> `Distribute`

- Direct download from your website
- Homebrew Cask (macOS)
- Windows Package Manager (winget)
- Snap Store / Flatpak (Linux)
- Mac App Store (sandboxed)

---

## API Monetisation

APIs are **products**. Usage-based pricing aligns cost with value and scales naturally.

### API Pricing Models

| Model | Example |
|-------|---------|
| **Pay-per-call** | $0.001 per request (Twilio) |
| **Tiered quotas** | 1K free, 10K = $29/mo (Algolia) |
| **Compute-based** | $0.01 per token (OpenAI) |
| **Flat + overage** | $49/mo + $0.01/extra call |

### Developer Portal Essentials
- API key management & rotation
- Interactive docs (Swagger / Redoc)
- SDKs in popular languages
- Usage dashboard & billing
- Rate limit headers in responses

### Rate Limiting Middleware (Express.js)

```javascript
import rateLimit from 'express-rate-limit';
import RedisStore from 'rate-limit-redis';
import { Redis } from 'ioredis';

const redis = new Redis(process.env.REDIS_URL);

// Per-API-key rate limiting
const apiLimiter = rateLimit({
  store: new RedisStore({ sendCommand: (...args) =>
    redis.call(...args) }),
  windowMs: 60 * 1000,    // 1 minute
  max: (req) => {
    // Different limits per plan
    switch (req.apiPlan) {
      case 'free':       return 60;
      case 'pro':        return 600;
      case 'enterprise': return 6000;
      default:           return 10;
    }
  },
  keyGenerator: (req) => req.apiKey,
  standardHeaders: true,  // X-RateLimit-* headers
  legacyHeaders: false,
});

app.use('/api/v1', authenticate, apiLimiter);
```

---

## Marketplace & Platform Distribution

Build on top of existing platforms to **tap into their user base** and distribution network.

| Platform | Revenue Split | Install Base | Monetisation |
|----------|--------------|--------------|--------------|
| **Shopify Apps** | 0% (first $1M) | 4.6M stores | Subscription or usage |
| **WordPress Plugins** | Varies (marketplace) | 800M+ sites | Freemium, GPL required |
| **Slack Apps** | 0% | 750K+ orgs | External billing |
| **Figma Plugins** | 0% | 4M+ designers | External billing |
| **Notion Integrations** | 0% | 100M+ users | External billing |

### Strategy: Platform as Distribution
- Build where users already are -- lower acquisition cost
- Platform handles auth, billing UI, discovery
- **Risk**: platform dependency, API changes, de-listing
- Diversify across platforms when possible

### Shopify App Lifecycle

```
Build App  ->  App Review
                  |
                  v
            List on Store  ->  Merchants Install
                  |
                  v
            Usage Billing via Shopify API
```

Shopify eliminated their 20% rev share for the first $1M -- making it one of the most developer-friendly platforms.

### VS Code Extensions
- Free to publish, no revenue share
- Monetise via premium features + external auth
- Examples: GitHub Copilot, GitLens, Tabnine
- Huge reach -- 15M+ VS Code users

---

## Landing Pages & Marketing Basics

You can build the best product in the world -- it doesn't matter if nobody knows it exists.

### Landing Page Anatomy
- **Hero**: clear headline + CTA + social proof
- **Problem**: pain point your product solves
- **Solution**: how your product fixes it
- **Features**: 3-5 key capabilities with visuals
- **Pricing**: transparent tiers
- **Testimonials**: real users, real quotes
- **CTA**: repeated call-to-action at bottom

### Tools for Developer-Marketers

| Tool | Best For | Cost |
|------|----------|------|
| **Next.js** | Full control, SEO | Free + hosting |
| **Framer** | Visual builder, fast | $5-20/mo |
| **Carrd** | Simple one-pagers | $19/yr |
| **Typedream** | Notion-like builder | Free-$15/mo |

### Developer Marketing Channels
- **Content marketing** -- blog posts, tutorials, guides
- **SEO** -- rank for problem-related keywords
- **Twitter/X** -- build in public, share progress
- **Hacker News** -- Show HN launches
- **Product Hunt** -- launch day visibility
- **GitHub** -- README as marketing, stars as social proof
- **YouTube** -- demos, tutorials, comparisons

### Common Marketing Mistakes
- Describing features instead of benefits
- No clear call to action
- Building for months without talking to users
- Ignoring SEO -- free long-term traffic
- Not having a changelog or public roadmap

---

## Analytics & Metrics That Matter

| Metric | Formula | Good Target |
|--------|---------|-------------|
| **MRR** | Sum of monthly recurring payments | Growing month-over-month |
| **Churn Rate** | Lost customers / start-of-period total | <5% monthly (B2C), <2% (B2B) |
| **LTV** | ARPU / Churn Rate | >3x CAC |
| **CAC** | Sales + marketing cost / new customers | LTV:CAC > 3:1 |
| **NRR** | (Start MRR + expansion - contraction - churn) / Start MRR | >100% (ideally >120%) |
| **Conversion** | Paid users / total signups | 2-5% (freemium), 10-20% (trial) |

### The Metrics That Actually Matter Early On
- **Retention** -- are people coming back?
- **Activation** -- do signups reach the "aha" moment?
- **Revenue** -- will someone pay for this?

Vanity metrics (page views, signups, stars) feel good but don't pay bills.

### Product Analytics
- PostHog (open source)
- Mixpanel
- Amplitude
- Plausible (privacy-first)

### Revenue Analytics
- Stripe Dashboard
- Baremetrics
- ChartMogul
- ProfitWell (free)

### The SaaS Rule of 40

Growth rate + profit margin should exceed 40%. A company growing at 50% can afford -10% margins. One growing at 10% needs 30%+ margins.

---

## Legal Considerations

Shipping software commercially means **legal obligations**. Don't skip these.

### Documents You Need

| Document | Purpose | Required? |
|----------|---------|-----------|
| **Terms of Service** | Rules of using your product | Yes |
| **Privacy Policy** | How you handle user data | Legally required |
| **Cookie Policy** | Cookie consent (EU) | GDPR/ePrivacy |
| **DPA** | Data Processing Agreement | B2B / enterprise |
| **Refund Policy** | Consumer protection | Recommended |

### GDPR Essentials
- Applies to any EU user, regardless of your location
- Lawful basis for processing (consent or legitimate interest)
- Right to access, rectify, delete data
- 72-hour breach notification requirement
- Fines up to 4% of global revenue

### Tax Obligations
- **US**: Sales tax varies by state (Nexus rules)
- **EU**: VAT on digital services (MOSS/OSS scheme)
- **UK**: VAT at 20% over £85K threshold
- Merchant of Record (Paddle, Lemon Squeezy) handles this for you
- Use **Stripe Tax** or **TaxJar** for automated compliance

### Business Entity
- **Sole trader**: simplest, unlimited personal liability
- **LLC (US)** / **Ltd (UK)**: limited liability, pass-through tax
- **C-Corp (US)**: required for VC funding (Delaware)
- Get a separate business bank account early
- Consider **Stripe Atlas** for US LLC formation ($500)

---

## Scaling from Free to Paid

The hardest transition: when your free project becomes a real business.

### When to Start Charging
- Users are already getting measurable value
- You have at least 10 users who would be upset if it disappeared
- Support burden is growing
- You need revenue to sustain development
- **Don't wait for "perfect"** -- charge early, iterate pricing

### Grandfathering Strategies
- **Lock in price** -- early users keep their rate forever
- **Generous free tier** -- existing users get legacy plan
- **Extended trial** -- give existing users 6-12 months free
- Always communicate changes **well in advance**
- Thank early users -- they took a risk on you

### Migration Playbook

1. **Announce** -- Email users 60+ days before changes
2. **Grandfather** -- Give existing users special pricing or extended access
3. **Introduce Tiers** -- Start with 2-3 simple plans
4. **Iterate** -- Adjust pricing based on feedback and data

### Real-World Examples
- **Heroku**: killed free tier in 2022 -- backlash, migration to Railway/Fly
- **Figma**: generous free tier drove adoption before monetising teams
- **Notion**: free for personal, paid for teams -- viral growth

---

## Common Mistakes Indie Developers Make

### Building Mistakes
- **Building without validating** -- spending months on something nobody wants
- **Over-engineering** -- microservices for 10 users
- **Not shipping** -- perfectionism is the enemy
- **Ignoring mobile** -- most traffic is mobile now
- **No analytics** -- flying blind on user behaviour

### Pricing Mistakes
- **Pricing too low** -- $5/mo signals "toy", not "tool"
- **Too many tiers** -- paradox of choice kills conversion
- **No annual discount** -- missing low-churn revenue
- **Charging per-feature** instead of per-value
- Lifetime deals that kill long-term revenue

### Distribution Mistakes
- **No landing page** -- sending traffic to a GitHub repo
- **No email list** -- relying on social media you don't own
- **Launching once** -- every feature is a launch opportunity
- **Ignoring SEO** -- the cheapest long-term channel
- Not building in public -- missing free marketing

### What to Do Instead
- **Talk to 10 users** before writing any code
- **Launch in weeks**, not months
- **Start with one price** and increase it until people push back
- **Write about your journey** -- content compounds
- **Charge from day one** -- paying users give better feedback
- Use a Merchant of Record to skip tax complexity

---

## Summary & Further Reading

### Key Takeaways
- Distribution model matters as much as the product itself
- **SaaS + recurring revenue** is the dominant model for a reason
- Use a **Merchant of Record** (Paddle, LemonSqueezy) to simplify tax and compliance
- Open source can be a business strategy, not just charity
- Validate before building, launch early, iterate pricing
- **LTV:CAC > 3:1** and **churn < 5%** are your north stars

### The Distribution Spectrum

`Open Source` -> `Freemium` -> `Paid SaaS`

Most successful products **combine** free distribution with paid monetisation. Give away what builds trust. Charge for what creates ROI.

### Further Reading
- **"Deploy Empathy"** by Michele Hansen -- customer research
- **"The Mom Test"** by Rob Fitzpatrick -- validating ideas
- **"Indie Hackers"** -- community of bootstrapped founders
- **Stripe Docs** -- best-in-class payment integration guide
- **choosealicense.com** -- pick the right open source license
- **"Working in Public"** by Nadia Eghbal -- open source economics
- **SaaS Playbook** by Rob Walling -- pricing and growth

### Tools Mentioned
Stripe, Paddle, LemonSqueezy, Keygen, Tauri, PostHog, Clerk, Vercel, Framer, Stripe Atlas
