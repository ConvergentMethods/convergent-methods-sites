# Company Site Directory

This directory hosts all public-facing company sites for Convergent Methods LLC.

## Structure

Each domain has its own subdirectory:
- `convergentmethods.com/` - Primary company website
- `convergentmethods.ai/` - AI-focused company website
- `convergentmethods.io/` - Product-focused website

Each domain folder contains:
- `index.html` - Stub website landing page
- `CNAME` - Domain name for GitHub Pages configuration

## Deployment via GitHub Pages

Each domain folder is served by GitHub Pages using its CNAME file.

### To Deploy:

1. **Push changes to the main branch.**
   - Each domain folder should be in its own branch or configured as a separate GitHub Pages site
   - Alternatively, use GitHub Actions or a monorepo structure

2. **Enable GitHub Pages in the repo:**
   - Go to Settings → Pages
   - Select "Deploy from branch"
   - Choose the appropriate branch (main or a domain-specific branch)

3. **Configure DNS in Namecheap:**
   - Set CNAME record for `@` (root domain) → `<your-github-username>.github.io`
   - Set CNAME record for `www` → `<your-github-username>.github.io`
   - Wait for DNS propagation (typically 5-30 minutes)

4. **HTTPS Certificate:**
   - GitHub will automatically issue HTTPS certificates via Let's Encrypt
   - Certificate provisioning typically takes a few minutes after DNS propagation

## Domain Portfolio

For complete domain inventory and renewal information, see:
- `Business/Operations/DOMAIN_PORTFOLIO.md`

## Notes

- Each domain's CNAME file must contain only the domain name (no trailing slash, no www prefix)
- GitHub Pages requires the CNAME file to be in the root of the deployed branch
- For multiple domains, consider using separate branches or GitHub Actions workflows

