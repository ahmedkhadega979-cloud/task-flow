# TaskFlow – Kanban Task Board

A responsive task management board built with **React** and **Vite**. Organize tasks across three columns, drag them between stages, and track your progress. Tasks are saved in the browser, so they survive a refresh.

**Live demo:** _add your GitHub Pages link here_
**Screenshot:** _add a screenshot here (e.g. `docs/screenshot.png`)_

## Features
- Add tasks with a title, priority (high / medium / low), and due date
- Drag and drop tasks between **To do**, **In progress**, and **Done** (move buttons for touch screens)
- Double-click a task title to edit it, or delete it
- Search tasks and filter by priority
- Progress bar and overdue task counter
- Light and dark mode
- Optional accounts: sign in to save tasks on a Node.js/Express + MongoDB API (JWT auth, hashed passwords). Signed out, tasks stay in `localStorage`
- Responsive layout, keyboard focus styles, and reduced-motion support

## Tech stack
Frontend: React 18 (hooks: `useState`, `useEffect`, `useMemo`, a custom `useLocalStorage` hook), Vite, CSS custom properties.
Backend: Node.js, Express, MongoDB (Mongoose), JWT, bcrypt.

## Run locally
Frontend (works on its own, saving tasks in the browser):
```bash
npm install
npm run dev
```
Backend (needed for accounts): create a free MongoDB Atlas cluster, then
```bash
cd server
cp .env.example .env   # add your MONGO_URI and a long random JWT_SECRET
npm install
npm run dev
```
The API runs on `http://localhost:5000`. For a deployed frontend, set `VITE_API_URL` to your API address.

## API
| Method | Route | Description |
| --- | --- | --- |
| POST | `/api/auth/register`, `/api/auth/login` | Returns a JWT |
| GET / POST | `/api/tasks` | List or create your tasks |
| PATCH / DELETE | `/api/tasks/:id` | Update or delete one of your tasks |

## Tests
```bash
npm test
```
Unit tests (Vitest) cover the progress and overdue logic. They also run automatically on every push.

## Deployment
**Frontend (automatic):** push to the `main` branch, then in the repository go to Settings > Pages and set the source to **GitHub Actions**. Each push runs the tests, builds the app, and publishes it. Without an API address, the live demo runs in browser-only mode.

**API (optional, for accounts):** deploy the `server` folder on [Render](https://render.com) using the included `render.yaml`, and add `MONGO_URI` and `CLIENT_ORIGIN` (your Pages address) as environment variables. Then in the repository go to Settings > Secrets and variables > Actions > Variables, add `VITE_API_URL` with your API address (ending in `/api`), and push again.

## Ideas for next steps
- API tests with Supertest
- Share boards between users
