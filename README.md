# 📧 Arcanomy Newsletters

This repository contains all newsletter content for Arcanomy's email campaigns, written in MDX format with automated publishing through GitHub webhooks.

## 📁 Repository Structure

```
newsletters/
├── 2025/                      # Newsletters organized by year
│   ├── 01-january/           # Monthly folders
│   ├── 02-february/
│   └── ...
├── templates/                # Reusable newsletter templates
│   ├── weekly-digest.mdx
│   ├── product-launch.mdx
│   └── educational-series.mdx
├── assets/                   # Newsletter assets
│   └── images/
│       └── headers/         # Header images
├── config/                   # Configuration files
│   ├── segments.json        # Subscriber segments
│   └── test-recipients.json # Test email list
└── .github/
    └── workflows/
        └── validate.yml     # MDX validation on PR
```

## ✍️ Writing Newsletters

### File Naming Convention
Newsletter files should follow this naming pattern:
```
YYYY-MM-DD-slug.mdx
```

Example: `2025-01-15-market-update.mdx`

### MDX Frontmatter

Every newsletter must include the following frontmatter:

```yaml
---
# Required Fields
slug: "2025-01-15-market-update"
subject: "📈 The January Rally: What It Means for Your Portfolio"
preheader: "Plus: New FIRE calculator features"

# Publishing Controls
publish: false                    # Must be true for live send
mode: "test"                      # "test" | "live"

# Targeting
segment: "all"                    # "all" | "engaged_30d" | "new_7d" | "dormant_90d"
tags: ["investing", "markets"]    # For categorization

# Optional Fields
schedule: "2025-01-15T09:00:00-05:00"  # ISO 8601 with timezone
utm_campaign: "weekly-digest-2025-01"   # UTM tracking
reply_to: "saleh@arcanomy.com"         # Override reply-to
test_override: ["specific@test.com"]    # Override test recipients

# Content Slots (Optional)
ads:
  - position: "top"
    content: "Check out our new Tax Calculator"
    cta: "Calculate Now"
    url: "/calculators/tax-calculator"

social:
  x: "Just published our weekly digest on market trends..."
  linkedin: "New insights on Q1 market movements..."
  threads: "Quick take on this week's rally..."

# Feature Flags (Optional)
features:
  show_related_posts: true
  show_calculator_spotlight: true
  show_community_section: false
---
```

## 📝 Available MDX Components

The following React Email components are available in MDX:

### Layout Components
- `<Container>` - Main email container
- `<Section>` - Content sections
- `<Row>` / `<Column>` - Grid layout
- `<Spacer size={32} />` - Add spacing

### Content Components
- `<Heading>` - Email headings (h1-h6)
- `<Text>` - Paragraph text
- `<Button href="/path">` - CTA buttons
- `<Link href="/path">` - Inline links
- `<Image src="" alt="" />` - Images

### Rich Content
- `<Callout type="tip|warning|info">` - Highlighted content boxes
- `<DataTable>` - Tables with markdown syntax
- `<CodeBlock>` - Code snippets
- `<Quote>` - Blockquotes

### Newsletter-Specific
- `<Greeting />` - Personalized greeting
- `<Signature />` - Email signature
- `<BlogGrid posts={["slug1", "slug2"]} />` - Featured blog posts
- `<CalculatorCard />` - Calculator highlights
- `<SocialLinks />` - Social media links
- `<UnsubscribeFooter />` - Unsubscribe links (auto-added)

## 🚀 Publishing Workflow

### Test Mode (Default)
1. Create/edit MDX file with `publish: false` or `mode: "test"`
2. Push to GitHub
3. Newsletter automatically sent to test recipients only
4. Subject line prefixed with [TEST]

### Live Mode
1. Set `publish: true` AND `mode: "live"` in frontmatter
2. Push to main branch
3. n8n workflow validates and triggers send
4. Newsletter sent to specified segment
5. Archived to newsletter-archive repository
6. Social posts created (if configured)

### Safety Gates
- Both `publish: true` AND `mode: "live"` required for live sends
- Test mode always overrides to test recipients
- Idempotency prevents duplicate sends
- All newsletters archived for reference

## 🎯 Subscriber Segments

Configured in `config/segments.json`:
- `all` - All active subscribers
- `engaged_30d` - Opened email in last 30 days
- `new_7d` - Subscribed in last 7 days
- `dormant_90d` - Haven't opened in 90+ days

## 🧪 Test Recipients

Configured in `config/test-recipients.json`:
- Always receives test mode emails
- Can be overridden with `test_override` in frontmatter
- Useful for QA before live sends

## 📊 Tracking & Analytics

All newsletters include:
- Open tracking pixel
- Click tracking on links
- UTM parameters for Google Analytics
- Unsubscribe one-click compliance
- Engagement metrics in dashboard

## 🔧 Development

### Local Preview
```bash
# Clone repository
git clone https://github.com/username/arcanomy-newsletters.git

# Create new newsletter
cp templates/weekly-digest.mdx 2025/01-january/2025-01-22-new-issue.mdx

# Edit content
code 2025/01-january/2025-01-22-new-issue.mdx

# Push to trigger test send
git add .
git commit -m "Add newsletter: 2025-01-22"
git push
```

### Validation
The `.github/workflows/validate.yml` workflow:
- Validates MDX syntax on pull requests
- Checks required frontmatter fields
- Ensures proper file naming
- Prevents accidental live sends on PRs

## 📋 Checklist Before Going Live

- [ ] Content reviewed and proofread
- [ ] Links tested and working
- [ ] Images optimized and hosted
- [ ] Test email sent and reviewed
- [ ] Subject line and preheader compelling
- [ ] Segment correctly targeted
- [ ] Social posts prepared (if applicable)
- [ ] Set `publish: true` and `mode: "live"`

## 🚨 Emergency Procedures

### Cancel Scheduled Send
1. Set `publish: false` immediately
2. Push to GitHub
3. Contact admin if send in progress

### Wrong Segment Sent
1. Note broadcast ID
2. Send apology/correction if needed
3. Update segment configuration

### Content Error After Send
1. Update MDX file for archive
2. Send correction if critical
3. Note in post-mortem

## 📚 Resources

- [MDX Documentation](https://mdxjs.com/)
- [React Email Components](https://react.email/)
- [Arcanomy Style Guide](https://arcanomy.com/style-guide)
- [Newsletter Best Practices](https://arcanomy.com/docs/newsletters)

## 🤝 Contributing

1. Create feature branch
2. Write/edit newsletter content
3. Test with `mode: "test"`
4. Create pull request
5. Get review from content team
6. Merge to main when approved

## 📄 License

© 2025 Arcanomy. All rights reserved.

---

**Questions?** Contact saleh@arcanomy.com