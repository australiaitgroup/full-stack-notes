# React Part 7

## Table of Contents

- [Thinking in React](#thinking-in-react)
- [React Developing Procedure](#react-developing-procedure)
- [Team Work](#team-work)
- [React Debug](#react-debug)
- [Git and GitHub](#git-and-github)
- [Additional Tips](#additional-tips)

## Thinking in React

- **Application** -> **Component** -> **Different State** -> **State Data Flow** -> **UI**

## React Developing Procedure

1. **Step 1:** Break the UI into a component hierarchy
2. **Step 2:** Build a static version in React
3. **Step 3:** Find the minimal but complete representation of UI state
4. **Step 4:** Identify where your state should live
5. **Step 5:** Add inverse data flow

## Team Work

1. **Challenges for Junior Developers:**

   - Junior developers may not be aware if they meet the standards.
   - Emphasis on teamwork rather than focusing solely on technical details.

2. **Approach:**

   - Divide work into epics, stories, and tasks. Break down further for team collaboration.

     - **Step 1:** Break the UI into a component hierarchy.

       - Avoid over-engineering; only divide parts that are ready for development, which usually isn't the entire website.
       - **Question:** If avoiding over-engineering, how do we address potential reusable components in the future?
       - **Answer:** Ensure components are readable, maintainable, and reusable by following SOLID principles, allowing for future adaptability.

       ```txt
       Example:

       - APP
         - Header
           - Logo
           - Button (Post a task)
           - Navigation
           - Authentication
           - Button (Become a Tasker)
         - Banner
           - BackgroundImage
           - Button (Post your task)
           - Button (Earn money as a Tasker)
           - AirtaskData

       Reusable component:
         - Button
       ```

       **Workflow Example:**

       ```
       From:
         -> Alice: Story 1, Bob: Story 2;

       To:
         -> Alice: Button, Bob: Banner (background image);
         -> Alice: PR for Button, Bob: Review, Team: Merge;
         -> Bob: Merge main into local branch, use Button for Banner;
       ```

       - Junior developers should perform at 80% of a senior developer's performance, using straightforward routines.

     - **Step 2:** Build a static version in React.
       - Focus on styling without interaction or functionality.
         - CSS + HTML
         - Use reset CSS (reset-css) and Normalize.css
       - Reuse components and props.
         - For static differences (not user interaction): use props.
           - Content differences: props
           - Style differences: props, states
             - Modifier in BEM
             - Memorize and frequently refer to MUI documentation (variants, colors, sizes, states like isActive, isDisabled, etc.)
             - Classname library
         - For dynamic differences: use state.

## React Debug

- Learn common bugs:
  - Not defined
  - Not found
  - ...

## Git and GitHub

- **Protocols:**

  - Git
  - SVN

- **Products:**
  - GitHub
  - Bitbucket
  - **Note:** Git ≠ GitHub

## Additional Tips

- Avoid giving a black-and-white answer in interviews; never directly answer with "no."
- When writing code in a team, write readable and maintainable code even if you don't need to consider others' work.
- Packages to consider: react-icon, classnames
- When encountering repetitive code, deduplicate it. Aim to implement all reuse as components rather than variables, ensuring each file contains only one component.
- As a junior developer, aim to write code like a senior developer and fully understand the SOLID principles.
