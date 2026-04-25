# Annotated Bibliography

What am I? I'm a living document where I (a total beginner) am trying to make sense of the Beekeepr project. I'm writing this partly so future me doesn't forget what any of this stuff does, and partly so the next confused new contributor has a friendlier place to start than the official docs.What are my sections?Sections:

1. Front End
2. Back End
3. Database
4. MISC

# Organization

This bibliography is organized into distinct sections (Front End, Back End, Database, and MISC) to reflect project architecture while allowing room for non-distinct contributions or notions. These sections are further broken down to discuss specific aspects/languages/frameworks/functions, link to external learning resources, and include my own notes.

# Section 1: Front End

The front end is what the user actually sees and taps on. For Beekeepr, that's an app that runs on iPhones, Androids, AND in a web browser all from the same code. t's built with React Native + Expo and written in TypeScript. There's a bottom tab bar with five sections: Home, HiveTracker, ApiaryManager, Almanac, and Community (AT THE TIME OF WRITING).

>> TYPE SCRIPT

Type-script is basically java-script but stricter, to my understanding. Every file ending in .ts or .tsx in the src/ folder is TypeScript. The project runs in "strict mode," which means you can't be lazy about things like null-checking. 

Example: When I'm writing a component that uses an Apiary object, TypeScript already knows what fields an Apiary has (they're defined in src/@types/). If I typo apiary.naem instead of apiary.name, it tells me immediately.

Learning Resources:

- Official TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/intro.html
- TypeScript in 5 Minutes (short intro): https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html
- freeCodeCamp "Learn TypeScript – Ultimate Beginner's Guide" (great for JS devs): https://www.freecodecamp.org/news/learn-typescript-beginners-guide/

>> REACT & REACT NATIVE

React is a library for building UIs out of little reusable pieces (components). Instead of one giant HTML file, you write components like <HiveCard /> and snap them together. React Native is the same idea but for mobile — instead of HTML tags like <div>, you use things like <View> and <Text> that turn into actual native iOS/Android UI.
The project is on React 19 and React Native 0.81. Every screen in src/screens/ is a function component using hooks (useState, useContext, useEffect). TLDR: This is what allows the app to be functional across platforms (web, IOS, Android...)

Learning Resources:

- React docs (interactive, genuinely the best way to learn): https://react.dev/learn
- React Native docs: https://reactnative.dev/docs/getting-started
- React hooks reference: https://react.dev/reference/react
- dev.to "What Are React Hooks? A Beginner-Friendly Guide" (plain English, with examples): https://dev.to/harsh_p30/what-are-react-hooks-a-beginner-friendly-guide-with-examples-1c3g

>> EXPO

Expo is a layer on top of React Native that does all the annoying setup for you. Without Expo, to use the camera you'd have to write platform-specific code for iOS and Android separately. With Expo, you just import { Camera } from 'expo-camera' and it works.
The project uses Expo SDK 54. You start the app with npm start, which boots up the Expo dev server.
Some Expo packages we use:

