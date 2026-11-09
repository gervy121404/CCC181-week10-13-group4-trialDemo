# CCC181 Week 10: CampusConnect Mobile-First Login Page

React + TypeScript starter for the Week 10 group activity. The page is already
built. Your group's job is the **mobile-first CSS** and the **GitHub teamwork**.

## Run it

```bash
npm install
npm run dev          # open the local URL it prints
npm run dev:phone    # same, but your phone (same Wi-Fi) can open the Network URL
npm run build        # must finish with no errors before you submit
```

## Rules

- Edit only the CSS files in `src/styles/` (one member = one file). Do not edit `reset.css`.
- Plain CSS only. No Tailwind, Bootstrap, Material UI, styled-components, or any UI library.
- Phone styles first (no media query), then `min-width` queries only. Never `max-width`.
- Do not edit the `.tsx` files or rename classes. If you must, tell the group first.

## Group information (fill in)

| Item | Your answer |
| --- | --- |
| Group number | 4 |
| Section | IT3-B |
| Repository URL | https://github.com/tangapagyandave-sudo/ccc181-week10-group4 |

## Members (each member fills in their own row in their own commit)

| Member | Name | GitHub username | CSS file | What I did |
| --- | --- | --- | --- | --- |
| 1 (leader) | Tangapa, Gyan Dave B. | tangapagyandave-sudo | `base.css` | Wrote `src/styles/base.css` using a mobile-first approach, in 3 breakpoints: basic mobile layout with Flexbox and a 1-column login layout, adjusted spacing and padding from 768px, a 2-column layout with visible brand perks from 1024px, and a centered 1200px container from 1280px. Also reviewed the `nav.css` pull request. |
| 2 | Kent T. Baloyos | Itsken-the-average | `nav.css` | Wrote src/styles/nav.css (Flexbox + Grid) using a mobile-first approach, in 3 commits: phone layout with a stacked navbar, 48px (3rem) links and a 1-column footer grid, brand left with links in one row from 768px, and a 3-column footer from 1024px. Reviewed the base.css pull request. |
| 3 | Gervy J. Rosario | gervy121404 | `form.css` | Wrote src/styles/form.css (Flexbox) using a mobile-first approach, in 4 commits: phone layout with stacked 48px (3rem) fields and buttons, side-by-side checkbox row and buttons from 768px, and roomier card from 1024px. Reviewed the nav.css pull request. |

## Experiment 0: the page without the viewport tag

What did the page look like in DevTools phone mode **before** adding the viewport meta tag?
What changed **after** adding it?

> Before adding the viewport tag: The page looked zoomed out and appeared smaller in DevTools phone mode, making the text and elements difficult to read.

After adding the viewport tag: The page adjusted to the phone's actual screen width, making the content properly sized and easier to view.

## DevTools test results

| Width | What must be true | Pass? |
| --- | --- | --- |
| 360 px | 1 column. Nav links stacked and 48px tall. Options and buttons stacked. Footer in 1 column. No sideways scrollbar. | Pass |
| 768 px | Nav in one row (brand left, links right). Checkbox and link in one row. Two buttons side by side. | Pass |
| 1024 px | Brand panel and login card side by side. Footer in 3 columns. Heading is larger. | Pass |
| 1280 px | Content centered and stops at 1200px. | Pass |

### Breakpoints I observed

Using **Show media queries** and dragging slowly from 360 px to 1280 px, the layout changed at these exact widths:


nav.css
>The layout changed at 768 px, 1024 px, and 1280 px. At 768 px, the navigation became horizontal with the brand on the left and the links in one row, the container side padding grew to 2rem, the checkbox and “Forgot password?” appeared side by side, and the two bottom buttons formed a row. The login card also became centered with a maximum width of 32rem. At 1024 px, the brand panel and login card formed two columns, the footer changed to three columns, and the welcome heading became larger (2.5rem) with the extra list visible. The login card also got roomier padding (2.5rem). At 1280 px, the content became centered with a maximum width of 1200 px. No broken layouts or horizontal scrolling appeared at the tested widths between 360 px and 1280 px.

form.css
> The layout changed at 768 px, 1024 px, and 1280 px. At 768 px, the navigation became horizontal, the checkbox and “Forgot password?” appeared side by side, and the two bottom buttons formed a row. At 1024 px, the brand panel and login card formed two columns, the footer changed to three columns, and the welcome heading became larger with the extra list visible. At 1280 px, the content became centered with a maximum width of 1200 px. No broken layouts or horizontal scrolling appeared at the tested widths between 360 px and 1280 px.

base.css
> The layout changed at 768px, 1024px, and 1280px. At 768px, the container side padding increased to 2rem, and the brand panel gained more padding. At 1024px, the login layout changed into two columns, the brand panel became left-aligned, the welcome heading increased to 2.5rem, and the perks section became visible. At 1280px, the container was limited to 1200px and centered. No broken layouts or horizontal scrolling were observed between 360px and 1280px.

Screenshots are in `screenshots/` as `360.png`, `768.png`, `1024.png`, `1280.png`.

## What our group learned (leader writes this last)

> Our group learned how to create a responsive, mobile-first website using CSS Flexbox, Grid, and media queries. We also learned the importance of testing different screen sizes, using GitHub for collaboration, and making sure the layout works properly on mobile phones, tablets, and desktops.


