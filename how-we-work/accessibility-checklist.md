# A11y Checklist 
A quick checklist for accessibility practices and tools for web developers. These are not only aimed at people with permanent disabilities, they [target the whole internet](https://thewholeinternet.com/). Contributions are more than welcome!

### 👀 Visual 
These practices and patterns are helping users with various types of dissabilities (permanent or temporary), from color-blindness, to vestibular dysfunction, to low vision to hearing deficits.

* color contrast, **>4.5** for AA standard, **>7.0** for AAA (a lot of tools can automate this check for the entire site)
* aim for _bigger_ contrast for _smaller_ text
* prioritize text contrast vs borders / other elements
* use **icons** or other visual indicators together with color (ex: showing errors in forms)
* min font-size should be **16px**
* keep 80 characters per line when displaying longer texts and ensure standard spacing for paragraphs
* ensure animations are _necessary_ and not _unexpected_
* use [**prefers-reduced-motion**](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion) to disable animations when users opt-in from their OS
* ensure videos have _subtitles_ or _auto-captions_
* ensure that at least 5 zoom levels are available on your website and that the layout responds well to zooming in

### ✅ Semantic HTML 
The use of semantic HTML is crucial for [offering support](http://wicg.github.io/aom/explainer.html) to screen readers and other assistive technologies. By default, HTML does a pretty decent job at this, but you have to make sure you follow the standard and don't override useful defaults.

* avoid using a <div> when a semantic tag can be used instead
* use standard **landmarks** for defining: header, main, footer, etc.
* use **headings** in the right order, always start from **h1**
* form inputs should always be accompanied by **labels**
* menus should start from a **<nav>** element and contains _lists_ and _list items_
* use relevant **titles** for links - they are read by screen readers as users tab their way through the site
* avoid titles like: "click here" or "read more", as they give no indication about the actual link
* images should be accompanied by relevant **alt** texts
* use _ARIA_ attributes only when there's no semantic alternative

### ✋ Interaction
Never make assumptions about how your users interact with the website and make sure you have support for things like keyboard navigation. Some of these practices target people with motion difficulties, tremors and other problems limiting their interaction skills.

* _links_ and _buttons_ should always be keyboard focusable (using the tab key)
* _menus_ and _lists_ should be keyboard accessible (left-right for navigation)
* modal windows have to close when pressing the Esc key
* always show an outline when focusing elements - at a minimum, support keyboard outline with [what-input](https://github.com/ten1seven/what-input)
* **focus** should be handled in parallel with click/tap events as well as with :hover pseudo-selectors
* don't use tabindex > 0, allow a natural flow for the focus through the interface
* trap focus when showing modal/overlays, so the user cannot navigate behind the foreground
* handle focus after navigation - especially for SPA-like applications which are not reloading the page
* ensure a **touch area** of at least 44px

### 🔨 Tools & Projects
* Screen Readers
  * **Jaws** for Windows
  * **NVDA**
  * **VoiceOver** on OS-X/iOS
  * **Orca** for Linux
* [lighthouse](https://developers.google.com/web/tools/lighthouse/) - performs audits in chrome (the audit tab in devtools).
* [axe-core](https://github.com/dequelabs/axe-core) - performs e2e automated tests for a11y issues, can easily be integrated in cypress or jest.
* [tota11y](https://khan.github.io/tota11y/) - shows a11y validations on top of existing websites.
* [alexjs](https://alexjs.com/) - catches insensitive and inconsiderate writing.
* [eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y) - ESLint plugin for static analysis of a11y violations.
* [ReachUI](https://ui.reach.tech/) - a list of a11y first React components
* [Inclusive Components](https://inclusive-components.design/) - a list of articles and examples of inclusive and accessibile components

### 📝 References 
* [A guide to color accessibility in product design](https://www.invisionapp.com/inside-design/color-accessibility-product-design/)
* [Designing Accessible Content: Typography, Font Styling, and Structure](https://webdesign.tutsplus.com/articles/designing-accessible-content-typography-font-styling-and-structure--cms-31934)
* [Designing Safer Web Animation For Motion Sensitivity
](https://alistapart.com/article/designing-safer-web-animation-for-motion-sensitivity/)
* [Accessibility showcases of real projects](https://a11ywins.tumblr.com/)
* [Web Accessibility Course on Udacity](https://eu.udacity.com/course/web-accessibility--ud891)
* [Useful Accessibility Resources by Stefan Judis](https://www.stefanjudis.com/useful-accessibility-resources/)
* [Status of a11y support in browsers](https://www.html5accessibility.com/)
* [Building Accessible Menu Systems](https://www.smashingmagazine.com/2017/11/building-accessible-menu-systems/)
* [Human Interface Guidelines for iOS](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/adaptivity-and-layout/)
* [Handling Touch Targets](https://a11yproject.com/posts/large-touch-targets/)
* [WAI-ARIA Guidelines](https://www.w3.org/WAI/standards-guidelines/aria/)


*** Credits go to [Alex Moldovan](https://github.com/alexnm/a11y-checklist)