expo-location — for GPS (finding local apiaries)
expo-splash-screen — that loading screen when the app opens
expo-linking — deep links (like beekeepr://hive/123)

Learning Resources:

- Expo docs (start here for setup): https://docs.expo.dev
- Expo SDK reference: https://docs.expo.dev/versions/latest/
- dev.to "Expo vs Bare Workflow: Which Should You Choose?" (beginner-friendly comparison): https://dev.to/lucas_wade_0596/react-native-expo-vs-bare-workflow-which-should-you-choose-47lo

>> REACT NAVIGATION

This is how you move between screens. It's not built into React Native, it's a separate library. There are two kinds we use:

Stack Navigator — like a stack of papers. You "push" a new screen on top when you drill into something (e.g., tapping a hive to see its details), and "pop" it off to go back.
Bottom Tabs — the five-tab bar at the bottom of the app.

The whole navigation tree is wired up in src/navigation/AppNavigator.tsx. Each tab has its own stack in src/navigation/stacks/.

Learning Resources:

- React Navigation docs: https://reactnavigation.org/docs/getting-started
- Stack Navigator: https://reactnavigation.org/docs/native-stack-navigator
- Bottom Tabs: https://reactnavigation.org/docs/bottom-tab-navigator

>> STATE MANAGEMENT

"State" = data that changes while the app is running (like the logged-in user, or dark mode on/off). The tricky part is sharing that data across a bunch of components without passing it down as props through every single layer (this is called "prop drilling" and apparently).
Bigger projects often use Redux for this, but Beekeepr uses React's built-in Context API instead, which is simpler. There are two contexts:

AuthContext — holds the logged-in user
ThemeContext — holds the current theme (light/dark mode)

Both wrap the whole app in src/App.tsx, so any component anywhere can just call useContext(AuthContext) and get the current user. Very cool.

Learning Resources:

- React Context docs: https://react.dev/learn/passing-data-deeply-with-context
- useContext hook: https://react.dev/reference/react/useContext
- Medium "React Context API vs Redux: A Beginner's Perspective": https://medium.com/@bernardtambo40/react-context-api-vs-redux-a-beginners-perspective-3244cd83fa2a

>> THEMEING/STYLEEESSS

All colors live in one file: src/styles/colors.ts. It defines a light theme and a dark theme, both using semantic names like primary, danger, success — not hex codes like #FF5733 scattered all over the app. That way if we ever want to change the primary color, we change it once.
Styles themselves use React Native's StyleSheet.create() — kind of like CSS but as JavaScript objects. Layout uses Flexbox, same as web.

Learning Resources:

- StyleSheet: https://reactnative.dev/docs/stylesheet
- Flexbox in React Native: https://reactnative.dev/docs/flexbox
- CSS-Tricks "A Complete Guide to Flexbox" (the definitive reference): https://css-tricks.com/snippets/css/a-guide-to-flexbox/

# Section 2: Back End

The back end is the server that the app talks to over the internet. When I tap "log in" in the app, it sends my email/password to the back end, which checks the database and sends back a token. The back end is a REST API built with Node.js + Express, running on port 3000.
Entry point: backend/server.js (connects to DB, starts server). App logic: backend/app.js (middleware + routes).

Important: there's a file at backend/docs.md written by the original backend author that does a much deeper architectural walkthrough. 

>> Node.js

Node.js lets JavaScript run outside the browser — on a server. That's basically it. Before Node, JS was a browser-only language. Now it runs pretty much everywhere. The project uses Node 20 (LTS = Long Term Support, the stable version).

Learning Resources:

- Node.js docs: https://nodejs.org/en/docs
- Node.js beginner guide: https://nodejs.dev/en/learn/
- freeCodeCamp "What Exactly is Node.js? Explained for Beginners": https://www.freecodecamp.org/news/what-is-node-js/

>> Express

Express is a framework that makes building a web server in Node way less painful. It handles:

* Parsing incoming JSON (so we can actually read what the app sent)
* Parsing cookies
* Matching URLs to handler functions (routing)
* Running middleware in order (logging → validating → auth → controller)
* Catching errors globally

Middleware order matters a lot. The error-handling middleware has to be registered last in backend/app.js — otherwise it won't catch errors from the stuff that runs after it.
Current endpoints:

* POST /api/auth/login
* POST /api/auth/refresh
* POST /api/auth/logout
* GET/POST/PATCH/DELETE /api/accounts

Learning Resources:

- Express docs: https://expressjs.com/en/5x/api.html
- Express routing: https://expressjs.com/en/guide/routing.html
- Express middleware: https://expressjs.com/en/guide/using-middleware.html

>> 6-Layer Architecture

This is the part I had to read backend/docs.md for. The back end is split into six layers, each with ONE job. When we're writing new code, we have to figure out which layer it belongs in:

* API Layer (app.js) — wires up routes and global middleware
* Routing Layer (backend/routers/) — defines endpoint paths
* Validation Layer (backend/validators/) — checks request input (Joi)
* Controller Layer (backend/controllers/) — handles the HTTP stuff (read request, send response)
* Service Layer (backend/services/) — the actual business logic (doesn't know HTTP exists)
* Data Layer (backend/models/) — talks to the database (Mongoose)

The big idea: if I want to change how passwords get hashed, I only touch the service layer. The controller, router, and validator don't care and don't change. This is called "separation of concerns".

Learning Resources:

- backend/docs.md in this repo — genuinely the best resource
- MVC / layered architecture: https://developer.mozilla.org/en-US/docs/Glossary/MVC
- dev.to "Layered Architecture: A Beginner's Guide to Structuring Software Systems" (uses a burger metaphor, I'm into it): https://dev.to/aznaxdev/layered-architecture-a-beginners-guide-to-structuring-software-systems-4omm

>> Authentication 

When I log in, the server gives me two tokens:

Access token — short life, sent with every request
Refresh token — longer life, only used to get a new access token when the old one expires

Both tokens have a version number (accessId, refreshId) stored in my user record. If we ever need to kick me out of all my sessions, we just bump the version number and any token with the old version is now invalid. Clean.
Passwords are hashed with Argon2 before being stored.  

Learning Resources:

- JWT intro + playground: https://jwt.io/introduction
- Argon2 on Wikipedia: https://en.wikipedia.org/wiki/Argon2
- OWASP password storage cheatsheet: https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html
- dev.to "JWT explained in 4 minutes (With Visuals)": https://dev.to/jaypmedia/jwt-explained-in-4-minutes-with-visuals-g3n

>> JOI (Validation)

Joi is a library that checks if incoming data is the right shape before it hits the controller. Every endpoint has a Joi schema in backend/validators/. If someone sends a request with a missing field or a malformed email, Joi rejects it at the door and the database never even gets pinged.
The "fail early" pattern means less junk in the database and way fewer mystery bugs.

Learning Resources:

- Joi docs: https://joi.dev/api
- Schema builder tutorial: https://joi.dev/tutorials/schema-builder

>> Error Handling

The project has custom error classes in backend/classes/ (like NotFoundError, UnauthorizedError) and a global error middleware in backend/middlewares/error.middleware.js. This means any layer can just throw new NotFoundError(...) and the middleware automatically turns it into the right HTTP status code and JSON response. No try/catch boilerplate in every controller. 

# Section 3: Database

A database is just where we save data so it doesn't disappear when the server restarts. Beekeepr uses MongoDB (the database itself) and Mongoose (a JS library that makes MongoDB easier to work with). In production, the database is hosted on MongoDB Atlas (cloud). In tests, we spin up a fake in-memory database that dies when tests finish.

>> MongoDB (NOT SQL)

MongoDB is a NoSQL database. Instead of tables with rows and columns (like SQL / PostgreSQL / MySQL), it stores data as JSON-ish documents in "collections." So instead of:
| id | email          | password |
| 1  | me@example.com | hash...  |

...you get:
json{ "_id": "...", "email": "me@example.com", "password": "hash..." }

The main collection right now is accounts (users).

The DB connection is handled in backend/utils/connectDb.js. It reads the connection URI from environment variables: MONGO_TEST for dev, MONGO_PROD for production.

Learning Resources:

- MongoDB docs: https://www.mongodb.com/docs/manual/
- MongoDB University (free courses, genuinely good): https://learn.mongodb.com
- Built In "SQL vs. NoSQL: What's the Difference?" (beginner-friendly comparison): https://builtin.com/data-science/sql-vs-nosql

>> Mongoose

Mongoose is the layer between our Node code and MongoDB. It gives us:

Schemas —-> you define the shape of a document (required fields, types, unique constraints) and Mongoose enforces it
Models —-> basically a class wrapping a collection, with methods like .findOne() and .save()
Hooks —-> functions that run before/after certain operations. The Account model has a pre('save') hook that auto-hashes passwords before saving —-> so we can never accidentally save a plaintext password
Instance methods —-> like validatePassword() on an Account document
Virtuals —-> the id virtual exposes MongoDB's _id as a clean string

The Account schema:
Field      Type          Notes
 email      String        Required, unique, lowercase
 phone      String        Optional, sparse unique index
 password   String        Argon2 hash, excluded from queries by default
 refreshId  Number        Token version for revocation
 accessId   Number        Token version for revocation

Learning Resources:

- Mongoose docs: https://mongoosejs.com/docs/guide.html
- Mongoose validation: https://mongoosejs.com/docs/validation.html
- Mongoose middleware: https://mongoosejs.com/docs/middleware.html

>> MongoDB (Atlas)

Atlas is MongoDB's cloud hosting service. It does replication, backups, scaling, and security so we don't have to run our own MongoDB server somewhere. The connection string is a secret. It lives in the MONGO_PROD environment variable and is never committed to the repo.

Learning Resources:

- Atlas quickstart: https://www.mongodb.com/docs/atlas/getting-started/
- Twelve-Factor App (config): https://12factor.net/config

>> MondgoDB (Memory Server/Testing)

This library spins up a real MongoDB instance in memory for tests w/ no external dependencies, no leftover test data. The lifecycle is in backend/__tests__/setupTests.js:

Starts before any tests run
Clears all collections between tests (so tests don't interfere)
Shuts down after all tests finish

The team specifically chose this over mocking the database. Mocks can drift from real MongoDB behavior and let real bugs slip through. Testing against a real (but in-memory) DB catches more.

Learning Resources:

- mongodb-memory-server: https://github.com/nodkz/mongodb-memory-server
- Kent C. Dodds on why not to mock: https://kentcdodds.com/blog/testing-implementation-details

# Section 4: MISC STUFF IDK

This section = testing, CI/CD, Docker, linting, and all the other infrastructure that isn't specifically front-end or back-end.

>> Jest (Testing Framework)

Jest is the test runner. Tests live in __tests__/ folders next to the code they test. Config is in jest.config.js.
Key config:

20-second test timeout (because in-memory MongoDB takes a sec to spin up)
40% coverage threshold — if coverage drops below 40%, CI fails
Runs setupEnv.js (loads .env) and setupTests.js (DB lifecycle) before tests

Helpers in backend/__tests__/helpers.js:

registerUser() — creates a test user + returns auth tokens
withAuth(request, tokens) — attaches auth cookies to a Supertest request

Learning Resources:

- Jest docs: https://jestjs.io/docs/getting-started
- Jest matchers: https://jestjs.io/docs/expect
- freeCodeCamp "How to Test Your Express.js and Mongoose Apps with Jest and SuperTest" (literally our exact stack): https://www.freecodecamp.org/news/how-to-test-in-express-and-mongoose-apps/

>> Supertest (HTTP Testing)

Supertest tests Express routes without actually starting the server. You pass your Express app directly to it and it fakes the HTTP layer internally. Fast, self-contained.
Example pattern we use everywhere:
javascriptconst response = await request(app)
  .post('/api/auth/login')
  .send({ email: 'test@example.com', password: 'secret' });

expect(response.status).toBe(200);

Learning Resources:

- Supertest repo: https://github.com/ladjs/supertest

>> ESLint (Code Quality)

ESLint yells at you when your code is ugly or suspicious. Config is in eslint.config.js (flat config format — newer style). Different rules for different file types:

TypeScript files — TS-specific rules
Backend JS — standard JS rules
Tests — relaxed rules (e.g., jest/no-disabled-tests is allowed in tests so you can skip a broken test temporarily)

CI runs in zero-warnings mode, so any lint warning blocks a merge to main.

Learning Resources:

- ESLint docs: https://eslint.org/docs/latest/
- TypeScript ESLint: https://typescript-eslint.io/getting-started

>> GitHub Actions (CI/CD)

CI = "continuous integration" = automatically running tests/lint/build every time someone pushes code. CD = "continuous deployment" = automatically deploying when stuff passes. Our pipeline is in .github/workflows/ci-cd.yml and runs on every push to main + every PR.
Three jobs in parallel:

Lint — npm run lint (zero warnings)
TypeCheck — npm run typecheck (tsc --noEmit)
Build & Test Coverage — installs Node 20, starts a MongoDB 6 container, runs tests with coverage, enforces the 40% threshold, uploads report as artifact

Secrets (JWT keys, DB URIs) live in GitHub repo secrets and get injected as env vars at runtime. Never committed. Ever.

Learning Resources:

- GitHub Actions quickstart: https://docs.github.com/en/actions/quickstart
- Secrets in Actions: https://docs.github.com/en/actions/security-guides/using-secrets-in-github-actions
- dev.to "CI/CD Tutorial For Developers" (clean beginner walkthrough): https://dev.to/pavanbelagatti/cicd-tutorial-for-developers-3l0

>> Docker & Docker Compose

Docker lets you run your app in a container — a lightweight, isolated environment that behaves the same on every machine. No more "works on my laptop." We have:

Dockerfile.backend — Node 20 Alpine, serves backend on port 3000
Dockerfile.frontend — Node 20 Alpine, runs Expo web on port 8081
docker-compose.yml — brings up both together with env vars from .env

Alpine is a tiny Linux distro (~5MB) — keeps images small and fast.

In class lab also a solid reference for this. 

Learning Resources:

- Docker intro: https://docs.docker.com/get-started/
- Docker Compose: https://docs.docker.com/compose/
- Fireship "Docker in 100 Seconds" (exactly what it sounds like, and exactly enough to start): https://www.youtube.com/watch?v=Gjnup-PuquQ

>> Environment Variables & .env

Secrets don't go in the code. They go in a .env file that's .gitignored (so git ignores it and it never hits the repo). The app reads them via process.env.VARIABLE_NAME. In CI, GitHub Secrets do the same job.
Required env vars:

MONGO_TEST — dev DB connection
MONGO_PROD — production DB connection
ACCESS_SECRET — access JWT signing key
REFRESH_SECRET — refresh JWT signing key
NODE_ENV — development / test / production

Learning Resources:

- Twelve-Factor App (config): https://12factor.net/config
- dotenv package: https://github.com/motdotla/dotenv

>> Figma (Design)

The .figma/ directory at the project root has design assets organized by screen (Home, ApiaryManager, HiveTracker, etc.). These are what the frontend is actually built to match. RPI Students get Figma Premium for free w/ an education plan!

Learning Resources:

- Figma for devs: https://help.figma.com/hc/en-us/articles/360040028114-Getting-started-for-developers

>> npm Scripts Reference

NMP SCRIPTS CHEAT SHEET

npm start --> Start Expo dev server (mobile + web)

npm run web --> Start Expo web only

npm run android --> Build + run on Android
npm run ios --> Build + run on iOS simulator
npm test --> Run Jest
npm run test:coverageRun --> Jest + coverage report
npm run test:ci --> Jest in CI mode (sequential, leak detection)
npm run lint --> Run ESLint (zero warnings)
npm run lint:fixAuto-fix --> lint errors
