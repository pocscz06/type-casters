
# Type Casters

This is a lightweight application to test and analyze user typing speed, accuracy, and averages.


## Table of Contents
- [Documentation](#Documentation)
- [Overview](#Overview)
- [Optimizations](#Optimizations)
- [Screenshots](#Screenshots)
- [Tech Stack](#Tech)
- [Installation](#Installation)
- [Authors](#Authors)
- [License](#License)

## Documentation

[Documentation link to docusaurus/confluence documentation page](https://linktodocumentation)


## Overview

Users will be able to:

- Login/Register with form validation
- Enter a landing page containing a global navbar that links to different modes of typing tests and challenges.
- Two current modes: dictionary and standard.
  - Dictionary: Uses a random word generator API from Vercel to generate an infinite chain of words for the user to type under a specified timer.
    - https://random-word-api.vercel.app/
  - Standard: Uses a random quotes generator API from They Said So to generate a quote of fixed length for the user to type under the same specified timer. 
    - https://quotes.rest/ 
-  The user can complete these tests/challenges on a desktop keyboard or a mobile keyboard.
- A statistics page will be available that documents the user's average wpm (words per minute), accuracy score, and a chart graphing trends of the statistics per typing test attempt during the current user session.

## Optimizations

What optimizations did you make in your code? E.g. refactors, performance improvements, accessibility


## Screenshots

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)



## Tech Stack

Frontend:
- HTML
- CSS
- JS
- Svelte bootstrapped with Vite

Backend:
- TBD

Utilities:
- Autoprefixer plugin for automated CSS vendor prefixing
- ESLint *probably* using our own custom configuration
- Jest for testing
- esbuild (Vite default) for transpilation and development building
-  Rollup for production bundling

Accessibility & Performance:
- Google Lighthouse for generating reports on SEO, Performance, and Accessibility
- NVDA for keyboard-only accessibility testing
- WAVE for WAI-ARIA guideline adherence

## Installation

Install my-project with npm

```bash
  npm install my-project
  cd my-project
```
    
## Authors

- [Kenny Pham](https://www.github.com/pocscz06)
- [Samuel Kim](https://www.github.com/skimlox)

## License

This project is licensed under the [GNU General Public License v3](https://www.gnu.org/licenses/gpl-3.0.en.html#license-text)