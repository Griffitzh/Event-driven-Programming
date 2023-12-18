# Event-driven Programming

The flow of the program is determined by events such as user actions (mouse
clicks, key presses), system events (page loaded, timer), or messages from other
programs (e.g. response for an HTTP Request, WebSocket message).

## Materials and Resources

| Material                                                                                              | Time  |
| :---------------------------------------------------------------------------------------------------- | ----: |
| [JavaScript DOM Tutorial #9 - Events](https://youtu.be/ndz6iH6o1ms)                                   | 11:13 |
| [JavaScript DOM Tutorial #10 - Event Bubbling](https://youtu.be/SqQZ8SttQsI)                          |  7:42 |
| [JavaScript DOM Tutorial #15 - Checkboxes & Change Events](https://youtu.be/D-sSNQfz_1s)              |  4:24 |
| [JavaScript DOM Tutorial #18 - DOMContentLoaded Event](https://youtu.be/G5Or47gPH-4)                  |  4:29 |
| [Javascript Events Tutorial - How Web Developers Respond to User Input](https://youtu.be/e57ReoUn6kM) | 18:49 |

| Optional                                                                                              | Time  |
| :---------------------------------------------------------------------------------------------------- | ----: |
| [JavaScript DOM Tutorial #11 - Interacting with Forms](https://youtu.be/n4B7vY9SIds)                  |  5:42 |

## Material Review

- What's an event and what's an event handler?
  <!--
    Event = something happened
    A real life action what you want to handle in your program.
    - an automatic door, action: you walked into the observed area
    - the elevator, action: you pushed the button
    - rendering website, action: content loaded
    - communicating with the server, action: response received

    An event handler is basically a callback function which is executed when the
    event happened
  -->
- How to add an event listener?
  <!--
    - the legacy way is the use the on... methods, e.g. onclick, onload, etc.
    - the more modern way is to use the `addEventListener()` function which is
      more flexible, e.g. you can attach multiple event handlers to the same
      event.
  -->
- What are the most common mouse and keyboard events?
  <!--
  - Mouse: `click` is the most common, sometimes `mouseenter`, `mouseleave`,
    `mousemove` are used
  - Keyboard: if you need low level control use `keydown` or `keyup`, but most
    of the time it's easier to use a higher level event like, `change`, `input`.
  -->
- What's focus and how to handle focus in and out?
- What's a typical use case for the `blur` event?
  <!--
    Focused element is the currently active element, you can type and interact
    with the focused element. Only one element can be focused.
    Use the `focus()` function to move the focus in.

    Use the `blur` event to handle the case when user left an element, this is a
    good place to do validation in a text field.
  -->
- What are the most common form and input events?
  - What's the best way to handle form submit
    (button `click` vs. form `submit`)?
    <!--
    - form `submit` event: use this instead of mouse click on the submit button,
      as it works with multiple buttons and on the enter key press as well
    -->
  - What's the best way to handle changes in `select`, `checkbox` and `radio`?
    <!--
    - use the `change` event on `select`, `checkbox` and `radio` elements to
      handle the state change
    -->
  - What's the best way to handle user input to a text field?
    <!--
    - use the `input` event to detect user input in a text field, this is better
      than using `keydown` event since it also works with copy & paste,
      voice, pen and other input methods. The `change` event only fires once the
      user left the text field, that's not what you usually want.
    -->
- How to detect user scroll?
  <!--
  - `scroll`, but watch out because this fires in a very high rate, see the next
    question.
  -->
- (Optional) How to handle high rate events like `scroll` and `mousemove`?
  <!--
    These events fire too many times, and it'll result in too many execution
    (too much CPU, or too many HTTP requests).
    You usually want to throttle these events meaning that you limit the number
    of actual execution.

    Here is a simple solution:

    let timeout = null;

    element.addEventListener('scroll', event => {
      if(timeout != null) return;

      timeout = setTimeout(() => {
        doWork(); // do the actual execution

        timeout = null;
      }, 250);
    });
  -->
- How to properly use `readystatechange`?
  <!--
    Why is it fired 4 times? => because there are 4 stages of an XHR request:
    open -> headers received -> loading -> done
    Most of the time we're interested in the `done` state, so we check
    `xhr.readyState === XMLHttpRequest.DONE`
  -->
- When to use the `load` event?
  <!--
    The load event can be used to detect a fully-loaded page. (each stylesheet,
    image, subframes, etc...)
    It is fired on the window element, window.addEventListener('load', ...);
  -->
- (Optional) What event fires when the document is fully ready to be used?
   <!--
     The `DOMContentLoaded` event is fired when the document has been completely
     loaded and parsed, without waiting for stylesheets, images, and subframes
     to finish loading
     It is fired on the document object,
     document.addEventListener('DOMContentLoaded, ...);
   -->
- What's the event target?
  <!--
    EventTarget is an interface implemented by objects that can receive events
    and may have listeners for them.
    Element, document, and window are the most common event targets, but other
    objects can be event targets too, for example XMLHttpRequest, AudioNode,
    AudioContext, and others.
  -->
- How and when to remove the event listener?
  <!--
    `removeEventListener()`: best practice is the remove the event listener once
    it's not needed any more to spare resources: CPU and memory,
    and generally to avoid bugs.
  -->
- (Optional) How to fire an event programmatically?
  <!-- `dispatchEvent`
    Fires the event on the EventTarget
  -->
- What's event bubbling?
  <!--
    The browser checks to see if the element that was actually clicked on has an
    onclick event handler registered on it in the bubbling phase, and runs it if
    so.
    Then it moves on to the next immediate ancestor element and does the same
    thing, then the next one, and so on until it reaches the <html> element.
  -->
- What's the difference between `event.target` and `event.currentTarget`?
  <!--
    event.target: the originator HTMLElement which dispatched the event
    event.currentTarget: the HTMLElement on we handle the event
  -->
- How to cancel the default behavior of the browser (e.g. how to cancel the
  form submit)?
  <!--
    The `preventDefault()` method prevents the default behavior, like anchor
    navigation and form submission
  -->

## Workshop

```javascript
const button = document.querySelector('button');
const alertGreenFox = () => {
  alert('Green Fox!');
};
button.addEventListener('click', alertGreenFox);
```

### Example

You can find the above JavaScript code in HTML format:

- [events.html](assets/events.html)

### Exercises

- [Count the elements](counter/counter.html)
- [Keyup Event](keyup/keyup.html)
- [One Time Clicker](click-once/click-once.html)
- [Bubbling](bubbling/bubbling.html)
- [Delayed Click](delayed-click/README.md)
- [Click Three Times](click-three-times/README.md)
- [Candy Game](candy-game/game.js), [HTML](candy-game/game.html)

### Advanced exercises

- [Infinite scroll 💪](infinite-scroll/README.md)
- [Dispatch click](dispatch-click/index.html)
- [Custom events 💪💪](custom-events/index.html)

## Individual Workshop Review

Please follow the styleguide: [Our JavaScript styleguide](../../styleguide/javascript.md)

- Is the directory structure and the name of the files correct?
- Is every file in strict mode?
- Is the indentation good in each file?
- Is there unnecessary code?
- Can you find unnecessary code in comments?
- Is there unnecessary code duplication?
- Are there unnecessary empty blocks?
- Can you spot unused variables?
