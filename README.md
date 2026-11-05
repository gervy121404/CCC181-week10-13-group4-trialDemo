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
| Group number | |
| Section | |
| Repository URL | |

## Members (each member fills in their own row in their own commit)

| Member | Name | GitHub username | CSS file | What I did |
| --- | --- | --- | --- | --- |
| 1 (leader) | | | `base.css` | |
| 2 | Kent T. Baloyos | itItsken-the-average | `nav.css` | Wrote src/styles/nav.css (Flexbox + Grid) using a mobile-first approach, in 3 commits: phone layout with a stacked navbar, 48px (3rem) links and a 1-column footer grid, brand left with links in one row from 768px, and a 3-column footer from 1024px. Reviewed the base.css pull request. |
| 3 | Gervy J. Rosario | gervy121404 | `form.css` | Wrote src/styles/form.css (Flexbox) using a mobile-first approach, in 4 commits: phone layout with stacked 48px (3rem) fields and buttons, side-by-side checkbox row and buttons from 768px, and roomier card from 1024px. Reviewed the nav.css pull request. |

## Experiment 0: the page without the viewport tag

What did the page look like in DevTools phone mode **before** adding the viewport meta tag?
What changed **after** adding it?

> 

## DevTools test results

| Width | What must be true | Pass? |
| --- | --- | --- |
| 360 px | 1 column. Nav links stacked and 48px tall. Options and buttons stacked. Footer in 1 column. No sideways scrollbar. ||
| 768 px | Nav in one row (brand left, links right). Checkbox and link in one row. Two buttons side by side. ||
| 1024 px | Brand panel and login card side by side. Footer in 3 columns. Heading is larger. ||
| 1280 px | Content centered and stops at 1200px. ||

### Breakpoints I observed

Using **Show media queries** and dragging slowly from 360 px to 1280 px, the layout changed at these exact widths:

>The layout changed at 768 px, 1024 px, and 1280 px. At 768 px, the navigation became horizontal with the brand on the left and the links in one row, the container side padding grew to 2rem, the checkbox and “Forgot password?” appeared side by side, and the two bottom buttons formed a row. The login card also became centered with a maximum width of 32rem. At 1024 px, the brand panel and login card formed two columns, the footer changed to three columns, and the welcome heading became larger (2.5rem) with the extra list visible. The login card also got roomier padding (2.5rem). At 1280 px, the content became centered with a maximum width of 1200 px. No broken layouts or horizontal scrolling appeared at the tested widths between 360 px and 1280 px.

> The layout changed at 768 px, 1024 px, and 1280 px. At 768 px, the navigation became horizontal, the checkbox and “Forgot password?” appeared side by side, and the two bottom buttons formed a row. At 1024 px, the brand panel and login card formed two columns, the footer changed to three columns, and the welcome heading became larger with the extra list visible. At 1280 px, the content became centered with a maximum width of 1200 px. No broken layouts or horizontal scrolling appeared at the tested widths between 360 px and 1280 px.

Screenshots are in `screenshots/` as `360.png`, `768.png`, `1024.png`, `1280.png`.

## What our group learned (leader writes this last)

> (write your answer here)
