---
title: "The GSoC Summary"
date: "2024-08-26"
summary: "The final report on GSoC 2024 under Zendalona working on the User Query Management Software"
description: "The final report on GSoC 2024 under Zendalona working on the User Query Management Software brief overview of web accessibility, Google Summer of Code, and more with Zendalona."
toc: true
readTime: true
autonumber: true
math: true
tags: ["gsoc", "accessibility", "web", "zendalona", "final"]
showTags: false
hideBackToTop: false
---

# The GSoC Summary : On Zendalona, Trudesk and Accessibility


## The Project: Trudesk Customization for Zendalona

The project I worked on as part of Google Summer of Code 2024(GSoC 2024) involved customizing Trudesk to meet the specific needs of Zendalona, with a strong focus on enhancing accessibility for users relying on screen readers and keyboard navigation. Trudesk, being a Single Page Application (SPA), posed unique challenges in terms of dynamic content updates, keyboard accessibility, and screen reader compatibility.

## The Grand Plan

The plan, at the outset, seemed straightforward enough: make the project more screen reader-friendly during the first month and then dive into implementing some custom features. Simple, right? Well, as it turns out, that initial scope was significantly optimistic. The goal of making the project truly accessible to screen readers quickly revealed itself to be a monumental task, far more complex than I had anticipated.

As I started navigating through the codebase, I realized that the issues weren’t just surface-level tweaks—they were deeply embedded in the structure of the application. The project was heavily reliant on custom components, which meant that many accessibility issues couldn’t be resolved with a quick fix. Each custom component had its own quirks, and figuring out where the problems lay often felt like trying to find a needle in a haystack. A task that seemed simple on the surface, like making a button accessible or ensuring a popup was announced, often took hours or even days of trial and error.

On top of that, the project setup itself was not the most cooperative. Every time I thought I was making progress, I’d hit a roadblock when trying to build the project on a different machine. The setup would break, and I’d find myself back at square one, trying to troubleshoot issues that seemed to crop up out of nowhere. It was frustrating, to say the least. But thanks to my mentor, @Akshay, these challenges became bearable. There were moments when I’d spend hours wrestling with a problem, only for him to step in and solve it in a matter of seconds. His guidance was invaluable, and I can’t overstate how much his support meant during those tough times.

Despite these challenges, by the end of the GSoC coding period on August 19th, the project had come a long way. The entire application can now be navigated using just the keyboard, with screen reader announcements guiding the way. It’s a far cry from where we started, but it’s not perfect yet. There are still some issues that need to be addressed, as noted in the TODO list, but the progress made so far is something I’m proud of. The journey has been intense, filled with unexpected hurdles, but seeing the project become more inclusive and accessible has made it all worth it.

The work isn’t done, but this phase of the project has laid a solid foundation for the improvements yet to come.

## Key Changes and Contributions

### Aria Live Regions for Dynamic Content:
   Since Trudesk dynamically renders content, it was crucial to implement aria-live regions to ensure screen readers announce changes appropriately. This enhancement made the application more accessible for users who rely on assistive technologies.

### Improved Keyboard Navigation and Focus Management:
   I made sure that all links, buttons, and custom components like accordions were fully navigable using the keyboard. Proper focus management was implemented, ensuring a seamless navigation experience.

### Shadow Components for Announcements:
   One of the innovative solutions involved creating shadow components with low z-index and aria-live attributes. These components track UI changes through JavaScript and ensure that necessary updates are properly announced by screen readers.

### General Enhancements:
   In addition to accessibility improvements, I also made general enhancements such as fixing faulty installations and implementing authentication-based restrictions on various endpoints.

You can read more about the project at [ZenDesk post](/docs/zendesk)

