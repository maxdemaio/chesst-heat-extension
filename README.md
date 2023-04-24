# chess-heat-extension

---

## How it works

The `popup.js` script is loaded by the `index.html` file when the user clicks on the extension icon. This script is responsible for modifying the content of index.html and updating the user interface.

The `background.js` script is loaded by the browser as soon as the extension is installed and runs in the background as long as the extension is enabled. This script is responsible for intercepting events from the browser (like clicking on the extension icon) and executing code in response to these events.

In the case of our Chess Heat example, when the user clicks on the extension icon, the `popup.js` script is executed and it sends a message to the background.js script requesting the name of the chess.com username in the current active tab. The background.js script receives this message and responds with the member name in the current tab. The `popup.js` script then receives the response and updates the content of `index.html` based on the member name. If it can't find a member name (`{name: null}`) response from `background.js`), it'll just display an error.

So the `background.js` script acts as a mediator between the `popup.js` script and the current browser tab, allowing the popup to access information from the tab without having direct access to it.

Fun find: Devtools windows are ignored by the tabs.query API. This means `tabs` will be an empty array when you try and refresh with the Devtools window open for the extension's `index.html` file and you refresh with `Ctrl+R`. So, what you should do is just open the extension and then look at the console errors afterwards in the extension's `index.html` Devtools. Link to this: https://bugs.chromium.org/p/chromium/issues/detail?id=462939.