## Part 2: Backend Login and Frontend Integration

Part 2 connects the existing CampusConnect React and TypeScript login page to a Node.js and Express backend. The frontend validates the form, sends the credentials to the API, and displays the result returned by the backend. The backend stores demo users in an in-memory list, checks passwords with bcryptjs, and issues a JWT that expires after one hour.

The Part 1 CSS-only restrictions above describe the earlier activity. Part 2 permits changes to the React/TypeScript files while keeping the mobile-first layout and plain CSS.

### How to run both applications

Use Node.js 22.12 or newer with npm. Open the project folder in VS Code. The project root is the folder containing `src/`, `server/`, and the frontend `package.json`.

Both applications must run at the same time in separate terminals.

#### 1. Start the backend — Terminal 1

Starting from the project root:

```cmd
cd server
npm install
```

On first setup, create the backend environment file:

```cmd
Copy-Item .env.example .env
```

The backend template is [server/.env.example](server/.env.example). Edit the new `server/.env` file to contain:

```dotenv
PORT=3000
JWT_SECRET=replace-with-your-generated-random-secret
CLIENT_ORIGIN=http://localhost:5173
```

Generate a random secret with:

```cmd
node -e "console.log(require('node:crypto').randomBytes(32).toString('hex'))"
```

Paste the entire generated value after `JWT_SECRET=`. The backend requires at least 32 characters. Keep this actual secret in `server/.env`; do not place it in the frontend or commit it to GitHub.

Start the API:

```cmd
npm start
```

Expected terminal message:

```text
API running on http://localhost:3000
```

Check [http://localhost:3000/api/v1/health](http://localhost:3000/api/v1/health). The expected response is status **200 OK** with:

```json
{ "status": "ok" }
```

Leave Terminal 1 running.

#### 2. Start the frontend — Terminal 2


Open another terminal in the project root, alongside the frontend `package.json`. Do not run these commands inside `server/`.

```cmd
npm install
```

On first setup, create the frontend environment file:

```cmd
Copy-Item .env.example .env
```

The frontend template is [.env.example](.env.example). The root `.env` must contain:

```dotenv
VITE_API_URL=http://localhost:3000/api/v1
```

Start the frontend on the port allowed by the backend:

```cmd
npm run dev -- --port 5173 --strictPort
```

Open [http://localhost:5173](http://localhost:5173).

| Application | Command location | Start command | Address |
| --- | --- | --- | --- |
| Backend | `server/` | `npm start` | `http://localhost:3000` |
| Frontend | Project root | `npm run dev` | `http://localhost:5173` |

Create the `.env` files only on first setup; keep existing configured values when restarting the project. Restart the relevant application after changing its `.env`. If port 5173 is occupied, stop the older frontend process before starting another instance.

#### Environment file summary

| Template committed to the repository | Local file created from it | Settings |
| --- | --- | --- |
| [.env.example](.env.example) | `.env` in the project root | `VITE_API_URL` |
| [server/.env.example](server/.env.example) | `server/.env` | `PORT`, `JWT_SECRET`, `CLIENT_ORIGIN` |

The real `.env` files stay on each member's computer and are ignored by Git. The `.env.example` files provide the shared setup templates.

The root `.gitignore` must allow the example templates while ignoring the real settings. Keep these entries in this order:

```gitignore
node_modules
dist
.DS_Store
*.log
.env

```

#### Required demo account

| Field | Value |
| --- | --- |
| Email | `student@campusconnect.test` |
| Password | `Campus26` |
| Name | `Demo Student` |

Use this fake classroom account for the demo. A correct login should display **Welcome, Demo Student** and the user's email from the API response.

#### Frontend build check

From the project root, run:

```cmd
npm run build
```

This checks TypeScript and creates the production frontend files. Resolve any build errors before submitting the project.

### API summary

Local API base URL: `http://localhost:3000/api/v1`.

| Method | Endpoint | Purpose | Success | Expected errors |
| --- | --- | --- | --- | --- |
| GET | `/api/v1/health` | Check that the API is running | `200` with `{ "status": "ok" }` | None in the normal contract |
| POST | `/api/v1/sessions` | Check login credentials and issue a token | `200` with `token` and `user` | `400` for missing or malformed fields; `401` for incorrect credentials |
| GET | `/api/v1/users/me` | Return the authenticated user | `200` with the user's `id`, `name`, and `email` | `401` for a missing, invalid, or expired token |

For `/api/v1/users/me`, send the token using `Authorization: Bearer <token>`.

See the complete [API specification](docs/API-SPEC.md) for request and response examples and the events resource design.

### Who did what in Part 2

| Member | Name | GitHub username | What I did in Part 2 |
| --- | --- | --- | --- | --- |
| 3 | Gervy J. Rosario | gervy121404 | Configured the frontend API address using the root `.env` and `.env.example`. Added `src/api/auth.ts` with `login()` and `getMe()` functions using fetch. Updated `src/components/LoginForm.tsx` to keep the original form validation, send valid-shaped credentials to the backend, and display Loading, Success, and Error states. Added the Welcome screen using the name and email returned by the API. Saved the token in sessionStorage, restored the user on refresh through `/users/me`, removed rejected tokens, and implemented Log out. Added `src/styles/auth.css` for the new messages and Welcome screen and imported it in `src/main.tsx`. |