You can explore the codebase for these enhancements on my [custom Trudesk repository](https://github.com/anima-regem/trudesk). The project is currently hosted and live at [zendesk.animaregem.me](https://zendesk.animaregem.me).

### Merged Pull Requests

Throughout the project, I submitted several pull requests (PRs) to the original Trudesk repository, which were subsequently merged. Here are the key PRs that were integrated:

- [PR #688:](https://github.com/polonel/trudesk/pull/688)   
- [PR #687:](https://github.com/polonel/trudesk/pull/687)    
- [PR #685:](https://github.com/polonel/trudesk/pull/685)    
- [PR #679:](https://github.com/polonel/trudesk/pull/679)    

### Branches in the Custom Trudesk Repository

The custom Trudesk repository contains several branches that represent different stages and features of the project:

- **[Master Branch](https://github.com/anima-regem/trudesk/tree/master):** The stable version with all basic setup and initial enhancements.
- **[Zendesk Branch](https://github.com/anima-regem/trudesk/tree/zendesk):** Contains specific customizations for Zendalona, focusing heavily on accessibility improvements.

## The TODO List: What's Next?

Even after the GSoC period, there are still some pending tasks to further refine and enhance the project:

1. **Fixing the SingleSelect Component:** The SingleSelect component still requires some adjustments for better accessibility.
2. **Creating a SignUp Page:** A SignUp page needs to be implemented or integrated from the upstream `next` branch.
3. **Announcing Popups:** Ensuring that all popups are properly announced when they appear.
4. **Fixing the Textarea Component:** The textarea component needs improvements to enhance its accessibility.
5. **Guidance for Text Entries:** Implementing prompts for users to "type your message" in relevant text entry fields.

## The Verdict

My GSoC journey with Zendalona, Trudesk, and accessibility has been an enriching experience. It was more than just coding; it was about understanding the importance of inclusivity in technology. By enhancing Trudesk's accessibility, we’ve taken a step towards ensuring that the web is usable by everyone, regardless of their abilities.

If you're interested in the project or want to contribute, feel free to check out the [custom Trudesk repository](https://github.com/anima-regem/trudesk) and the hosted version at [https://zendesk.animaregem.me](https://zendesk.animaregem.me). Let’s keep pushing for a more accessible web!

## References


1. **ARIA and Keyboard Shortcuts:**
   - [ARIA Keyboard Interface Practices](https://www.w3.org/WAI/ARIA/apg/practices/keyboard-interface/#keyboardshortcuts)
   - [aria-keyshortcuts Attribute on MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes/aria-keyshortcuts)
   - [Landmark Roles on MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles#3._landmark_roles)

2. **Combobox and Accordion Patterns:**
   - [Combobox Select-Only Example](https://www.w3.org/WAI/ARIA/apg/patterns/combobox/examples/combobox-select-only/)
   - [ARIA Accordion Patterns](https://www.w3.org/WAI/ARIA/apg/patterns/accordion/examples/accordion/)
   - [Ensure Accessible Accordions](https://universaldesign.ie/communications-digital/web-and-mobile-accessibility/web-accessibility-techniques/developers-introduction-and-index/ensure-custom-widgets-are-accessible/create-accessible-accordions)

3. **General Accessibility Guidelines:**
   - [Web Content Accessibility Guidelines (WCAG) - No Keyboard Trap](https://www.w3.org/TR/WCAG22/#no-keyboard-trap)
   - [WebAIM Keyboard Accessibility Techniques](https://webaim.org/techniques/keyboard/)
   - [Syncfusion React Accessibility Documentation](https://ej2.syncfusion.com/react/documentation/common/accessibility/)

4. **Focus Management and UI Considerations:**
   - [Focus Order Understanding](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html#techniques)
   - [Improve Accessibility in React Apps by Managing Focus](https://medium.com/swlh/improve-accessibility-in-your-react-app-by-managing-focus-in-mutable-content-4ddf4ed92186)
   - [Auto Focus on Input with React](https://stackoverflow.com/a/46036043)

5. **Project-Specific Resources:**
   - [Discussion on Trudesk Accessibility](https://github.com/polonel/trudesk/discussions/674)
   - [Trudesk Deployment Guide](https://docs.trudesk.io/v1.2/getting-started/deployment/ubuntu-deployment)

6. **React and SPA Accessibility:**
   - [Next.js Accessibility Documentation](https://nextjs.org/docs/architecture/accessibility)
   - [Gatsby Client-Side Routing Improvements](https://www.gatsbyjs.com/blog/2020-02-10-accessible-client-side-routing-improvements/)
   - [React Aria Live Route](https://github.com/AlmeroSteyn/react-aria-live-route)
   - [React Router Accessibility](https://github.com/remix-run/react-router/issues/5210)

7. **Other Useful Discussions and Solutions:**
   - [Accessibility in Mutable Content](https://medium.com/swlh/improve-accessibility-in-your-react-app-by-managing-focus-in-mutable-content-4ddf4ed92186)
   - [React's useId Hook Documentation](https://legacy.reactjs.org/docs/hooks-reference.html#useid)
   - [Accessible Client-Side Routing](https://www.gatsbyjs.com/blog/2020-02-10-accessible-client-side-routing-improvements/)
   - [Aditum - Accessibility in React Applications](https://github.com/oslabs-beta/aditum)
   - [Oaf Project - React Router Accessibility](https://github.com/oaf-project/oaf-react-router)

8. **Video References:**
   - [Demystifying Accessibility in React Apps](https://www.youtube.com/watch?v=0ckOUBiuxVY&t=20655s)

These references were instrumental in guiding the development process and ensuring that the final product met the necessary accessibility standards.
