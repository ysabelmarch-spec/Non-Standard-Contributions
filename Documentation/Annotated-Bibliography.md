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

>> REACT NAVIGATION

>> STATE MANAGEMENT

>> THEMEING/STYLEEESSS