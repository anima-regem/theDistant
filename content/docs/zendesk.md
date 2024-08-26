---
title: "ZenDesk"
date: "2024-08-22"
summary: "ZenDesk, an accessible user query management software based on TruDesk"
# description: ""
toc: true
readTime: true
autonumber: true
math: true
tags: ["gsoc", "accessibility", "web", "zendalona", "final"]
showTags: false
hideBackToTop: false
---

# ZenDesk
---

![A Screenshot of ZenDesk](../../assets/zendesk.png)

## Project Setup

To get started with the custom version of Trudesk (referred to as Zendesk in this context), follow these steps:

### Clone the Repository

Start by cloning the custom Trudesk repository:

```bash
git clone https://github.com/anima-regem/trudesk.git
```

### Install Node.js Version 16.20

Ensure you have Node.js version 16.20 installed. You can use `nvm` (Node Version Manager) to install the required version. If you don't have `nvm` installed, you can follow the [nvm installation guide](https://github.com/nvm-sh/nvm#installing-and-updating).

Once `nvm` is installed, you can install and use Node.js version 16.20:

```bash
nvm install 16.20
nvm use 16.20
```

### Install Yarn and Git

If you haven’t already installed Yarn and Git, you can do so using the following command:

```bash
npm install -g yarn
```

### Install MongoDB

You need MongoDB installed and running to use the Zendesk custom Trudesk project. Follow the official [MongoDB installation guide](https://docs.mongodb.com/manual/installation/) to install MongoDB on your system.

### MongoDB Setup

After installing MongoDB, create an admin user for the Trudesk database:

1. Start the MongoDB shell:

   ```bash
   mongo
   ```

2. Switch to the `admin` database:

   ```bash
   use admin
   ```

3. Create an admin user with the following command:

   ```javascript
   db.createUser({
      user: "trudeskAdmin",
      pwd: "yourPasswordHere",
      roles: [{ role: "userAdmin", db: "trudesk" }]
   })
   ```

Replace `"yourPasswordHere"` with a secure password.

### Install Project Dependencies (Master Branch)

Navigate to the cloned project folder and switch to the master branch:

```bash
cd trudesk
git checkout master
```

Install the project dependencies and run the build:

```bash
yarn install
yarn run grunt
```

### Launch the Application

Once the project is ready, launch the application by going to `http://localhost:8118`. You can then proceed with the web-based installation:

- Provide the credentials for the MongoDB admin user you created earlier.
- Set up a new database or use an existing one.
- If needed, you can create additional users from the master branch (note that signup is not implemented in the Zendesk branch).

### Switch to the Zendesk Branch

After setting up the master branch, stash any changes:

```bash
git stash
```

Then, switch to the Zendesk branch:

```bash
git checkout zendesk
```

### Install Dependencies and Build (Zendesk Branch)

Install dependencies and run the build for the Zendesk branch:

```bash
yarn install
yarn run grunt
```

### Access the Project

You can now go to `http://localhost:8118` to see the project in action.

## Usage

The project provides the following features:

- **Create Tickets**: Users can create support tickets to report issues or requests.
- **Respond to Tickets**: Team members can respond to tickets, providing support or further information.
- **Add Comments to Tickets**: Users and team members can add comments to ongoing tickets for better communication.
- **Update Profile and Settings**: Users can update their profile information and configure their settings.
- **View Dashboard of Tickets**: A dashboard view that shows the status and details of all tickets.
- **Manage Users, Groups, Tags, etc.**: Admins can manage users, groups, and tags to organize and streamline support activities.


## Changes Made from the Original Trudesk

Significant changes were made to enhance accessibility and improve overall functionality from the original Trudesk project. Here’s a summary of the key modifications:

### Aria Live Regions for Dynamic Content
   - The main component of Trudesk is dynamically rendered since it’s a Single Page Application (SPA). To ensure that screen readers properly announce content changes, we implemented an aria-live region. This region announces updates as they occur, improving accessibility for users relying on assistive technologies.

### Keyboard Navigation and Focus Management
   - We made all links and buttons fully navigable using the keyboard. Custom components like accordions, which initially lacked proper keyboard accessibility, were reworked to support navigation using JavaScript events such as `onFocus` and `onClick`.
   - Proper focus management was a priority, ensuring that users can efficiently navigate through the application using the keyboard. This was particularly challenging with custom modals, select components, and tables containing buttons, but we tackled these issues with a combination of JavaScript and careful component design.

### Shadow Components for Announcements
   - Many accessibility issues stemmed from the heavy use of custom components. To address this, we introduced shadow components—background elements with a low z-index that aren’t visible in the DOM. These shadow components were given aria-live attributes, and changes in the UI were tracked with JavaScript. By writing updates to these hidden divs, we ensured that necessary changes were properly announced to users.

### Enhanced Keyboard Shortcuts
   - We implemented keyboard shortcuts for various pages within the application, making it easier for users to navigate without relying on a mouse or trackpad.

### General Improvements
   - Several general improvements were also made, including fixing faulty installation processes and implementing authentication-based restrictions on various endpoints. These changes not only enhanced security but also contributed to a smoother user experience.

## TODO List

There are still a few tasks that need to be completed to further enhance the functionality and accessibility of the Zendesk custom Trudesk project. Here’s what’s on the list:

### Fixing the SingleSelect Component
   - The SingleSelect component currently has some issues that need to be addressed to improve its usability and accessibility. This includes ensuring proper keyboard navigation and screen reader support.

### Creating a SignUp Page
   - A SignUp page needs to be implemented to allow new users to register within the application. This can either be developed in-house or integrated from the upstream `next` branch once it's available.

### Announcing the Popup Popping Up
   - Ensuring that popups are announced properly when they appear is crucial for accessibility. This involves implementing a mechanism to alert screen readers when a popup is triggered.

### Fixing the Textarea
   - The textarea component needs adjustments to ensure it is fully accessible, including proper labeling and handling of focus events.

### Guidance for Text Entries
   - For text entry fields, especially in forms and messaging, implementing a feature that prompts users to "type your message" would enhance usability and provide clear guidance for screen reader users.
