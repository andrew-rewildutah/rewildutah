# Deploying rewildutah.com via GoDaddy
# ======================================

## What you have
- index.html  —  the complete single-file website (all CSS and JS inline)

## Option 1: GoDaddy Website Builder (easiest, 5 min)
This works if you want zero maintenance overhead.

1. Log into godaddy.com → My Products
2. Find your domain → click "Manage" next to rewildutah.com
3. Click "Website Builder" → choose the free tier
4. In the builder, look for "Custom HTML" or use the raw HTML option
   (GoDaddy's builder supports pasting raw HTML in some plans)

However: GoDaddy's drag-and-drop builder will fight your custom HTML.
For a custom-coded site, Option 2 is much cleaner.

## Option 2: GoDaddy Hosting + File Upload (recommended)
GoDaddy includes basic cPanel web hosting with domain purchases.

1. Log into godaddy.com → My Products
2. Find "Web Hosting" — if not included, it's ~$3/month to add
3. Click "Manage" → open cPanel
4. In cPanel, click "File Manager"
5. Navigate to public_html/
6. Delete any default index.html that's there
7. Upload your index.html
8. Done — visit rewildutah.com and it should load

## Option 3: GitHub Pages + GoDaddy DNS (best for a developer)
This is the cleanest long-term setup. Free, version-controlled, fast.

1. Create a GitHub repo called "rewildutah"
2. Push index.html to the repo
3. Go to repo Settings → Pages → Source: main branch → /root
4. GitHub gives you a URL like: rewild-genomics.github.io/rewildutah
5. Now point your GoDaddy domain to it:
   a. GoDaddy DNS → Add CNAME record:
      - Name: www
      - Value: rewild-genomics.github.io
   b. Add A records for apex domain (@):
      - 185.199.108.153
      - 185.199.109.153
      - 185.199.110.153
      - 185.199.111.153
   c. In your GitHub repo, add a file called CNAME (no extension)
      containing just:  rewildutah.com
6. Wait 10–30 min for DNS to propagate → rewildutah.com loads from GitHub

GitHub Pages also gives you free HTTPS automatically.

## Option 4: Netlify drop (30 seconds, also free)
1. Go to netlify.com/drop
2. Drag your index.html into the browser
3. Netlify gives you a URL instantly
4. Go to Domain Settings → Add custom domain → rewildutah.com
5. Netlify will walk you through updating GoDaddy DNS (2 DNS records)

This is the fastest path to a live site with HTTPS.

## Updating the site later
Since it's a single HTML file, updating is simple:
- Edit index.html locally
- Re-upload to wherever you're hosting
- If using GitHub Pages: git commit + git push → site updates in ~60 sec

## Things to customize before going live
- Replace "Andrew [Last Name]" with your full name in the About section
- Update GitHub and bioRxiv links to your actual profiles
- Update andrew@rewildutah.com to your real email
- Add a real photo to the About section (replace the SVG placeholder)
  — swap the <div class="about-portrait-frame"> contents with an <img> tag
- Update the pipeline status dots to reflect actual progress
- The contact form currently just shows a success message client-side
  — to make it actually send emails, add Formspree:
    1. Sign up at formspree.io (free tier handles 50 submissions/month)
    2. Create a form, get your endpoint URL
    3. Change <form id="contact-form" onsubmit="handleSubmit(event)">
       to    <form action="https://formspree.io/f/YOUR_ID" method="POST">
    4. Remove the handleSubmit JS function
    5. Done — submissions go to your email

## GoDaddy-specific notes
- GoDaddy domains auto-renew — make sure your payment method is current
- GoDaddy includes free SSL (HTTPS) on their hosting plans
- If you go the GitHub Pages route, GoDaddy's SSL doesn't apply —
  GitHub Pages provides its own free SSL via Let's Encrypt
- GoDaddy's DNS propagation is usually fast (~15 min) but can take up to 48hr
