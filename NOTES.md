# Movie Night — Session 1 Lab Notes

## Lab 1 — Scaffold and Explore

### 1. In which file are the `<html>` and `<body>` tags?

They are in `app/layout.tsx`. This is the root layout of the application and wraps all pages.

### 2. Which file renders the page at `/`?

`app/page.tsx` renders the home page at the root URL `/`.

### 3. Which folder is for images and other static files, and how do you reference them?

The `public/` folder stores static files such as images and icons.

Files are referenced from the root URL. For example, `public/next.svg` can be accessed using `/next.svg`.

### 4. What is `tsconfig.json` doing in your project?

It configures TypeScript for the project. It defines compiler options, type-checking behaviour and module resolution.

### 5. What does `@/*` mean in `tsconfig.json`? Write an import that uses it.

`@/*` is an import alias that points to the project root.

Example:

`import { getMovies } from "@/lib/movies";`

This refers to `lib/movies.ts` without writing a long relative path.

### 6. What does `app/layout.tsx` import from `next/font/google`, and what does Next.js do with it at build time?

It imports `Geist` and `Geist_Mono`.

Next.js downloads and self-hosts the font files during the build so the application can serve them locally instead of depending on a browser request to Google Fonts.

### 7. What's the difference between `layout.tsx` and `page.tsx`?

`layout.tsx` defines shared UI that wraps pages in a route segment. It can contain elements such as a header or navbar.

`page.tsx` defines the actual content displayed for a particular URL.

### 8. Where would you put a navbar that appears on every page?

I would put it in `app/layout.tsx`, because the root layout wraps every page in the application.

### 9. What is `globals.css` for, and where is it imported?

`app/globals.css` contains global styles and imports Tailwind CSS.

It is imported in `app/layout.tsx`, so the styles are available throughout the application.

### 10. What is `AGENTS.md`, and does your app need it to run?

`AGENTS.md` provides instructions and project context for AI coding agents working on the project.

The application does not need this file to run. It is guidance for development tools.

---

## Lab 2 — First Server-Rendered Page

### 1. In the page source, are the movie titles present for `/movies`? For `/movies-client`? Why?

For `/movies`, the movie titles are present because the Server Component fetches the data on the server and includes the movie list in the HTML sent to the browser.

For `/movies-client`, the titles are not present in the initial HTML. The page initially contains "Loading movies...". The browser fetches the JSON data inside `useEffect` and displays the titles afterwards.

### 2. Without the `force-dynamic` line, what does the "Rendered at" timestamp show after building tomorrow?

It shows the timestamp from the time the application was built. This is because the page is statically prerendered during `npm run build`. Refreshing the page does not generate a new timestamp.

### 3. Give one situation where `force-dynamic` is the right choice.

A personalized dashboard showing a user's latest account information is a good example. It needs fresh data for every request, so dynamic rendering is appropriate.

### 4. A classmate sees `[movies] rendered 6 movies` in the browser console and says the code runs in the browser. What do you answer, and how can you prove it?

The code still runs on the server. Next.js may show a copy of the log in the browser console as a debugging aid.

I can prove server rendering by checking the terminal, viewing the original HTML source, and disabling JavaScript while the movie titles remain visible.

### 5. Which version would you choose for a public movie catalogue that changes once a week, and why?

I would choose static rendering because the catalogue does not change frequently. The page can be generated at build time and served quickly to visitors.

I can rebuild the application when the catalogue changes, or use Incremental Static Regeneration (ISR) to update it automatically.
