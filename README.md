# Quantum Club ASU Website

Welcome to the official repository for the Quantum Club at Arizona State University's website. Built using [Jekyll](https://jekyllrb.com/) and the [Chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) theme, this site serves as a hub for our community, blog posts, and research updates.

## 🚀 Getting Started

### Prerequisites

- **Ruby** (version 3.1 or higher)
- **Bundler** (`gem install bundler`)
- **Node.js** (for asset processing)

### Local Development

1. **Clone the repository:**
   ```bash
   git clone https://github.com/QuantumClubASU/quantumclubasu.github.io.git
   cd quantumclubasu.github.io
   ```

2. **Install dependencies:**
   ```bash
   bundle install
   npm install
   ```

3. **Run the local server:**
   ```bash
   bash tools/run.sh
   ```
   *Alternative:* `bundle exec jekyll serve`
   
   The site will be available at `http://127.0.0.1:4000`.

---

## 📝 How to Update the Website

### 1. Adding a New Blog Post
Posts are stored in the `_posts/` directory (or its subdirectories like `_posts/announcements/`).

1. **Create a new Markdown file** with the format: `YYYY-MM-DD-title.md`.
2. **Add front matter** at the top of your file:
   ```markdown
   ---
   title: "Your Post Title"
   date: 2026-04-01 12:00:00 -0700
   categories: [Announcements]
   tags: [Quantum, Research]
   image: /assets/img/your-image.png # Optional
   ---
   Your post content goes here...
   ```

### 2. Updating Website Configuration
Site-wide settings (title, description, social links, etc.) are managed in `_config.yml`.
- **Social Links:** Update the `social.links` section.
- **Site Metadata:** Update `title`, `tagline`, and `description`.
- **Comments:** The site uses Giscus; settings are located under the `comments` key.

### 3. Adding Media
- **Images:** Place images in `/assets/img/` or the designated post media folder.
- **Reference in Post:** Use standard Markdown or the Chirpy image syntax:
  ```markdown
  ![Description](/assets/img/my-image.png)
  ```

### 4. Updating Tabs/Pages
Sidebar navigation nodes (like 'Team', 'Blog', 'Socials') are defined in the `_tabs/` directory. Modify these files to update static page content.

---

## 🏗️ Deployment
This project uses **GitHub Actions** for automated deployment.

1. **Commit your changes:**
   ```bash
   git add .
   git commit -m "feat: add new research post"
   ```
2. **Push to the main branch:**
   ```bash
   git push origin main
   ```
3. GitHub Actions will automatically rebuild and deploy the site to GitHub Pages.

---

## 💡 Pro Tips
- **Testing:** You can run `bash tools/test.sh` to check for broken links and other issues.
- **Drafts:** You can create a `_drafts/` folder for posts that aren't ready yet.
- **Search:** The Chirpy theme includes built-in search that indexes your posts automatically.
- **Documentation:** For advanced customization, refer to the [Chirpy Wiki](https://github.com/cotes2020/jekyll-theme-chirpy/wiki).

---

© 2025-2026 Quantum Club ASU. Built with ❤️ and Quantum bits.
