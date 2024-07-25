# blockly-ai-playground #

experiment with AI and build your own AI agents using Blockly - even if you are a complete beginner! (also suitable for school lessons)

> (Work in progress - intended as a contribution to the [Backdrop Build](https://backdropbuild.com/) contest, please stay tuned - contest ends at July, 31st)

[Live Demo](https://rozek.github.io/blockly-ai-playground/LiveDemo) **Warning: this is currently just a "proof-of-concept" which only runs an inference on a given OpenAI-compatible Server (tested with [Perplexity](https://www.perplexity.ai/)). More interesting blocks will follow in the next few days**

![Live Demo Screenshot](https://rozek.github.io/blockly-ai-playground/LiveDemo/Screenshot.png)

## Overview ##

AI agents are "cool" these days and can be found at many places - but for most of us, they are basically just "black boxes" which do not reveal how they work internally.

[Blockly](https://developers.google.com/blockly) is a visual programming environment developed by Google that allows users to create code using drag-and-drop "Lego"-like blocks. It is designed to simplify coding by abstracting away the syntax, making it accessible for beginners and educational purposes.

By combining these two technologies, the "blockly-ai-playground" offers beginners and casual programmers an easy way to play and experiment with AI and build their own AI agents!

## Prerequisites ##

The "blockly-ai-playground" can be used with any AI provider offering an [OpenAI compatible API](https://platform.openai.com/docs/api-reference) - this may be [OpenAI](https://openai.com/) itself, [Perplexity](https://www.perplexity.ai/) (which was used for development), [Ollama](https://ollama.com/) (which runs LLMs locally on one's computer) and, presumably, many others.

As a consequence, you will need

* the **URL of an API entry point** (either locally on your machine or on the internet) and
* an **API Access Key** if you are using an official AI provider

While you may already use large language models (LLMs) on their own, they can only show their true capabilities in combination with other tools - this is what makes "agents" so powerful.

One of these tools is the web search. Since automating search engines is quite tedious, the "blockly-ai-playground" uses [SearXNG](https://docs.searxng.org/) for that purpose. Although there are several [public servers](https://searx.space/) which offer a web interface similar to other search engines, the [SearXNG API](https://docs.searxng.org/dev/search_api.html) is normally not publically available and you should run your own SearXNG instance instead (which does not have to be public but may remain private) - fortunately, installation is really simple if you use [Docker](https://www.docker.com/) (which is free for personal use, choose "Docker Desktop" rather than the CLI version - it is much simpler to maintain)

Thus, if you want to use the built-in web search, you should install

* [Docker Desktop](https://www.docker.com/products/docker-desktop/)
* [SearXNG](https://docs.searxng.org/admin/installation-docker.html)

## Custom Blocks ###

Besides common blocks which can be found in many Blockly environments, the "blockly-ai-playground" also provides a set of custom blocks to manage an internal context, a simple (but dynamic) user interface, basic and enhanced functions for AI, auxiliary tools for AI agents and other useful functions.

### Playground Context ###

The playground manages a dynamic "context" which is a collection of "items", consisting of a "value" (typically a boolean, number or string) and its unique "name". Context items can store settings (e.g., the URL of an API server, its access key or the AI model to use) or intermediate results generated by an agent or they provide a link between an agent and its user interface.

> Please note, that context item names are case-sensitive.

Some context items are already used internally, these are

* `APIServer` - the URL (and base path) of the OpenAI-compatible API you plan to use
* `APIKey` - your API Access Key (if required)
* `SearXNGServer` - the URL of your SearXNG server (preset to `http://127.0.0.1:8080`)

the inferencing parameters

* `default_model` - the model to use for completions (no preset, as it highly depends on the configured API Server)
* `default_max_tokens` - the maximum number of completion tokens to be returned (preset to 2048)
* `default_temperature` - the "response randomness" setting (0...2, preset to 0)
* `default_top_p` - the "nucleus sampling threshold" setting (0...1, no preset)
* `default_top_k` - the "top-k filtering setting" setting (0...2048, preset to 1)
* `default_presence_penalty` - the "token presence penalty" setting (-2...2, preset to 1)
* `default_frequency_penalty` - the "token frequency penalty" setting (0..., no preset)
* `default_SystemTemplate` - the default template for the "system" message in a chat (preset to `Be precise and concise.`)
* `default_UserTemplate` - the default template for the "user" message in a chat (preset to `{{Prompt}}`)

and

* `Prompt` - the prompt to be sent to the AI model (preset to `who was Joseph Weizenbaum?`)
* `Console` - the current contents of the built-in "Console" (initially empty)

![ContextKeys](./Screenshots/ContextKeys.png)

> returns a list with the names of all currently defined context items (see [Context example](#context))

![clearContext](./Screenshots/clearContext.png)

> clears the context (i.e., deletes all currently defined context items) (see [Context example](#context))

![getFromContext](./Screenshots/getFromContext.png)

> returns the current value of a given context item. If the requested item does not exist, `undefined` is returned (see [Context example](#context))

![setInContext](./Screenshots/setInContext.png)

> sets the given context item to the given value. If the addressed item does not exist, it will be created (see [Context example](#context))

![removeFromContext](./Screenshots/removeFromContext.png)

> removes the given context item. It is safe to remove an item which does not exist (see [Context example](#context))

### Playground UI ###

The playground also manages a programmable reactive "user interface" (aka "UI"). The playground UI is basically a vertical list of user interface "elements", often preceeded by a "label".

Every UI element has a unique "name" which is bound to a context item with the same name. As a consequence,

* changing the value of a context item automatically updates the contents of a bound UI element and
* entering data into a UI element automatically updates the assciated context item

This concept makes UI programming super easy.

#### Event Loop ####

Often, a program has to react on user inputs. In the simplest way, this just means to present a few input fields to the user (e.g., to enter `APIServer`, `APIKey` and a `Prompt`) and start inferencing as soon as the user has pressed a button. In the meantime, the UI may also be used to inform the user about the validity of any inputs while (s)he is entering them.

This is achieved by an "event loop".

#### Enabling ####

(t.b.w.)

![showWorkspace](./Screenshots/showWorkspace.png)

> makes the Blockly workspace visible

![showUI](./Screenshots/showUI.png)

> makes the user interface visible

![UIElements](./Screenshots/UIElements.png)

> returns a list with the names of all currently defined UI elements

![UIhasElement](./Screenshots/UIhasElement.png)

> returns `true` if the UI currently contains an element with the given name - (or `false` otherwise

![clearUI](./Screenshots/clearUI.png)

> clears the user interface (i.e., deletes all currently defined UI elements)

![removeFromUI](./Screenshots/removeFromUI.png)

> removes the element with the given name from the UI. It is safe to remove an element which does not exist

![appendTextlineInput](./Screenshots/appendTextlineInput.png)

> appends a textline input element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendPasswordInput](./Screenshots/appendPasswordInput.png)

> appends a password input element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendURLInput](./Screenshots/appendURLInput.png)

> appends a URL input element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendTextInput](./Screenshots/appendTextInput.png)

> appends a (multiline) text input element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendCheckbox](./Screenshots/appendCheckbox.png)

> appends a checkbox element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendRadiobuttonGroup](./Screenshots/appendRadiobuttonGroup.png)

> appends a radio button group element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendDropDown](./Screenshots/appendDropDown.png)

> appends a drop-down element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendButton](./Screenshots/appendButton.png)

> appends a button element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendTextlineOutput](./Screenshots/appendTextlineOutput.png)

> appends a textline output element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendNumberOutput](./Screenshots/appendNumberOutput.png)

> appends a number output element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendTextOutput](./Screenshots/appendTextOutput.png)

> appends a (multiline) text output element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendText](./Screenshots/appendText.png)

> appends an unlabelled text view element with the given name to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendFinePrint](./Screenshots/appendFinePrint.png)

> appends an unlabelled "fine print" view element with the given name to the UI. If an element with the same name already exists, it is removed before the new one is appended

![configureUI](./Screenshots/configureUI.png)

> sets the current value of a given option for an UI element with the given key to a given value. If no element with the given key can be found, an exception is thrown and the program aborted. Which options and option values are meaningful (and, thus, used by the UI), depends on the type of the given UI element

![ConfigurationOf](./Screenshots/ConfigurationOf.png)

> returns the current value of a given option for an UI element with the given key. If no element with the given key can be found, an exception is thrown and the program aborted. The requested option does not have to exist

![EnablingOf](./Screenshots/EnablingOf.png)

> returns `true` if an UI element with the given key is enabled or `false` otherwise. If no element with the given key can be found, an exception is thrown and the program aborted.

![enable](./Screenshots/enable.png)

> enables the UI element with the given key. If no element with the given key can be found, an exception is thrown and the program aborted.

![disable](./Screenshots/disable.png)

> disables the UI element with the given key. If no element with the given key can be found, an exception is thrown and the program aborted.

![isEnabled](./Screenshots/isEnabled.png)

> returns `true` if an UI element with the given key (exists and) is enabled. If no element with the given key can be found, an exception is thrown and the program aborted.

![clearChoicesOf](./Screenshots/clearChoicesOf.png)

> clears all currently defined choices of a radiobutton group or a drop-down element

![appendChoiceTo](./Screenshots/appendChoiceTo.png)

> appends the given text to the list of choices for a radiobutton group or a drop-down element

![clearConsole](./Screenshots/clearConsole.png)

> clears the built-in "Console" (see [Console example](#console))

![print](./Screenshots/print.png)

> appends the given string to the built-in "Console" (see [Console example](#console))

![println](./Screenshots/println.png)

> appends the given string to the built-in "Console" and starts a new line (see [Console example](#console))

![clearPendingUIEvents](./Screenshots/clearPendingUIEvents.png)

> removes all pending UI events from the internal queue. If there are no pending events, this statement is simply ignored

![wheneverUIEventOccurredWithin](./Screenshots/wheneverUIEventOccurredWithin.png)

> starts an event loop and runs the given statements whenever a new UI event was received. If the given timeout is `0` the loop is exited as soon as no more UI events are pending. If the given timeout is greater than `0` the loop is exited if no event was received within the given number of seconds. With a negative timeout, the loop waits indefinitely for the next UI event

![wheneverUIEventOccurred](./Screenshots/wheneverUIEventOccurred.png)

> starts an event loop and runs the given statements whenever a new UI event was received, waiting indefinitely for new events

![ButtonWasClicked](./Screenshots/ButtonWasClicked.png)

> returns `true` if the currently processed UI event is a click on a button with the given name - or `false` otherwise

![InputWasChanged](./Screenshots/InputWasChanged.png)

> returns `true` if the currently processed UI event indicates that new input for the UI element with the given name was received - or `false` otherwise

![leaveUIEventLoop](./Screenshots/leaveUIEventLoop.png)

> leaves the current event loop

### AI Basics ###

(t.b.w.)

### AI Mezzanines ###

(t.b.w.)

### AI Tools ###

(t.b.w.)

### Miscellany ###

The following blocks do not fit into the categories shown before - may may still be helpful when creating agents:

![wait](./Screenshots/wait.png)

> waits for a given number of seconds and continues (see [Console example](#console))

![alert](./Screenshots/alert.png)

> opens a browser "alert" pop-up dialog, displays the given message and continues as soon as the user has closed the dialog

![confirm](./Screenshots/confirm.png)

> opens a browser "confirmation" pop-up dialog, displays the given message and continues as soon as the user has responded with "ok" or "Cancel". If cancelled, the block returns `false`, otherwise it returns `true`

![prompt](./Screenshots/prompt.png)

> opens a browser "prompt" pop-up dialog, displays the given message and continues as soon as the user has entered a response. If cancelled, the block returns an empty string, otherwise it returns the entered string

![ValueIsNonEmpty](./Screenshots/ValueIsNonEmpty.png)

> returns `true` if the given value contains a string that is neither empty nor contains whitespace only - or `false` otherwise

![ValueIsNumber](./Screenshots/ValueIsNumber.png)

> returns `true` if the given value contains a number - or `false` otherwise

![ValueIsNumberInRange](./Screenshots/ValueIsNumberInRange.png)

> returns `true` if the given value contains a number with a value ranging from the given minimum to the given maximum - or `false` otherwise. The additional arguments "withMinimum" and "withMaximum" specify wether the given "minimum" and "maximum" values are themselves part of that range or not

![ValueIsInteger](./Screenshots/ValueIsInteger.png)

> returns `true` if the given value contains an integer number - or `false` otherwise

![ValueIsIntegerInRange](./Screenshots/ValueIsIntegerInRange.png)

> returns `true` if the given value contains an integer number with a value ranging from the given minimum to the given maximum - or `false` otherwise

![ValueIsOrdinal](./Screenshots/ValueIsOrdinal.png)

> returns `true` if the given value contains an "ordinal" number (i.e., an integer greater than or equal to 0) - or `false` otherwise

![ValueIsCardinal](./Screenshots/ValueIsCardinal.png)

> returns `true` if the given value contains a "cardinal" number (i.e., an integer greater than or equal to 1) - or `false` otherwise

![ValueIsStringMatching](./Screenshots/ValueIsStringMatching.png)

> returns `true` if the given value contains a string that matches a given JavaScript regular expression - or `false` otherwise

![ValueIsURL](./Screenshots/ValueIsURL.png)

> returns `true` if the given value contains a string that looks like a URL - or `false` otherwise

![ValueIsWikipediaURL](./Screenshots/ValueIsWikipediaURL.png)

> returns `true` if the given value contains a string that looks like a Wikipedia document URL - or `false` otherwise

## Examples ##

Here are a few examples which you can uploda into the Blockly workspace to get familiar with Blockly itself and the custom blocks specifically made for the "blockly-ai-playground"

### Hello, World ###

![Hello_World](./Examples/Hello_World.png)

> this is the typical "Hello, World" example (see [Blockly workspace file](./Examples/Hello_World.json))

### Console ###

![Console](./Examples/Console.png)

> this example demonstrates all Console functions (see [Blockly workspace file](./Examples/Console.json))

### Suspend, Resume, Abort ###

![Suspend_Resume_Abort](./Examples/Suspend_Resume_Abort.png)

> use this little Blockly program to get familiar with "Suspend", "Resume" and "Abort" (see [Blockly workspace file](./Examples/Suspend_Resume_Abort.json))

### Context ###

![Context](./Examples/Context.png)

> this example demonstrates all context functions (see [Blockly workspace file](./Examples/Context.json))

## License ##

[MIT License](LICENSE.md)
