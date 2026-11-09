<div align="center">

# 🚀 Bootstrap 5 Starter

**A simple starting point for building responsive websites—and understanding how they work.**

HTML · Bootstrap · Sass · Font Awesome · JavaScript

![Bootstrap 5](https://img.shields.io/badge/Bootstrap-5-7952B3?logo=bootstrap&logoColor=white)
![Sass](https://img.shields.io/badge/Styles-Sass-CC6699?logo=sass&logoColor=white)
![Font Awesome](https://img.shields.io/badge/Icons-Font_Awesome-538DD7?logo=fontawesome&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E?logo=javascript&logoColor=black)

**Install → Compile → Preview → Customize**

</div>

---

## 🧭 Find your way

- [What is included](#-what-is-included)
- [Guided setup](#-guided-setup)
- [Project structure](#-project-structure)
- [How the files work together](#-how-the-files-work-together)
- [Customize your theme](#-customize-your-theme)
- [Build your first component](#-build-your-first-component)
- [Add icons and JavaScript](#-add-icons-and-javascript)
- [Troubleshooting](#-troubleshooting)
- [Before publishing](#-before-publishing)
- [Learning resources](#-learning-resources)

## ✨ What is included

| Tool | What it does | Where you use it |
| --- | --- | --- |
| 📐 Bootstrap 5 | Provides responsive layouts, utilities, and components | Classes in `index.html` |
| 🎨 Sass | Compiles your theme settings and styles into CSS | Files in `scss/` |
| ⭐ Font Awesome | Provides icons using local font files | Icon classes in your HTML |
| ⚙️ Bootstrap JavaScript | Powers components such as dropdowns and modals | `js/bootstrap.bundle.min.js` |
| 🧩 Your JavaScript | Holds your own interactions | `js/script.js` |

There is no application framework or JavaScript bundler. The browser loads the HTML, compiled CSS, JavaScript, and fonts directly. Node.js is used for development tooling.

## 🚀 Guided setup

### 1. Check your tools

Install a supported Node.js LTS release with npm, then confirm both commands work:

```bash
node --version
npm --version
```

You also need a browser and a code editor. No environment variables or database are required.

### 2. Install the dependencies

Open a terminal inside this project's folder and run:

```bash
npm install
```

This installs Bootstrap, Sass, and Font Awesome into `node_modules/`. Keep `package-lock.json`: it records the resolved dependency versions so installations can be reproduced.

### 3. Start compiling Sass

```bash
npm run sass:build
```

> **Despite its name, `sass:build` currently starts a watcher.** It compiles the files in `scss/` into `css/`, then stays running and recompiles when you save Sass changes. Press **Ctrl+C** to stop it.

For a single compilation that exits when finished, use the installed Sass executable:

```bash
npx --no-install sass --no-source-map scss:css
```

### 4. Preview the page

Serve the project folder over HTTP using your editor's local web server, such as VS Code's Live Server extension, and open `index.html` through that server.

If Python 3 is already installed, you can instead run this in a **second terminal**:

```bash
python3 -m http.server 5500 --bind 127.0.0.1
```

Then visit **http://localhost:5500**.

Using HTTP matters because `js/script.js` is loaded as a JavaScript module; opening the page through `file://` can prevent it from loading.

### 5. Check that everything works

- The page shows the starter heading, a Bootstrap button, and a star icon.
- Change the background color in `scss/styles.scss` and save.
- Confirm the Sass watcher reports a compilation, then refresh the browser.

The Sass watcher rebuilds CSS. It does **not** provide a web server or automatically refresh the page; an editor extension may handle browser refresh separately.

## 🗂️ Project structure

```text
bs5-starter/
├── index.html                  # Page markup and asset links
├── scss/                       # Styles you edit
│   ├── bootstrap.scss          # Bootstrap theme overrides and import
│   ├── font-awesome.scss       # Font Awesome core, brands, and solid icons
│   └── styles.scss             # Your own page and component styles
├── css/                        # Generated styles loaded by the browser
│   ├── bootstrap.css
│   ├── font-awesome.css
│   └── styles.css
├── js/
│   ├── bootstrap.bundle.min.js # Local Bootstrap bundle, including Popper
│   └── script.js               # Your JavaScript module
├── webfonts/                   # Local Font Awesome font files
├── package.json                # Dependencies and npm commands
├── package-lock.json           # Resolved dependency versions
└── .gitignore                  # Excludes node_modules/ from Git
```

**Edit the files in `scss/`, not the generated files in `css/`.** The next compilation overwrites manual CSS edits. Likewise, avoid editing `node_modules/`; reinstalling or updating dependencies can replace those changes.

## 🔄 How the files work together

```text
scss/bootstrap.scss    → Sass → css/bootstrap.css
scss/font-awesome.scss → Sass → css/font-awesome.css → webfonts/
scss/styles.scss       → Sass → css/styles.css

index.html loads the compiled CSS and the JavaScript files.
```

Each Sass file is compiled separately. The Font Awesome stylesheet references fonts in `webfonts/`; the HTML links the three stylesheets and loads Bootstrap's bundle before your script.

The current CSS order is **Font Awesome → Bootstrap → your styles**. Loading your styles last lets later rules override earlier rules when specificity and importance allow it.

## 🎨 Customize your theme

### Change Bootstrap's design settings

Put Bootstrap variable overrides **before** the existing import in `scss/bootstrap.scss`:

```scss
// Theme settings: define these before importing Bootstrap.
$primary: #6f42c1;
$secondary: #475569;
$border-radius: 0.75rem;
$font-family-sans-serif: system-ui, sans-serif;

@import "../node_modules/bootstrap/scss/bootstrap.scss";
```

Save and compile. Bootstrap uses these values to generate styles such as `.btn-primary` and rounded component corners.

To explore more settings, read `node_modules/bootstrap/scss/_variables.scss`. Copy the variables you want to override into your own `scss/bootstrap.scss`; leave the dependency file untouched.

### Add your own styles

Use `scss/styles.scss` for page backgrounds, custom components, and other project-specific styling:

```scss
// Replace the starter background styles with these to try a light theme.
body {
  background-color: #f8fafc;
  color: #0f172a;
}

.welcome-card {
  max-width: 40rem;
  margin-inline: auto;
}
```

> **Why doesn't `$primary` in `styles.scss` change Bootstrap buttons?**
> Each Sass entry point has its own compilation scope. The starter currently defines `$primary: #333` in `styles.scss` and uses it for the body background only. To change Bootstrap's primary color, define `$primary` in `bootstrap.scss` before its import.

## 🧱 Build your first component

After applying the light background example above, replace the existing contents of `<body>` with this markup, keeping both script tags at the bottom:

```html
<main class="container py-5">
  <section class="welcome-card card border-0 shadow-sm">
    <div class="card-body p-4 p-md-5">
      <span class="badge text-bg-primary mb-3">Your first component</span>
      <h1 class="h2 mb-3">Build something useful.</h1>
      <p class="text-body-secondary mb-4">
        Start with a clear layout, customize your theme, and add one
        interaction at a time.
      </p>
      <button id="welcome-button" class="btn btn-primary" type="button">
        <i class="fa-solid fa-star me-2" aria-hidden="true"></i>
        Try an interaction
      </button>
      <p id="welcome-message" class="mt-3 mb-0" role="status"></p>
    </div>
  </section>
</main>

<script src="js/bootstrap.bundle.min.js"></script>
<script type="module" src="js/script.js"></script>
```

**What to notice:** `.container` limits the page width; `.py-5` adds vertical space; `.p-4 .p-md-5` increases padding from the medium breakpoint upward. The card and button use Bootstrap styles, while `.welcome-card` comes from your own Sass.

## ⭐ Add icons and JavaScript

### Use a solid or brand icon

```html
<!-- Decorative icon: the visible text provides the meaning. -->
<span><i class="fa-solid fa-star" aria-hidden="true"></i> Featured</span>

<!-- Brand icon with a text label. -->
<span><i class="fa-brands fa-github" aria-hidden="true"></i> GitHub</span>
```

The starter imports **solid** and **brand** icons. Other styles need their corresponding imports and available font files; a regular font file alone does not enable regular icon classes.

For an icon-only button, give the button an accessible name, for example `aria-label="Close"`. Keep decorative icons hidden from assistive technology with `aria-hidden="true"`.

### Connect the example button

Add this to `js/script.js`:

```js
const welcomeButton = document.querySelector('#welcome-button');
const welcomeMessage = document.querySelector('#welcome-message');

if (welcomeButton && welcomeMessage) {
  welcomeButton.addEventListener('click', () => {
    welcomeMessage.textContent = 'Your JavaScript is connected. Keep building!';
  });
}
```

The element checks let the script run on pages without this component. `textContent` inserts the message as text, and the status region announces the update to assistive technology.

## 🛠️ Troubleshooting

| Problem | What to check |
| --- | --- |
| `npm` is not recognized | Install Node.js with npm, then reopen your terminal. |
| `sass:build` never finishes | This is expected: the command watches for changes. Stop it with Ctrl+C. |
| Sass changes do not appear | Keep the watcher running, resolve compilation errors, then refresh the browser. |
| Buttons keep the old primary color | Put `$primary` before the Bootstrap import in `scss/bootstrap.scss` and recompile. |
| An icon appears as an empty square | Check the icon name and imported style, then look for missing font requests in the browser's Network panel. |
| Custom JavaScript does not run | Use a local HTTP server and inspect the browser console for errors. |
| A dropdown or modal does not open | Check the Bootstrap bundle loads successfully and the component uses Bootstrap 5 `data-bs-*` attributes. |
| Sass prints deprecation warnings | The Bootstrap and Font Awesome Sass imports can produce warnings with newer Sass versions. Check whether compilation succeeds; review dependency compatibility before changing import syntax. |

## 📦 Before publishing

1. Run a single Sass compilation and resolve any errors.
2. Preview through a local server and check the browser console and Network panel.
3. Test narrow and wide screens, keyboard navigation, and readable color contrast.
4. If you used the guided example, click the button and confirm its message appears.
5. Upload `index.html`, `css/`, `js/`, `webfonts/`, and any additional page assets to a static host.

The browser does not need `node_modules/` or Sass source files to run this site. Keep the published folder structure intact so relative asset URLs continue to work.

**Dependency updates need an extra check:** compiling Sass rebuilds CSS, but does not copy Bootstrap's JavaScript bundle or Font Awesome's fonts. After updating those packages, refresh the local files in `js/` and `webfonts/` from the installed packages and verify compatibility.

There is no automated test suite configured. The checks above provide a starting point for manual validation.

## 📚 Learning resources

- [Bootstrap documentation](https://getbootstrap.com/docs/5.3/getting-started/introduction/) — layouts, utilities, components, and JavaScript behavior.
- [Bootstrap Sass customization](https://getbootstrap.com/docs/5.3/customize/sass/) — theme variables and import order.
- [Sass documentation](https://sass-lang.com/documentation/) — variables, nesting, and compilation.
- [Font Awesome documentation](https://docs.fontawesome.com/) — icon styles and accessibility.

### 🎯 A small challenge

Turn the welcome card into a responsive feature section: show one card per row on small screens and three per row on large screens. Give each card an icon and a useful action. Verify keyboard access and check that no horizontal scrollbar appears on mobile.

---

Inspired by [Brad Traversy's Bootstrap 5 Simple Starter](https://github.com/bradtraversy/bs5-simple-starter). This guide describes the files and commands in this repository.

Maintained by **Moslem Ajra**.
