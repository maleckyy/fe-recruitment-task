# Submission: Patryk Kupfer

## Time Spent

Total time: **4 hours** (approximate)

## Ticket Triage

### Tickets I Addressed

List the ticket numbers you worked on, in the order you addressed them:

1. **CFG-142**: Fixed the price display by making sure the usePriceCalculation hook always uses the newest configuration.
2. **CFG-152**: Added tabIndex and keyboard support (Enter/Space) for color picking, and fixed missing focus outlines on quantity buttons.
3. **CFG-149**: Created a LoadingIcon component to hide the old price while the new one is loading, so the user doesn't see incorrect data.
4. **CFG-156**: Replaced key={index} with unique IDs in all lists to prevent UI bugs and make React rendering faster and safer.
5. **CFG-145**: Added a keyboard shortcut (Ctrl + Enter) to quickly add products to the cart and ensured it is properly removed when not needed.
6. **CFG-143**: Fixed a memory leak by adding a cleanup function to the window resize listener.

### Tickets I Deprioritized

List tickets you intentionally skipped and why:

| Ticket  | Reason                 |
| ------- | ---------------------- |
| CFG-144 | Ticket requires clarification due to CFG-145. |
| CFG-146 | Visual element, relatively easy to improve with low priority. |
| CFG-147 | Ticket requires clarification. |
| CFG-148 | Ticket requires. |
| CFG-150 | Visual element, relatively easy to improve with low priority. |
| CFG-151 | An important element of the UI, but not so crucial for the upcoming demo. |
| CFG-152 (3, 4) | These two points require more time for testing. |
| CFG-153 | Execution time too long. |
| CFG-154 | Ticket requires clarification. |
| CFG-155 | Not enough time to complete the task. |
| CFG-157 | Not enough time to complete the task. |

### Tickets That Need Clarification

List any tickets where you couldn't proceed due to ambiguity:

| Ticket  | Question                  |
| ------- | ------------------------- |
| CFG-144 | Does removing the “Quick Add” option affect adding a shortcut from CFG-145? If we opt out of this option, should CFG-145 also not be executed? |
| CFG-147 | The Size: 10" Large option is not available in the configuration options. Is this the correct display size? |
| CFG-148 | How should I interpret “Premium Material”? |
| CFG-154 | Should 50 already qualify for a discount? |

---

## Technical Write-Up

### Critical Issues Found

Describe the most important bugs you identified:

#### Issue 1: [Price shows wrong value after rapid option changes]

**Ticket(s):** CFG-142

**What was the bug?**

The price was not displayed correctly after changes were made to the product configuration.

**How did you find it?**

In my case, the correct price did not appear at all. Regardless of configuration changes, it always remained “0.”

**How did you fix it?**

I modified the usePriceCalculation hook so that it correctly accepts the latest product configuration.

**Why this approach?**

This approach means that the latest version of the configuration will be used to calculate the final price.

---

#### Issue 2: [App becomes sluggish after extended use]

**Ticket(s):** CFG-143

**What was the bug?**

When changing the window width, unnecessary eventListeners were added.

**How did you find it?**

When changing the window width in devTools, the number of active eventListeners increased.

**How did you fix it?**

I added a cleanup function in the appropriate useEffect.

**Why this approach?**

The current useEffect did not have a cleanup function.

---

#### Issue 3: [Improve Quick Add feature with keyboard shortcut]

**Ticket(s):** CFG-145

**What was the bug?**

The customer needed a shortcut to add a product to the shopping cart.

**How did you find it?**

[Your debugging process]

**How did you fix it?**

I added addEventListener for the “CTRL” + “Enter” combination, which adds the current configuration to the cart.

**Why this approach?**

This is a simple method to add keystroke listening.

---

#### Issue 4: [Add loading indicator during price calculation]

**Ticket(s):** CFG-149

**What was the bug?**

The old price remains visible when calculating new prices.

**How did you find it?**

When changing the product configuration, the old product price is displayed.

**How did you fix it?**

I created a LoadingIcon component and display it when the new price is still being calculated.

**Why this approach?**

Creating a reusable component was a simple option and allows the component to be used in other places in the application.

---

#### Issue 5: [Accessibility - Can't navigate with keyboard only / in part]

**Ticket(s):** CFG-152

**What was the bug?**

Color picker swatches are unreachable without a mouse.
Increment and decrement quanitity buttons doesn't have focus styles.

**How did you find it?**

Errors found when navigating the application using the keyboard.

**How did you fix it?**

I added appropriate styles to the buttons responsible for increment and decrement quanitity.
I added tabIndex to the color variants and then selected the one marked with the “enter” or “space” keys.

**Why this approach?**

Styles for the focus state were added to match those on input elements.
Adding tabIndex allowed me to easily add elements for navigation.

---

#### Issue 6: [Console warnings about missing keys in lists]

**Ticket(s):** CFG-156

**What was the bug?**

Some lists used index as key.

**How did you find it?**

I searched through the lists where index was used as the key, starting with those listed in the ticket.

**How did you fix it?**

I used unique identifiers of this objects.

**Why this approach?**

Using a unique key allows to properly identify list items. This approach improves re-rendering.

---

### Other Changes Made

Brief description of any other modifications:

- I added validation to the handleQuickAdd function.
- I changed shareUrl to useMemo so that it is only generated when changes affecting its dependencies occur.

---

## Code Quality Notes

### Things I Noticed But Didn't Fix

List any issues you noticed but intentionally left:

| Issue   | Why I Left It                                         |
| ------- | ----------------------------------------------------- |
| [Empty "Catch" block statment] | Out of time |
| [Error: Calling setState synchronously] | Out of time |
| [Use of type “any” in ConfigChangeEvent] | Out of time |
| [Unused useDebouncedPriceCalculation hook] | Out of time |

### Potential Improvements for the Future

If you had more time, what would you improve?

1. Breaking down a component into smaller parts to improve readability
2. Creating reusable components using styled-components, for example
3. Add a library for managing the application state, such as Zustand.
4. Adapting the application to WCAG, a quick audit revealed errors with contrast and missing labels.

---

## Questions for the Team

Questions you would ask in a real scenario:

1. What elements are most crucial for the customer or what matters most to them?

---

## Assumptions Made

List any assumptions you made to proceed:

1. The time required for code changes is 4 hours.
2. The priority is tasks that are key for the customer or key for the upcoming demo.

---

## Self-Assessment

### What went well?

I'm glad I managed to complete the most important tasks for the demo in 4 hours. 

### What was challenging?

I really wanted to test myself in four hours. That's how long it took to do all the coding and ticket analysis. The biggest challenge for me was the time limit, which forced me to think carefully and manage my time well.

### What would you do differently with more time?

If I had more time, I would definitely try to add the elements I mentioned in the “Potential Improvements for the Future” section.
---

## Additional Notes

Anything else you want us to know:

As time was limited, I used both Gemini and the local agent qwen3 for help.
