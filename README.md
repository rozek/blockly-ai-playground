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

"blockly-ai-playground" can be used with any AI provider offering an [OpenAI compatible API](https://platform.openai.com/docs/api-reference) - this may be [OpenAI](https://openai.com/) itself, [Perplexity](https://www.perplexity.ai/) (which was used for development), [Ollama](https://ollama.com/) (which runs LLMs locally on one's computer) and, presumably, many others.

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

(t.b.w.)

![ContextKeys](./Screenshots/ContextKeys.png)

![clearContext](./Screenshots/clearContext.png)

![getFromContext](./Screenshots/getFromContext.png)

![setInContext](./Screenshots/setInContext.png)

![removeFromContext](./Screenshots/removeFromContext.png)

### Playground UI ###

(t.b.w.)

![showWorkspace](./Screenshots/showWorkspace.png)

![showUI](./Screenshots/showUI.png)

![UIElements](./Screenshots/UIElements.png)

![UIhasElement](./Screenshots/UIhasElement.png)

![clearUI](./Screenshots/clearUI.png)

![removeFromUI](./Screenshots/removeFromUI.png)

![appendTextlineInput](./Screenshots/appendTextlineInput.png)

![appendPasswordInput](./Screenshots/appendPasswordInput.png)

![appendURLInput](./Screenshots/appendURLInput.png)

![appendTextInput](./Screenshots/appendTextInput.png)

![appendCheckbox](./Screenshots/appendCheckbox.png)

![appendRadiobuttonGroup](./Screenshots/appendRadiobuttonGroup.png)

![appendDropDown](./Screenshots/appendDropDown.png)

![appendButton](./Screenshots/appendButton.png)

![appendTextlineOutput](./Screenshots/appendTextlineOutput.png)

![appendNumberOutput](./Screenshots/appendNumberOutput.png)

![appendTextOutput](./Screenshots/appendTextOutput.png)

![appendText](./Screenshots/appendText.png)

![appendFinePrint](./Screenshots/appendFinePrint.png)

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

![appendChoiceTo](./Screenshots/appendChoiceTo.png)


![clearConsole](./Screenshots/clearConsole.png)

![print](./Screenshots/print.png)

![println](./Screenshots/println.png)


![clearPendingUIEvents](./Screenshots/clearPendingUIEvents.png)

![wheneverUIEventOccurredWithin](./Screenshots/wheneverUIEventOccurredWithin.png)

![wheneverUIEventOccurred](./Screenshots/wheneverUIEventOccurred.png)

![ButtonWasClicked](./Screenshots/ButtonWasClicked.png)

![InputWasChanged](./Screenshots/InputWasChanged.png)

![leaveUIEventLoop](./Screenshots/leaveUIEventLoop.png)

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

### Hello, World ###

![Hello_World](./Examples/Hello_World.png)

> this is the typical "Hello, World" example (see [Blockly workspace file](./Examples/Hello_World.json))

### Console ###

![Console](./Examples/Console.png)

> this example illustrates all Console functions (see [Blockly workspace file](./Examples/Console.json))

### Suspend, Resume, Abort ###

![Suspend_Resume_Abort](./Examples/Suspend_Resume_Abort.png)

> use this little Blockly program to get familiar with "Suspend", "Resume" and "Abort" (see [Blockly workspace file](./Examples/Suspend_Resume_Abort.json))

## License ##

[MIT License](LICENSE.md)
