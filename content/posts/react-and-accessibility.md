---
title: "React and Accessibility"
date: "2024-08-23"
summary: "My rant on React and Accessibility."
description: "My rant on React and Accessibility."
toc: true
readTime: true
autonumber: true
math: true
tags: ["gsoc", "accessibility", "web", "zendalona", "final", "react", "trudesk"]
showTags: false
hideBackToTop: false
---

# React and Accessibility


## Intro

Accessibility is something that every developer should care about, but it's often one of those things that get pushed to the bottom of the priority list. I get it—deadlines are tight, and sometimes it feels like adding accessibility features is just an extra burden. But trust me, making your React apps accessible, especially for screen readers, is not just a nice-to-have; it’s a must.

While working on [TruDesk](https://trudesk.io/) as part of [GSoC](/posts/the-gsoc-summary) under [Zendalona](https://zendalona.com/), I got a lot more into in web accessibility. Specifically, I had to dive deep into screen reader accessibility in React, which was both challenging and eye-opening. It’s easy to underestimate the complexity of making an app truly accessible. There are tons of approches and even more methods out there in the internet, so much documentation on small and finer things but not a one stop destination to clear all your doubts.

## Why Screen Reader Accessibility Matters

Screen readers are vital tools for people with visual impairments. They convert digital text into synthesized speech, enabling users to navigate and interact with web content. Unfortunately, not all web applications are designed with screen reader accessibility in mind, making it difficult or even impossible for these users to have a good experience.

For a React app, ensuring that your components are accessible to screen readers is a critical step. It’s not just about ticking a box—it’s about opening up your app to a wider audience and ensuring that everyone can use it effectively. Sometimes, that might mean giving up on some functionality.


### The Accessibility Tree: A Hidden World Within Your Browser

The accessibility tree is one of those behind-the-scenes elements that many developers—myself included—might not even know exists. It’s not something you’ll encounter in your day-to-day coding, but once you’re aware of it, you start to realize how crucial it is to building accessible web applications. I was introduced to the concept while watching [this talk](https://www.youtube.com/watch?v=0ckOUBiuxVY&t=20655s) on demystifying accessibility in React apps, and it was like discovering a hidden layer of the web I never knew about.

So, what exactly is the accessibility tree? Think of it as a parallel DOM (Document Object Model) that browsers generate specifically for assistive technologies like screen readers. While the DOM represents the visual structure of a webpage, the accessibility tree represents the semantic structure. It’s how screen readers interpret your app, converting visual elements into a format that can be understood and navigated by users with disabilities. This tree is automatically created based on the HTML and ARIA (Accessible Rich Internet Applications) attributes in your code, and it’s what allows screen readers to convey the meaning and function of different elements to users.

What’s fascinating is how the accessibility tree can either enhance or hinder a user’s experience, depending on how well you’ve structured your HTML and used ARIA roles. Elements that seem trivial in the visual DOM, like a missing `alt` attribute on an image, can lead to major issues in the accessibility tree. This can result in screen readers skipping over important content or presenting information in a confusing way. The more I learned about it, the more I realized how much power we, as developers, have in shaping this hidden tree, and consequently, in making our apps truly accessible.

Understanding the accessibility tree has made me rethink how I approach coding. It’s easy to get caught up in making things look good on the surface, but if we ignore the underlying structure that assistive technologies rely on, we’re excluding a significant portion of our users. Now, I find myself inspecting the accessibility tree alongside the DOM, ensuring that what I’m building is not just visually appealing but also accessible to everyone. It’s like adding a new tool to your belt—one that helps you craft a more inclusive and user-friendly web.

![An image of Uncle Ben from Spider Man saying, "With Great Power comes Great Responsibility"](../../assets/uncleben.jpg)


## Best Practices for Screen Reader Accessibility in React

### **Use Semantic HTML**
   
   I've always wondered why the makers of the web would put so many different tags that basically do the same thing—act as a glorified `div`—but going down the whole screen reader rabbit hole opened my eyes! It turns out these tags are not just there to make your code look pretty or to confuse beginners; they actually serve a crucial purpose.

   Semantic HTML tags like `<header>`, `<nav>`, and `<main>` do more than just give your content a fancy wrapper. They provide context to screen readers, which in turn helps users understand the structure and importance of the content on the page. For instance, when a screen reader encounters a `<nav>` element, it knows that this section contains navigational links, which can then be presented differently to the user. The same goes for `<main>`, which indicates the primary content of the page, and `<footer>`, which often contains supplementary information.

   By using these tags, you're essentially communicating with screen readers in their language, making your app more accessible to users who rely on them. This small change can have a significant impact on how easily someone can navigate through your application. And the best part? It’s a low-effort improvement with a high reward. So the next time you reach for a `div`, ask yourself if there’s a more semantic alternative that could do the job better. Chances are, there is, and it will make your app more inclusive as a result.

### **Accessible Form Labels**

Forms are one of those places where accessibility issues tend to sneak in, often because we forget the little things. Every input in a form needs a buddy—a `<label>` that’s there to explain what that input is all about. It might seem like a small detail, but for someone using a screen reader, it’s a game-changer.

Imagine filling out a form without being able to see the screen. When a screen reader user tabs through the inputs, they rely on the labels to tell them what each field is for. Without a proper label, they’re left guessing whether they’re supposed to type in their name, email, or something else entirely. That’s where the `for` attribute in HTML, or the `htmlFor` property in React, comes in. It creates a link between the label and the input, so when the user focuses on the input, the screen reader reads out the label. It’s like giving someone a map when they’re lost—simple, but so important.

For example, if you have a form field for an email address, you’d write something like this in React:

```jsx
<label htmlFor="email">Email Address</label>
<input type="email" id="email" />
```

This way, when the screen reader lands on the input, it’ll say “Email Address,” and the user will know exactly what to do. Without this, they’d just hear “edit text” or something equally unhelpful. And let’s be honest, who doesn’t want their forms to be as user-friendly as possible?

It’s little tweaks like these that make a huge difference in accessibility. So, the next time you’re working on a form, take an extra minute to make sure every input has a proper label. Your users will thank you—even if you never hear it!


### **ARIA Attributes**

ARIA (Accessible Rich Internet Applications) attributes are like the secret sauce for screen reader accessibility. They’re there to help out when native HTML elements don’t quite cut it. Think of ARIA as a way to fill in the gaps and make your web app speak the language of assistive technologies more fluently.

For example, say you’ve got a button that only has an icon—no visible text. A screen reader would usually just skip over it, leaving users clueless about what that button does. But with the magic of `aria-label`, you can give that button an invisible label, something like this:

```jsx
<button aria-label="Search">
  <SearchIcon />
</button>
```

Now, when a screen reader hits that button, it’ll announce “Search,” and users will know exactly what it does.

Or maybe you’ve got some dynamic content on your page—something that changes without a full page reload, like a live chat widget. Without any help, a screen reader might not even notice the change. But if you throw in an `aria-live` attribute, you can make sure the screen reader picks up on that change and reads it out to the user:

```jsx
<div aria-live="polite">
  {/* dynamic content here */}
</div>
```

But here’s the catch: don’t get too ARIA-happy. The first rule of using ARIA is pretty simple—if you can do it with native HTML, do it that way. ARIA should be your backup plan, not your go-to. Overusing ARIA can actually make things more complicated for screen reader users, so keep it as a tool in your accessibility toolbox, but don’t lean on it too much. It’s all about finding that sweet spot where your app is accessible without being overloaded with unnecessary code.
### **Keyboard Navigation**

Keyboard navigation is a lifeline for screen reader users. While we might take a mouse or trackpad for granted, many people rely on the keyboard to move through a website or app. That’s why it’s crucial to make sure that all interactive elements—like buttons, links, and form fields—are easily accessible via the keyboard.

First things first, every interactive element needs to be focusable. By default, most elements like buttons and links are already in the tab order, so users can hop from one to the next by hitting the Tab key. But sometimes, especially with custom components, you might need to step in and use the `tabindex` attribute to ensure they’re focusable. For instance, if you’ve built a fancy custom button that isn’t naturally focusable, adding `tabindex="0"` can make it accessible:

```jsx
<div role="button" tabindex="0">
  Custom Button
</div>
```

This simple addition means that keyboard users can reach it just as easily as any other button on the page.

But making sure something is focusable is just part of the story. You also need to give users a clear visual indication of where their focus is. Those default focus outlines that browsers add might not win any beauty contests, but they serve a critical purpose. Removing them without providing a clear alternative is like turning off the headlights on a dark road—it’s disorienting and can lead to a frustrating experience. If you really must customize the focus styles, make sure your new styles are just as noticeable, if not more so:

```css
.custom-focus {
  outline: 2px solid #007acc;
  outline-offset: 2px;
}
```

This way, you keep your app looking sleek while ensuring that keyboard users can still easily see where they are on the page. 
### **Focus Management**

Focus management is like the unsung hero of accessibility, especially in single-page applications (SPAs) where content changes dynamically without a full page reload. If you’re not careful, users can get lost in the shuffle, especially those relying on screen readers or keyboard navigation. That’s why it’s so important to make sure that when content changes, the focus moves to the right place at the right time.

In a React app, this usually means taking control of the focus programmatically. Let’s say you’ve got a modal or a new section that pops up based on user interaction. If you don’t explicitly set the focus to the new content, users might still be stuck on an element that’s no longer relevant, or worse, not even visible. This is where React’s `ref` system comes in handy. By assigning a `ref` to the new content and then using `ref.current.focus()` when it appears, you ensure that users’ attention is directed exactly where it needs to be:

```jsx
const MyComponent = () => {
  const newContentRef = React.useRef(null);

  const handleClick = () => {
    // some action that reveals new content
    newContentRef.current.focus();
  };

  return (
    <div>
      <button onClick={handleClick}>Show Content</button>
      <div ref={newContentRef} tabIndex="-1">
        This is the new content that should be focused.
      </div>
    </div>
  );
};
```

By doing this, when the new content is revealed, the focus jumps right to it, making for a seamless experience. It’s a small tweak that can make a big difference, particularly in apps where the content is constantly shifting and changing.

Remember, good focus management is about guiding users through your app in a way that feels intuitive and natural. If they’re hitting the Tab key or relying on a screen reader, they should be able to follow the flow of your content without getting lost or confused. It’s all about keeping the user experience smooth, regardless of how they’re interacting with your app.


### **Skip Navigation Links**

Skip navigation links might seem like a tiny, easily overlooked feature, but for screen reader users, they can be a game-changer. Imagine having to listen to the same navigation menu read out loud on every single page before you can get to the actual content you’re interested in—it gets old really fast. That’s where a “Skip to content” link comes in handy.

By placing a “Skip to content” link right at the top of your page, you give users a quick and easy way to jump past all the repetitive stuff (like the navigation bar) and go straight to the main content. It’s a small gesture that shows you’ve thought about their experience, making your app more user-friendly for everyone. Here’s how you might implement it:

```html
<a href="#main-content" className="skip-link">Skip to content</a>
```

And then, in your HTML, you’d have something like this:

```html
<main id="main-content">
  <!-- Main content here -->
</main>
```

This link usually isn’t visible to sighted users unless they’re navigating via the keyboard, but for those using screen readers or keyboard navigation, it’s a real timesaver. When they hit Tab on a new page, the first thing they encounter is the “Skip to content” link, which they can activate to bypass the header, nav bar, and anything else they don’t need to hear again.

Think of it as a fast pass to the good stuff. It’s easy to add, doesn’t interfere with your design, and makes a huge difference for users who rely on assistive technology. Plus, it’s one of those things that shows you’ve put thought into the little details—something that can set your app apart in terms of accessibility.

### **The Elephant in the Room: "Nobody Actually Creates Components Anymore, Right? Let’s Talk About Custom Components"**

Let’s address the elephant in the room: in today’s development world, nobody’s really handcrafting components from scratch anymore, are they? We’ve all been there—why reinvent the wheel when there’s a shiny, feature-packed component library just a `npm install` away? Whether you’re using Material-UI, Bootstrap, or any of the countless other libraries out there, it’s become the norm to lean on pre-built components to speed up development and maintain consistency across your app.

But here’s the catch: while these libraries can save you tons of time and effort, they don’t always come with accessibility baked in. Sure, they look good and they’re easy to drop into your app, but if you’re not careful, you might end up with a beautiful UI that’s a nightmare for screen reader users or those relying on keyboard navigation. That’s where understanding how to create and manage custom components with accessibility in mind really comes into play.

When you’re working with custom components—whether you’re building them from scratch or extending a library’s offerings—it’s crucial to ensure they’re accessible. This means thinking about things like ARIA roles, keyboard interaction, focus management, and making sure all the relevant content is accessible to screen readers. It’s easy to assume that the library you’re using has already taken care of all that, but that’s not always the case. Even the most popular libraries sometimes fall short on accessibility, or require additional configuration to get it right.

Let’s say you’re creating a custom dropdown component. It’s not enough to just make it look good and function on a click; you need to consider how it’s going to work for someone navigating with a keyboard or using a screen reader. Are you providing appropriate ARIA roles like `aria-expanded` and `aria-haspopup`? Can the user navigate through the options with arrow keys? Does focus move correctly between elements?

Here’s a simple example:

```jsx
const Dropdown = () => {
  const [isOpen, setIsOpen] = React.useState(false);
  const toggleDropdown = () => setIsOpen(!isOpen);

  return (
    <div>
      <button
        aria-haspopup="listbox"
        aria-expanded={isOpen}
        onClick={toggleDropdown}
      >
        Options
      </button>
      {isOpen && (
        <ul role="listbox">
          <li role="option" tabIndex="0">Option 1</li>
          <li role="option" tabIndex="0">Option 2</li>
          <li role="option" tabIndex="0">Option 3</li>
        </ul>
      )}
    </div>
  );
};
```

In this example, we’re not just throwing in some `div`s and calling it a day—we’re thinking about how the component will interact with assistive technologies. The button has the `aria-haspopup` attribute to indicate that it controls a dropdown, and `aria-expanded` to communicate its state. Each list item has a `role="option"` to tell the screen reader it’s an option within the dropdown. 

The takeaway here is that even if you’re relying on component libraries (and let’s face it, we all do), it’s essential to take a step back and make sure those components are truly accessible. Sometimes this means diving into the library’s documentation or even contributing a fix yourself. Other times, it might mean extending or customizing components to meet accessibility standards. But in the end, putting in that extra effort ensures that your app is usable by everyone, not just those who interact with it in the same way you do.

## Conclusion

Making your React app accessible to screen readers isn’t just about following a checklist—it’s about empathy. Understanding the challenges that users with disabilities face and addressing them in your code is both a technical and a moral responsibility.

I’m still learning and making mistakes along the way, but the journey toward building accessible web apps is definitely worth it. By following these best practices, you can make a significant difference in the lives of users who rely on screen readers, ensuring that your app is usable by everyone, not just the majority.

If you’re looking to dive deeper into accessibility, here are some great resources that I’ve found incredibly helpful:

- **[MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/Accessibility)**: A comprehensive guide to web accessibility, including best practices and ARIA roles.
- **[W3C Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/)**: The go-to source for all things accessibility, offering tutorials, guidelines, and resources to help you make the web more inclusive.
- **[W3Schools Accessibility Tutorial](https://www.w3schools.com/accessibility/)**: A beginner-friendly introduction to web accessibility, covering basic principles and techniques.
- **[A11Y Project](https://www.a11yproject.com/)**: A community-driven effort to make digital accessibility easier, with checklists, articles, and tools.
- **[Inclusive Components](https://inclusive-components.design/)**: A blog by Heydon Pickering that focuses on designing accessible and inclusive web components.

These resources have been invaluable in my own journey toward understanding and implementing accessibility in my projects. Whether you’re just getting started or looking to deepen your knowledge, these sites provide the tools and guidance you need to make your web apps more accessible to everyone.

---