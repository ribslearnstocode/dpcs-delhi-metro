# LeadsPM Delhi Metro website

This is a self-contained React website for GitHub Pages. Its validated metro
network is served as `public/metro-network.json`, and route calculations run in
the browser; no Flask server or API is needed.

## Run and test

```powershell
npm ci
npm test
npm run build
npm run preview
```

## GitHub Pages

Push the `github-pages` branch to build and deploy the site with GitHub Actions.
The workflow publishes only `website/dist`; the `public/CNAME` file configures
`dpcs.ribence.com.np` on the GitHub Pages side. Configure the matching DNS
record with your DNS provider.
