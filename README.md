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

![appendChoiceTo](./Screenshots/clearPendingUIEvents.png)

![appendChoiceTo](./Screenshots/wheneverUIEventOccurredWithin.png)

![appendChoiceTo](./Screenshots/wheneverUIEventOccurred.png)

![appendChoiceTo](./Screenshots/ButtonWasClicked.png)

![appendChoiceTo](./Screenshots/InputWasChanged.png)

![appendChoiceTo](./Screenshots/leaveUIEventLoop.png)

### AI Basics ###

(t.b.w.)

### AI Mezzanines ###

(t.b.w.)

### AI Tools ###

(t.b.w.)

### Miscellany ###

(t.b.w.)

![wait](./Screenshots/wait.png)

![alert](./Screenshots/alert.png)

![confirm](./Screenshots/confirm.png)

![prompt](./Screenshots/prompt.png)

![ValueIsNonEmpty](./Screenshots/ValueIsNonEmpty.png)

![ValueIsNumber](./Screenshots/ValueIsNumber.png)

![ValueIsNumberInRange](./Screenshots/ValueIsNumberInRange.png)

![ValueIsInteger](./Screenshots/ValueIsInteger.png)

![ValueIsIntegerInRange](./Screenshots/ValueIsIntegerInRange.png)

![ValueIsOrdinal](./Screenshots/ValueIsOrdinal.png)

![ValueIsCardinal](./Screenshots/ValueIsCardinal.png)

![ValueIsStringMatching](./Screenshots/ValueIsStringMatching.png)

![ValueIsURL](./Screenshots/ValueIsURL.png)

![ValueIsWikipediaURL](./Screenshots/ValueIsWikipediaURL.png)

## Examples ##

(t.b.w.)

## License ##

[MIT License](LICENSE.md)
