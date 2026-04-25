## Beekeepr Glossary
A reference for every project-specific term, abbreviation, or piece of jargon that might trip up a newcomer. Alphabetical. Keep entries short, for the deep version, see the annotated bibliography or backend/docs.md.

## A
Access Token — A short-lived JWT sent with every authenticated API request. Lives in a cookie. See accessId.
accessId — A version number stored on the user's Account record and embedded in their access token. If they don't match, the token is rejected. Bumping this number invalidates all existing access tokens for that user.
Account — The user record. Defined in backend/models/accounts.model.js. Stores email, phone, password hash, and token version numbers.
ACID — Atomicity, Consistency, Isolation, Durability. A set of properties traditional SQL databases guarantee for transactions. NoSQL (MongoDB) trades some of these for flexibility.
Alpine (Linux) — A super lightweight Linux distribution (~5MB) used as the base for our Docker images. Keeps containers small and fast.
Apiary — A location where beehives are kept. In Beekeepr, a top-level entity a user owns; will contain multiple Hives.
API — Application Programming Interface. In our case, the set of HTTP endpoints the frontend calls (like POST /api/auth/login).
API Layer — The topmost layer of the backend (backend/app.js). Mounts routes and applies global middleware. Don't put business logic here.
Argon2 — A password hashing algorithm. Won the Password Hashing Competition; current gold standard. We use it via the argon2 npm package.
Atlas → see MongoDB Atlas.

## B
Bottom Tabs — The five-tab navigation bar at the bottom of the app (Home, HiveTracker, ApiaryManager, Almanac, Community). Powered by @react-navigation/bottom-tabs.

## C
CD — Continuous Deployment (or Delivery). Automatically pushing tested code to production (or to a staging environment).
CI — Continuous Integration. Automatically running tests/lint/build on every push.
CI/CD — Both of the above, together. Our pipeline lives in .github/workflows/ci-cd.yml.
Collection — In MongoDB, the equivalent of a SQL table. A group of documents. Our main collection is accounts.
Component — A reusable piece of UI in React/React Native. Function components (using hooks) are the standard.
Context API — React's built-in way to share state across components without passing props down manually. We use it instead of Redux.
Controller Layer — Backend layer (backend/controllers/) that handles the HTTP contract: reads the request, calls a service, sends the response. No business logic here.
Coverage Threshold — The minimum percentage of code that must be exercised by tests. Ours is 40% — CI fails if it drops below.

