---
layout: default
title: "Validation Testing Notes"
permalink: /validation-testing-notes/
---

# GENERAL

Your goal is to **repeat yourself as little as possible** while testing as much as possible - not only inside the test steps, but across the entire test suite. If you've already confirmed that the window opens, you don't need to confirm it again. If a test touches multiple windows that have already been tested, you can assume those tests have passed and nothing in them needs to be confirmed UNLESS the situation is wholly different or distinct enough that it deserves a new checkbox.

In general, the assumption is that **the tester knows nothing about the application** being tested, **but knows how to use a computer**, navigate a menu, click a mouse, download files, etc. You do not need to explain those things.

Test documents should be a **get-in-get-out** situation. We don't need a preamble, icons, pretty things, lots of screenshots to scroll through, nice formatting, etc. Just numbered test steps you can run through real quick to know for sure something works. Though you might feel the need to spice it up and make it more fun and attractive for the tester, trust me, when you have to process through a 140 page test suite with 9pt font, the last thing you want is extra info you have to scan and figure out if you need.

# HOW TESTS ARE WRITTEN

Each statement or complex statement group must be **independently testable**, unless it is setup or informative (which must be nested in the step). We should be able to write 1:1 automated tests from your written steps, with few exceptions. There WILL BE exceptions, but we want most of the test to be "testable."

**The majority of test steps must generally be written in 2 parts:** The action verb, and the confirmation verb. Check out these examples:

* Click the Submit button. Confirm that the window closes.
* Type "2" in the Dose field. 
  * Confirm that the field is highlighted in red and a warning icon is displayed
  * Verify that the value in the <whatever> field updates to reflect this change
* Navigate to *System > Windows > Patient Demographics*. Confirm that the window opens.

If you only have the action verb, you're not testing anything, just moving around. If you only have the confirmation verb, your test is ambiguous and may not be accurate; either case means the statement isn't "testable."

That isn't to say that ALL steps in a process must be in this format - just most of them. You will still sometimes need to undo things you did just for some isolated test, and sometimes you'll still need to do a bunch of setup or navigation that doesn't require any validation.

In general, **you want to mention/specify only what is important to test the step**. If it's not important what color the button is, don't mention the color of the button. The only exceptions are if there are many elements that match the descriptor and the only way to tell them apart is by their color... but that would be bad UX so hopefully that should never come up.

When writing a test, **you can assume that all tests prior to/relevant for it have passed.** For example, you can assume there is a patient with a prescription, a provider, a dosing plan, and a treatment plan ready to go when you need to test injections. In each test, you should mention and link (if possible) any procedures that you assume have been done. This will keep each individual test procedure lightweight, but still imply the relationship between the procedures. 

# FORMAT

For traceability purposes, we need to write isolated tests that completely test the functionality, errors, etc of each individual window and area.

Once those individual tests have been written, we can write "bridge tests" that don't test the parts we've already tested, but instead test the interactions between windows that would be hard to measure in an isolated window-only test.

Since the action is localized to one window, ONE screenshot with all areas/buttons/etc named will suffice, with exceptions for error messages, popups, etc, which can have their own images. These images represent states of the window, not each step along a path.

**Always use the same names for everything**, even if you're just making it up and the name isn't final - that will make it easier to maintain in the future, and easier to follow while testing.

Always use the same action and confirmation verbs, with the following being the preferred:

* "Navigate to..."/"Use the <something> to navigate to..." - Menus, URLs
* "Click on..."/"Click the..." - Buttons
* "Select <something> in the..." - Dropdowns, Date/Color pickers, multi-selects, wall-of-options
* "Search for <something> in..." - Search boxes
* "Type <something> into..." - Input fields
* "Confirm that..." - Confirmation is for yes or no questions
* "Verify that..." - Verification is for when you need to know if a value is right

Notice that there is no room for confusion or alternate possibilities or uncertainty in this wording - testable tests aren’t uncertain.

**Do not narrate individual steps** if they are all describing a linear path through something - combine it all into one thing. Common examples of this are navigating through menus. Prefer "In the System Menu, navigate to *System > Windows > Butt*" over "Click the *System Menu*... Hover over *Window*... Click on *Butt*".

Make use of links to point at other test steps in the chain. Will the tester need to make use of something later, so it's important they hold on to something? Let them know. 

Squeeze as many testable tests as you can out of each window WITHOUT reaching out to step on the toes of other tests. When you fill out Patient Demographics, for example, the Save button only shows up if something has changed. So, to sneak that test in there:

1. Type a value into the First Name field. Confirm that the Save button appears *(This tests this specific bit of functionality, while also blending into your next test which is filling out all the values)*
2. Type "XYZ" in the Zip Code field. Confirm that you are unable to do it. *(Same here)*
3. Type … into …
4. …
5. Click the *Save* button. Confirm that all information entered is present when the window is reopened.
	
For clarity's sake, enclose anything the user types in double quotes. Code elements (including SQL, .env settings, etc) should be in back-ticks or fenced code blocks. Everything else should be written normally. Optionally, you can write the names of elements (the *System Menu*, the *Submit* button, dropdown entries) in italics to make them stand out more, but only do this if it enhances clarity inside the test step.