## D
Data Layer — Backend layer (backend/models/) that defines Mongoose schemas and talks to the database.
Deep Link — A URL that opens a specific screen inside the app (e.g., beekeepr://hive/123). Handled via expo-linking.
Document (MongoDB) — A single record in a collection. Stored as JSON-like data (technically BSON). The MongoDB equivalent of a SQL row.
Docker — A tool for running apps in lightweight, isolated "containers" so they behave the same on any machine.
Docker Compose — A tool for running multiple Docker containers together. Our docker-compose.yml brings up the frontend and backend at once.
dotenv — An npm package that loads variables from a .env file into process.env.

## E
.env — A file holding secret config values (DB URIs, JWT signing keys). Listed in .gitignore. Never commit this.
ESLint — A linter that catches code style issues and common bugs automatically. Config: eslint.config.js.
Expo — A framework on top of React Native that simplifies setup, builds, and access to native features. We use SDK 54.

## F
Flat Config (ESLint) — The newer ESLint config format (eslint.config.js) replacing the older .eslintrc style.
Flexbox — The layout system used by React Native (and modern CSS). Arranges items in rows or columns.

## H
Hive — A single beehive within an Apiary. A future entity in the data model.
HiveLog — A record of an inspection or event for a specific Hive. A future entity.
Hook (Mongoose) — A function that runs automatically before or after a database operation. Example: our pre('save') hook auto-hashes passwords before they're saved.
Hook (React) — A function like useState, useContext, or useEffect that lets you "hook into" React features from a function component.

## I
In-Memory MongoDB → see mongodb-memory-server.
Instance Method — A method attached to a single document (not the whole model). Example: account.validatePassword('foo').

## J
Jest — Our test runner and assertion library. Config: jest.config.js.
Joi — A library for validating and sanitizing incoming request data. Schemas live in backend/validators/.
JSON — JavaScript Object Notation. The data format used everywhere — API requests, responses, MongoDB documents.
JWT — JSON Web Token. A signed, stateless token used for authentication. Pronounced "jot." Has three parts (header, payload, signature) separated by dots.

## L
LTS — Long Term Support. The stable, supported-for-years version of a piece of software. We use Node 20 LTS.

## M
Middleware — A function that sits in the request/response pipeline in Express. Runs in the order it's registered. Examples: logging, validation, auth checking, error handling.
Model (Mongoose) — A class wrapping a MongoDB collection, with methods like .findOne(), .save(), .updateOne(). Defined in backend/models/.
MongoDB — Our database. Document-oriented and NoSQL.
MongoDB Atlas — The cloud-hosted version of MongoDB. We use it for production.
mongodb-memory-server — A library that spins up a real MongoDB instance in memory for tests. Lifecycle managed in backend/__tests__/setupTests.js.
Mongoose — Our ODM (Object Data Mapper) for MongoDB. Provides schemas, models, hooks, and validation.

## N
Native Stack Navigator — A React Navigation navigator that manages a stack of screens (push/pop) using each platform's native UI primitives.
Node.js — A runtime that lets JavaScript run outside a browser, on a server. We use Node 20 LTS.
NoSQL — "Not only SQL." A category of databases that don't use the traditional table/row/column model. MongoDB is one example.
npm — Node Package Manager. Installs JS dependencies and runs scripts defined in package.json.

## O
ODM — Object Data Mapper. The thing that translates between JS objects and database documents. Mongoose is our ODM.

## P
pre('save') Hook — A Mongoose middleware function that runs before a document is saved. Used in our Account model to hash passwords automatically.
Prop Drilling — Passing data down through many layers of components via props just to get it to a deep child. Annoying. The Context API solves this.

## R
React — The JavaScript library for building UIs out of components. We're on React 19.
React Native — A framework that lets you build mobile apps using React. Renders to native iOS/Android UI elements. We're on 0.81.
React Navigation — The standard routing/navigation library for React Native apps. Version 7.
Redux — A popular state management library (we don't use it — we use Context API instead).
Refresh Token — A longer-lived JWT used only to get a new access token when the current one expires. See refreshId.
refreshId — A version number stored on the Account record and embedded in the refresh token. Bumping it invalidates all of a user's refresh tokens.
REST — REpresentational State Transfer. The architectural style our API follows. Endpoints map to nouns (resources) and HTTP verbs (GET, POST, PATCH, DELETE) map to actions.
Routing Layer — Backend layer (backend/routers/) that defines endpoint paths and applies route-specific middleware.

## S
Schema (Mongoose) — A definition of what fields a document has, their types, and their constraints. Enforced before the document hits the database.
Service Layer — Backend layer (backend/services/) holding business logic. Doesn't know HTTP exists. The layer you change if a rule changes.
Sparse Unique Index — A MongoDB index that enforces uniqueness, but only for documents where the field exists. Used on phone in Account so multiple users can have no phone, but no two users can have the same phone.
Stack Navigator — See Native Stack Navigator.
State — Data that changes while the app is running (logged-in user, current theme, form input values).
StyleSheet — React Native's API for defining styles as JS objects (StyleSheet.create({...})).
Strict Mode (TypeScript) — A compiler setting that enforces stricter type-checking (no implicit any, null-safety, etc.). We have it on.
Supertest — A library for testing Express routes without actually starting a server. Used alongside Jest in our backend tests.

## T
Tab Bar — See Bottom Tabs.
Theme — The active color palette (light or dark). Defined in src/styles/colors.ts, provided through ThemeContext.
ThemeContext — Our React Context that holds the active theme. See src/Contexts/ThemeContext.tsx.
Token Revocation — Invalidating a user's tokens. We do this by bumping accessId or refreshId on their Account record — any token with the old version is now rejected.
tsc — The TypeScript compiler command. We run tsc --noEmit in CI to type-check without producing JS output.
TypeScript — A statically typed superset of JavaScript. Catches type errors before the app runs.

## U
useContext — The React hook that reads a value from a Context.
useEffect — The React hook that runs side effects (data fetching, subscriptions, timers) after a render.
useState — The React hook that adds state to a function component.

## V
Validation Layer — Backend layer (backend/validators/) that runs Joi schemas on incoming requests before the controller sees them.
validatePassword() — Instance method on Account documents that does a constant-time comparison between a plaintext password and the stored Argon2 hash.
Virtual (Mongoose) — A field on a document that doesn't get saved to the DB — it's computed on read. Our id virtual exposes MongoDB's _id as a clean hex string.

## Z
Zero-Warnings Mode (ESLint) — Running ESLint with --max-warnings 0. Any warning is treated as a failure. CI runs lint this way, so warnings block merges.