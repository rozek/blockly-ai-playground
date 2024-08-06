<center>
  <a href="#prerequisites">Prerequisites</a> |
  <a href="#browser-troubleshooting">Browser Troubleshooting</a> |
  <a href="#current-status-and-future-plans">Future plans</a> |
  <a href="#playground-context">Playground Context</a> |
  <a href="#playground-ui">Playground UI</a> |
  <a href="#ai-basics">AI Basics</a> |
  <a href="#ai-mezzanines">AI Mezzanines</a> |
  <a href="#ai-support">AI Support</a> |
  <a href="#miscellany">Miscellany</a> |
  <a href="#object-support">Object Support</a> |
  <a href="#examples">Simple Examples</a> |
  <a href="#ai-examples">AI Examples</a>
</center>

# blockly-ai-playground #

experiment with AI and build your own AI agents using Blockly - even if you are a complete beginner! (also suitable for school lessons)

**Build your own Copilot - with Blockly - the video will show you how well it can perform (even in comparison with the original)!** (sorry for the bad quality: the video had to be created in a hurry)

[![Backdrop Build Launch Video](./Video-Thumbnail.webp)](https://www.youtube.com/watch?v=_JJzPLHObiY)

> (Work in progress - it was my contribution to the [Backdrop Build v5](https://backdropbuild.com/) contest and had to be launched as an MVP before their deadline. I'm now working on polishing it up...)

[Live Demo](https://rozek.github.io/blockly-ai-playground/LiveDemo) **Warning: please read "Overview" and "Prerequisites" first**

> **Import News: you no longer need to install your own SearXNG Server to perform web searches - just leave the SearXNGServer context item empty!**

> **CORS note: modern browser security measures may complicate API requests. To succeed, you may have to install a "CORS Unblocking" extension into your browser (like [this](https://chromewebstore.google.com/detail/cross-domain-cors/mjhpgnbimicffchbodmgfnemoghjakai) one)**

> **Recommendation: start with the [basic Settings example](#basic-settings) and enter your `APIServer`, `APIKey` and `default_model` settings, at least. Then use the [PoC example](#text-completion-proof-of-concept) and run your first inferences. Later, you may also try the [AI-assisted Web Search](#ai-web-search) and the [AI Agent](#ai-agent) to learn about the benefits of "AI agents"**

> **Please note: the "blockly-ai-playground" has only been tested with Perplexity AI on a Mac so far. Additionally, the performance of generative AI is hard to predict - as a consequence, your mileage may vary when compared to what you saw in the video**

![Live Demo Screenshot](https://rozek.github.io/blockly-ai-playground/LiveDemo/Screenshot.png)

> You have comments, wishes or ideas? You found a bug? Then [open an issue](https://github.com/rozek/blockly-ai-playground/issues). You like this tool and plan to use it? Then leave a star!

## Overview ##

AI agents are "cool" these days and can be found at many places - but for most of us, they are basically just "black boxes" which do not reveal how they work internally.

[Blockly](https://developers.google.com/blockly) is a visual programming environment developed by Google that allows users to create code using drag-and-drop "Lego"-like blocks. It is designed to simplify coding by abstracting away the syntax, making it accessible for beginners and educational purposes.

By combining these two technologies, the "blockly-ai-playground" offers beginners and casual programmers an easy way to play and experiment with AI and build their own AI agents!

## Prerequisites ##

The "blockly-ai-playground" can be used with any AI provider offering an [OpenAI compatible API](https://platform.openai.com/docs/api-reference) - this may be [OpenAI](https://openai.com/) itself, [Perplexity](https://www.perplexity.ai/) (which was used for development), [Ollama](https://ollama.com/) (which runs LLMs locally on one's computer) and, presumably, many others.

As a consequence, you will need

* the **URL of an API entry point** (either locally on your machine or on the internet) and
* an **API Access Key** if you are using an official AI provider

## Browser Troubleshooting ##

Modern browser security may cause a lot of trouble when a web application wants to communicate with servers that have not been configured properly. If you know what you are doing, you may lower specific security levels in order to get the experience you expect.

### CORS ###

t.b.w.

### Communicating with you own PC ###

t.b.w.

## Current Status and Future Plans ##

As you can see in the video, the "blockly-ai-playground" is principally working. However, due to the haste with which development had to take place, the result should only be considered as a "minimum viable product" (MVP) as it still requires a lot of "polishing" before it will be as easy to use as it should be for beginners.

These are my plans for the near future:

* create more examples (in the end, every custom block should be covered by at least one example)
* make sure that everything is working properly in the most important browsers and on the most important platforms (including tablets, but not smartphones - their displays are just too small)
* **important: create a "Browser Troubleshooting" section!**
* quick notes on how to get and install Ollama (perhaps together with Open-WebUI)
* create a tutorial for real beginners (perhaps with tutorial videos?)
* use a bundler (vite) to make a real web app out of the playground
* use some of the available Blockly plugins to enhance the user interface
* create a desktop application (NW.js or Electron.js)
* create installers for Windows/Linux/macOS, provide update paths (e.g., similar to the GitHub Desktop)
* detect browser security violations (TLS, CORS etc.) and give user-friendly error messages with suggestions how to fix them

The idea is to have a beginner-friendly version ready for the next lecture season (starting in October)

## Custom Blocks ###

Besides common blocks which can be found in many Blockly environments, the "blockly-ai-playground" also provides a set of custom blocks to manage an internal context, a simple (but dynamic) user interface, basic and enhanced functions for AI, auxiliary tools for AI agents and other useful functions.

### Playground Context ###

The playground manages a dynamic "context" which is a collection of "items", consisting of a "value" (typically a boolean, number or string) and its unique "name". Context items can store settings (e.g., the URL of an API server, its access key or the AI model to use) or intermediate results generated by an agent or they provide a link between an agent and its user interface.

> Please note, that context item names are case-sensitive.

Some context items are already used internally, these are

* `APIServer` - the URL (and base path) of the OpenAI-compatible API you plan to use
* `APIKey` - your API Access Key (if required)
* `SearXNGServer` - the URL of your own SearXNG server (just leave it empty if you don't have one - in that case, a random public server will be looked-up and used instead)

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

* `Console` - the current contents of the built-in "Console" (initially empty)

In addition to the items listed above, "AI Mezzanine" blocks provide their own context items in order to allow customization of their internal API calls. To find these items, simply replace the `default` prefix of the inferencing parameter items by the prefix for the given mezzanine (e.g., 'summarizer_max_tokens' specifies the token generation limit for text summarization). If any mezzanine-specific context item is removed (or empty) the related default setting is used instead.

#### Preserve and Restore ####

During development it is sometimes useful to keep settings and values beyond the life-time of a single program. Typical use case are:

* you use one Blockly program to define APIServer, APIKey or other settings and use these settings in other Blockly programs
* you save intermediate results of API calls in order to avoid having to rerun them after restarting an AI-assisted application

![preserveContextItem](./Screenshots/preserveContextItem.png)
![restoreContextItem](./Screenshots/restoreContextItem.png)

These two blocks provide such a functionality: use the first block to preserve a given context item and the second to restore it later

#### Context-related Blocks ####

![ContextKeys](./Screenshots/ContextKeys.png)

> returns a list with the names of all currently defined context items (see [related example](#context))

![clearContext](./Screenshots/clearContext.png)

> clears the context (i.e., deletes all currently defined context items) (see [related example](#context))

![getFromContext](./Screenshots/getFromContext.png)

> returns the current value of a given context item. If the requested item does not exist, `undefined` is returned (see [related example](#context))

![setInContext](./Screenshots/setInContext.png)

> sets the given context item to the given value. If the addressed item does not exist, it will be created (see [related example](#context))

![removeFromContext](./Screenshots/removeFromContext.png)

> removes the given context item. It is safe to remove an item which does not exist (see [related example](#context))

![preserveContextItem](./Screenshots/preserveContextItem.png)

> preserves the given context item (as a string) in the Browser Storage. If the addressed item does not exist, an empty string will be preserved (see [related example](#preserve-restore))

![restoreContextItem](./Screenshots/restoreContextItem.png)

> restores the given context item (as a string) from the Browser Storage. If the addressed item was not preserved before, the context item will be set to an empty string (see [related example](#preserve-and-restore))

### Playground UI ###

The playground also manages a programmable reactive "user interface" (aka "UI"). The playground UI is basically a vertical list of user interface "elements", often preceeded by a "label".

Every UI element has a unique "name" which is bound to a context item with the same name. As a consequence,

* changing the value of a context item automatically updates the contents of a bound UI element and
* entering data into a UI element automatically updates the assciated context item

This concept makes UI programming super easy.

#### Event Loop ####

Often, a program has to react on user inputs. In the simplest way, this just means to present a few input fields to the user (e.g., to enter `APIServer`, `APIKey` and a `Prompt`) and to start inferencing as soon as the user has pressed a button. In the meantime, the UI may also be used to inform the user about the validity of any inputs while (s)he is entering them.

This is achieved by an "event loop".

![showWorkspace](./Screenshots/wheneverUIEventOccurredWithin.png)
![showWorkspace](./Screenshots/wheneverUIEventOccurred.png)

The core of any event loop is one of the blocks shown above. Each of them waits for incoming UI "events" (which indicate that the user has entered some data or clicked on a button) and then executes a sequence of inner blocks (the so called "loop body").

![showWorkspace](./Screenshots/ButtonWasClicked.png)
![showWorkspace](./Screenshots/InputWasChanged.png)

Within the loop body you may now check what the user actually did and react accordingly - this is what the two blocks shown above are good for:

* the first one returns `true` if a button with the given name was pressed and
* the second one returns `true` if the user entered new data into an input element with the given name

Both blocks are typically placed into the condition field of an "if-then" block to run the "then" clause only if the given button was pressed or the given input element received new data.

![showWorkspace](./Screenshots/leaveUIEventLoop.png)

The loop body is executed over and over again - until the loop is exited using the block shown above.

A Blockly program may contain several event loops - but only one of them may be running at the same tine (i.e., **event loops must not be nested**).

#### Enabling ####

Often, a programmer wants to prevent buttons to be clicked or new data entered into input fields. Typical situations are

* users should not be able to start inferencing by pressing a "Submit" button before `APIServer`, `APIKey` and `Prompt` were entered (and valid)
* users should not be able to interact with the UI while an API request is running

This behaviour is achieved by "enabling" or "disabling" either the UI as a whole or specific UI elements only.

![UIElements](./Screenshots/enableUI.png)
![UIElements](./Screenshots/disableUI.png)

The two blocks shown above enable or disable the playground UI in its entirety. Disabling the whole UI disables all UI elements, while "enabling" the whole UI means that the enabling of every UI element depends on its own setting (i.e., elements may still be individually disabled)

![UIElements](./Screenshots/enable.png)
![UIElements](./Screenshots/disable.png)

These two blocks enable or disable specific UI elements.

#### UI-related Blocks ####

![showWorkspace](./Screenshots/showWorkspace.png)

> switches to the playground workspace pane

![showUI](./Screenshots/showUI.png)

> switches to the playground user interface pane

![UIElements](./Screenshots/enableUI.png)

> (re-)enables the playground UI in its entirety. Please note that "enabling the whole UI" only means that the UI is no longer disabled in its entirety and every UI element is now enabled or disabled depending on its own setting (see [related example](#enable-and-disable))

![UIElements](./Screenshots/disableUI.png)

> disables the playground UI in its entirety (see [related example](#enable-and-disable))

![UIElements](./Screenshots/UIElements.png)

> returns a list with the names of all currently defined UI elements

![UIhasElement](./Screenshots/UIhasElement.png)

> returns `true` if the UI currently contains an element with the given name - or `false` otherwise

![clearUI](./Screenshots/clearUI.png)

> clears the user interface (i.e., deletes all currently defined UI elements)

![removeFromUI](./Screenshots/removeFromUI.png)

> removes the element with the given name from the UI. It is safe to remove an element which does not exist

![appendTextlineInput](./Screenshots/appendTextlineInput.png)

> appends a textline input element (based on an [HTML input element of type "text"](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text)) with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended. This element supports the options `Placeholder`, `readonly`, `minLength`, `maxLength`, `Pattern`, `SpellChecking` and `Enabling` (see [related example](#textline-input))

![appendPasswordInput](./Screenshots/appendPasswordInput.png)

> appends a password input element (based on an [HTML input element of type "password"](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/password)) with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended. This element supports the options `Placeholder`, `readonly`, `minLength`, `maxLength`, `Pattern` and `Enabling`

![appendNumberInput](./Screenshots/appendNumberInput.png)

> appends a number input element (based on an [HTML input element of type "number"](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number)) with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended. This element supports the options `Placeholder`, `readonly`, `Minimum`, `Maximum`, `Stepping` and `Enabling`

![appendURLInput](./Screenshots/appendURLInput.png)

> appends a URL input element (based on an [HTML input element of type "url"](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/url)) with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended. This element supports the options `Placeholder`, `readonly`, `minLength`, `maxLength`, `Pattern` and `Enabling`

![appendTextInput](./Screenshots/appendTextInput.png)

> appends a (multiline) text input element (based on an [HTML textarea](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea)) with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended. This element supports the options `Placeholder`, `readonly`, `minLength`, `maxLength`, `LineWrapping`, `SpellChecking` and `Enabling`

![appendSpeechInput](./Screenshots/appendSpeechInput.png)

> appends an input element (with the given name and label) to the UI that can be used to listen to and recognize what a user says into a microphone. If an element with the same name already exists, it is removed before the new one is appended. This element supports the options `Placeholder`, `readonly`, `minLength`, `maxLength`, `LineWrapping`, `SpellChecking` and `Enabling` (see [related example](#speechinput))

> Nota bene: speech recognition requires microphone access - for that reason the browser may ask for permission to use your PC's microphone. Recognition will only work if you grant that permission - or else fail.

> **Important: not all browsers support speech recognition (Chrome seems to, but other browsers may not - even if they are based on webkit). Additionally, the playground must be served over valid (and secure!) HTTPS**

![appendCheckbox](./Screenshots/appendCheckbox.png)

> appends a checkbox element (based on an [HTML input element of type "checkbox"](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox)) with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended. This element only supports the option `Enabling`

![appendRadiobuttonGroup](./Screenshots/appendRadiobuttonGroup.png)

> appends a radio button group element (based on an [HTML input elements of type "radio"](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio)) with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended.
>
> Radiobutton groups are a bit special as they contain a whole group of radio buttons, each with its own label. As a consequence, after appending a new radio button group element, you will have to define a list of radio buttons using the "append Choice" block - and the value of the whole group (i.e., the associated context item) is the (0-based) index of the currently checked radio button (or `-1` if no button is checked) (see [related example](#radiobutton-group))

![appendDropDown](./Screenshots/appendDropDown.png)

> appends a drop-down element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended
>
> After adding a new DropDown to the UI, you still have to define the entries from which the user may select. This can be done using the "append Choice" block - one per selectable entry. The context item associated with the DropDown will then contain the (0-based) index of the currently selected entry

![appendButton](./Screenshots/appendButton.png)

> appends a button element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended

![appendTextlineOutput](./Screenshots/appendTextlineOutput.png)

> appends a textline output element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended (see [related example](#output-elements))

![appendNumberOutput](./Screenshots/appendNumberOutput.png)

> appends a number output element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended (see [related example](#output-elements))

![appendTextOutput](./Screenshots/appendTextOutput.png)

> appends a (multiline) text output element with the given name and label to the UI. If an element with the same name already exists, it is removed before the new one is appended (see [related example](#output-elements))

![appendText](./Screenshots/appendText.png)

> appends an unlabelled text view element with the given name to the UI. If an element with the same name already exists, it is removed before the new one is appended (see [related example](#output-elements))

![appendFinePrint](./Screenshots/appendFinePrint.png)

> appends an unlabelled "fine print" view element with the given name to the UI. If an element with the same name already exists, it is removed before the new one is appended (see [related example](#output-elements))

![appendAPIServerInput](./Screenshots/appendAPIServerInput.png)

> appends a URL input element customized for the selection or input of the `APIServer` context item with the given label to the UI. If an element with the name `APIServer` already exists, it is removed before the new one is appended. This element supports the options `Placeholder`, `readonly`, `minLength`, `maxLength`, `Pattern` and `Enabling`

![configureUI](./Screenshots/configureUI.png)

> sets the current value of a given option for an UI element with the given key to a given value. If no element with the given key can be found, an exception is thrown and the program aborted. Which options and option values are meaningful (and, thus, used by the UI), depends on the type of the given UI element

![ConfigurationOf](./Screenshots/ConfigurationOf.png)

> returns the current value of a given option for an UI element with the given key. If no element with the given key can be found, an exception is thrown and the program aborted. The requested option does not have to exist

![EnablingOf](./Screenshots/EnablingOf.png)

> returns `true` if an UI element with the given key is enabled or `false` otherwise. If no element with the given key can be found, an exception is thrown and the program aborted.

![enable](./Screenshots/enable.png)

> enables the UI element with the given key. If no element with the given key can be found, an exception is thrown and the program aborted (see [related example](#enable-and-disable))

![disable](./Screenshots/disable.png)

> disables the UI element with the given key. If no element with the given key can be found, an exception is thrown and the program aborted (see [related example](#enable-and-disable))

![isEnabled](./Screenshots/isEnabled.png)

> returns `true` if an UI element with the given key (exists and) is enabled. If no element with the given key can be found, an exception is thrown and the program aborted.

![clearChoicesOf](./Screenshots/clearChoicesOf.png)

> clears all currently defined choices of a radiobutton group or a drop-down element

![appendChoiceTo](./Screenshots/appendChoiceTo.png)

> appends the given text to the list of choices for a radiobutton group or a drop-down element

![clearConsole](./Screenshots/clearConsole.png)

> clears the built-in "Console" (see [related example](#console)).

![print](./Screenshots/print.png)

> appends the given string to the built-in "Console" (see [related example](#console))

![println](./Screenshots/println.png)

> appends the given string to the built-in "Console" and starts a new line (see [related example](#console))

![clearPendingUIEvents](./Screenshots/clearPendingUIEvents.png)

> removes all pending UI events from the internal queue. If there are no pending events, this statement is simply ignored

![wheneverUIEventOccurredWithin](./Screenshots/wheneverUIEventOccurredWithin.png)

> starts an event loop and runs the given statements whenever a new UI event was received. If the given timeout is `0` the loop is exited as soon as no more UI events are pending. If the given timeout is greater than `0` the loop is exited if no event was received within the given number of seconds. With a negative timeout, the loop waits indefinitely for the next UI event

![wheneverUIEventOccurred](./Screenshots/wheneverUIEventOccurred.png)

> starts an event loop and runs the given statements whenever a new UI event was received, waiting indefinitely for new events

![ButtonWasClicked](./Screenshots/ButtonWasClicked.png)

> returns `true` if the currently processed UI event is a click on a button with the given name - or `false` otherwise (see [related example](#button-clicks))

![InputWasChanged](./Screenshots/InputWasChanged.png)

> returns `true` if the currently processed UI event indicates that new input for the UI element with the given name was received - or `false` otherwise

![leaveUIEventLoop](./Screenshots/leaveUIEventLoop.png)

> leaves the current event loop

### AI Basics ###

The following blocks perform basic AI functions

![ChatCompletionForOptionPrefix](./Screenshots/ChatCompletionForWithOptionPrefix.png)
![ChatCompletionFor](./Screenshots/ChatCompletionFor.png)

> performs a chat completion for the given list of messages and returns the string created by the LLM. The message list must consist of an initial "system" message, a "user" message and (optionally) a sequence of "assistant" and "user" messages. If provided, any required options (such as `model`, `temperature`, `top_k` etc.) are taken from context items whose names start with the given option prefix. If such context items do not exist, are empty or the prefix is missing, any options are taken from context items whose names start with `default_`

![TextCompletionForWithOptionPrefix](./Screenshots/TextCompletionForWithOptionPrefix.png)
![TextCompletionFor](./Screenshots/TextCompletionFor.png)

> performs a text completion for the given prompt. The prompt is used to generate a "system" and a "user" message which are then used to generate a "chat completion". The "system" message is generated from the `SystemTemplate` context item, the "user" message from `UserTemplate`. If provided, any required options (such as `model`, `temperature`, `top_k` etc.) are taken from context items whose names start with the given option prefix. If such context items do not exist, are empty or the prefix is missing, any options are taken from context items whose names start with `default_`.  

### AI Mezzanines ###

The following blocks internally use AI requests themselves to perform some tasks which are often found in AI agents:

![SummaryOfText](./Screenshots/SummaryOfText.png)

> returns a summary of the given text. The block uses its own set of context items (prefixed with `Summarizer_`) to configure the inferencing parameters for text summarization - missing (or empty) items are taken from the default set

![TaskDecomposer](./Screenshots/TaskDecomposer.png)

> generates a sequence of steps that have to be worked through in order to achieve a given goal. A single "step" is an object with the following properties:
>
> * `Tool`: name of a selected tool (either `ResearchTool`, `ComputationTool` or `ResponseTool`)
> * `Objective`: a short statement of what the chosen tool should achieve
> * `Justification`: a brief explanation of why this tool and objective were chosen
>
> The result of this block is a list of such steps (see [related example](#steps-derived-from-a-given-objective))

![ResearchFor](./Screenshots/ResearchFor.png)

> uses the given "objective" to generate an adequate search phrase, search the internet, fetch all documents found by the search engine, extract any relevant information from these documents and produce a common result from all individual findings. Internally, this block uses the search phrase generator, information extractor and validator, solution merger and solution encoder described below.

![SearchGenerator](./Screenshots/SearchGenerator.png)

> generates a "phrase" which can be used to perform an internet search using a common search engine (or SearXNG) (see [AI Web Search](#ai-web-search) example)

![InformationExtractor](./Screenshots/InformationExtractor.png)

> a web search usually returns a list of URLs - one per document that seems relevant. This block now fetches one of theses documents from the given URL, "reads" it and extracts any information that seems relevant for the given objective (see [AI Web Search](#ai-web-search) example)

![InformationValidator](./Screenshots/InformationValidator.png)

> extracting information from a document may return nonsense. In order not to dilute the final result, this block checks if the given extract is actually relevant for the given objective or not. It returns `true` if it is or `false` otherwise (see [AI Web Search](#ai-web-search) example)

![SolutionMerger](./Screenshots/SolutionMerger.png)

> extracting information from several documents yields a list of separate extracts which may overlap in their contents. This block takes two such extracts and combines them into a single response relevant for a given objective (see [AI Web Search](#ai-web-search) example)

![SolutionEncoder](./Screenshots/SolutionEncoder.png)

> AI responses are often "noisy", i.e. they contain additional "decorative" words besides the actually requested information. This block therefore extracts the plain response and returns it as a list of facts (see example [AI Web Search with live Reporting](#ai-web-search-with-live-reporting))

![ComputationOf](./Screenshots/ComputationOf.png)

> generates a JavaScript function to achieve the given "objective", executes it and returns the result. This block internally uses the parameter list, function and argument generators described below.

![ParameterListGenerator](./Screenshots/ParameterListGenerator.png)

> uses the current "knowledge" (taken from the context item `Knowledge`) and generates a (possibly empty) list of parameter specifications for a Javascript function to achieve the given "objective")

![FunctionGenerator](./Screenshots/FunctionGenerator.png)

> uses the given parameter specification list and generates a JavaScript function to achieve the given "objective".

![ArgumentGenerator](./Screenshots/ArgumentGenerator.png)

> uses the current "knowledge" (taken from the context item `Knowledge`) and generates an argument value suitable for the given parameter specification.

![AnswerGenerator](./Screenshots/AnswerGenerator.png)

> uses the current "knowledge" (taken from the context item `Knowledge`) and generates a human-readable response to the given "task".

![KnowledgeGenerator](./Screenshots/KnowledgeGenerator.png)

> takes a given "fact", generates a concise description based on the given "objective" that was used to find or compute this data and appends it to the current "knowledge" of the running AI agent. The new "knowledge" will be writen to the context item `Knowledge` but not automatically preserved.

### AI Support ###

The following blocks have been made to support the creation of AI agents.

![ValueIsKnowledge](./Screenshots/ValueIsKnowledge.png)

> returns `true` if the given value represents valid agent "knowledge" - or `false` otherwise. Agent "knowledge" is a (possibly empty) list of JavaScript objects containing the following properties:
> 
> * `Description`: a concise description of what the actual `fact` represents
> * `Fact`: the actual knowledge as a JSON-encoded JavaScript value
>
> The `Description` will help the AI to find relevant facts for its task, while the `Fact` contains the actual data.

![ValueIsStep](./Screenshots/ValueIsStep.png)

> returns `true` if the given value represents a single working step for an AI agent - or `false` otherwise. A "working step" is a Javascript object containing the following properties:
> 
> * `Tool`: name of a selected tool (either `ResearchTool`, `ComputationTool` or `ResponseTool`)
> * `Objective`: a short statement of what the chosen tool should achieve
> * `Justification`: a brief explanation of why this tool and objective were chosen

![ValueIsStepList](./Screenshots/ValueIsStepList.png)

> returns `true` if the given value represents a sequence of working steps for an AI agent - or `false` otherwise.

![ValueIsParameter](./Screenshots/ValueIsParameter.png)

> returns `true` if the given value a single function parameter specification - or `false` otherwise. A "parameter specification" is a Javascript object containing the following properties:
>
> `Name`: the parameter name (a valid JavaScript identifier)
> `Description`: a short description of the parameter's purpose
>
> both settings can be used to create a JavaScript function and derive its argument values from the already given knowledge

![ValueIsParameterList](./Screenshots/ValueIsParameterList.png)

> returns `true` if the given value represents a list of function parameter specifications - or `false` otherwise.

![ValueIsWikipediaURL](./Screenshots/ValueIsWikipediaURL.png)

> returns `true` if the given value is a string containing a Wikipedia URL - or `false` otherwise

![ValueIsWikipediaPageName](./Screenshots/ValueIsWikipediaPageName.png)

> returns `true` if the given value is a string containing a Wikipedia page name - or `false` otherwise

![HTMLtoText](./Screenshots/HTMLtoText.png)

> converts the given HTML into formatted text

![JSONinText](./Screenshots/JSONinText.png)

> returns the first JSON object found in a given text - or `undefined` if no such JSON specification could be found (or the specification was incorrect)

![TextOfWikipediaArticle](./Screenshots/TextOfWikipediaArticle.png)

> fetches the (english) Wikipedia article with the given page name and returns its contents as plain text

![WebSearch](./Screenshots/WebSearch.png)

> searches the web for documents related to a given search phrase and returns a list with the URLs of the first found documents. If context item `SearXNGServer` contains a valid URL, the search request is sent to that server and only documents with a score greater than or equal to the threshold specified in context item `SearXNGScoreThreshold` (a number in the range 0...10 which defaults to 2) will be listed. Otherwise, a random public server will be looked up and used to perform the search. In both cases, up to 10 URLs will be returned, at most.

![WikipediaSearch](./Screenshots/WikipediaSearch.png)

> searches the (english) Wikipedia for articles related to a given search phrase and returns a list with the Wikipedia page names of the first found articles

### Miscellany ###

The following blocks do not fit into the categories shown before - may may still be helpful when creating agents:

![nop](./Screenshots/nop.png)

> this block has no specific functionality but serves as a visual separator between adjacent blocks only - this may help identifying related blocks

![throwError](./Screenshots/throwError.png)

> throws the given exception (which is then shown in an alert dialog) and aborts the running program (see related [example](#throw))

![wait](./Screenshots/wait.png)

> waits for a given number of seconds and continues (see [Console example](#console))

![alert](./Screenshots/alert.png)

> opens a browser "alert" pop-up dialog, displays the given message and continues as soon as the user has closed the dialog (see related [example](#alert-confirm-prompt))

![confirm](./Screenshots/confirm.png)

> opens a browser "confirmation" pop-up dialog, displays the given message and continues as soon as the user has responded with "ok" or "Cancel". If cancelled, the block returns `false`, otherwise it returns `true` (see related [example](#alert-confirm-prompt))

![prompt](./Screenshots/prompt.png)

> opens a browser "prompt" pop-up dialog, displays the given message and continues as soon as the user has entered a response. If cancelled, the block returns an empty string, otherwise it returns the entered string (see related [example](#alert-confirm-prompt))

![speak](./Screenshots/speak.png)

> uses text-to-speech to speak the given (english!) message (see related [example](#text-to-speech))

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

### Object Support ###

The following blocks help to create and manipulate objects

![createObject](./Screenshots/createObject.png)

> returns a newly created empty object (see related [example](#objects))

![PropertiesOfObject](./Screenshots/PropertiesOfObject.png)

> returns a (possibly empty) list with the keys of all own properties of a given object (see related [example](#objects))

![ObjectHasProperty](./Screenshots/ObjectHasProperty.png)

> returns `true` if the given object contains a proeprty with the given key - or `false` otherwise (see related [example](#objects))

![getObjectProperty](./Screenshots/getObjectProperty.png)

> returns the current value of the given object's property with the given key (see related [example](#objects))

![setObjectProperty](./Screenshots/setObjectProperty.png)

> sets the given object's property with the given key to a given value (see related [example](#objects))

![deleteObjectProperty](./Screenshots/deleteObjectProperty.png)

> deletes the given object's property with the given key (see related [example](#objects))

## Examples ##

Here are a few examples which you can upload into the Blockly workspace to get familiar with Blockly itself and the custom blocks specifically made for the "blockly-ai-playground". The linked Blockly workspace files should first be downloaded onto your computer and then uploaded into your Blockly workspace

### Hello, World ###

![Hello_World](./Examples/Hello_World.png)

> this is the typical "Hello, World" example (see [Blockly workspace file](./Examples/Hello_World.json))

### Alert, Confirm, Prompt ###

![Alert_Confirm_Prompt](./Examples/Alert_Confirm_Prompt.png)

> if you do not want to implement a "real" user interface (with an event loop), it may already be sufficient to use the browser's built-in pop-up dialogs `alert`, `confirm` and `prompt` - for simple use cases, at least. This example demonstrates how to use them (see [Blockly workspace file](./Examples/Alert_Confirm_Prompt.json))

### Console ###

![Console](./Examples/Console.png)

> this example demonstrates all Console functions (see [Blockly workspace file](./Examples/Console.json))

### Suspend, Resume, Abort ###

![Suspend_Resume_Abort](./Examples/Suspend_Resume_Abort.png)

> use this little Blockly program to get familiar with "Suspend", "Resume" and "Abort" (see [Blockly workspace file](./Examples/Suspend_Resume_Abort.json))

### throw ###

![throwError](./Examples/throwError.png)

> this example illustrates how to use the "throw" block (see [Blockly workspace file](./Examples/throwError.json)) - please note, that all blocks following a "throw" will not be evaluated as throwing an exception will terminate a Blockly program



### Text-to-Speech ###

![speak](./Examples/speak.png)

> this example demonstrates text-to-speech synthesis using the Browser's built-in WebSpeech API (see [Blockly workspace file](./Examples/speak.json))

### WebSpeech ###

![WebSpeech](./Examples/WebSpeech.png)

> this example illustrates how to use the Browser's built-in WebSpeech API (see [Blockly workspace file](./Examples/WebSpeech.json))



### Context ###

![Context](./Examples/Context.png)

> this example demonstrates all local context functions (see [Blockly workspace file](./Examples/Context.json))

### preserve and restore ###

![preserve_restore](./Examples/preserve_restore.png)

> this example demonstrates how to preserve and restore context items (see [Blockly workspace file](./Examples/preserve_restore.json))



### Textline Input ###

![TextlineInput](./Examples/TextlineInput.png)

> this example shows textline input elements in several variations (see [Blockly workspace file](./Examples/TextlineInput.json)). the other input elements work quite similarly

### SpeechInput ###

![SpeechInput](./Examples/SpeechInput.png)

> this example demonstrates speech recognition using the Browser's built-in WebSpeech API (see [Blockly workspace file](./Examples/SpeechInput.json))

### CheckboxElement ###

> t.b.w.

### Radiobutton Group ###

![RadiobuttonGroup](./Examples/RadiobuttonGroup.png)

> this example illustrates how to use a radiobutton group (see [Blockly workspace file](./Examples/RadiobuttonGroup.json))

### DropDown ###

> t.b.w.

### APIServerInputElement ###

> t.b.w.

### Output Elements ###

![OutputElements](./Examples/OutputElements.png)

> this example shows all output elements of the playground UI (see [Blockly workspace file](./Examples/OutputElements.json))

### Configuration Options ###

> t.b.w.

### enable and disable ###

![enable_disable](./Examples/enable_disable.png)

> this example demonstrates the effects of enabling or diabling either the whole UI or individual UI elements (see [Blockly workspace file](./Examples/enable_disable.json))

### Event Loop ###

> t.b.w.

### Button Clicks ###

![ButtonWasClicked](./Examples/ButtonWasClicked.png)

> this example demonstrates how to react on a button click (see [Blockly workspace file](./Examples/ButtonWasClicked.json))

### Objects ###

![Objects](./Examples/Objects.png)

> this example demonstrates how to work with objects (see [Blockly workspace file](./Examples/Objects.json))

### Web Search ###

> t.b.w.

### Web Document Retrieval ###

> t.b.w.

### Wikipedia Search ###

> t.b.w.

### Wikipedia Article Retrieval ###

> t.b.w.


## AI Examples ##

The following examples actually include AI-related blocks. As before, the Blockly workspace files should first be downloaded onto your computer and then uploaded into your Blockly workspace

### Basic Settings ###

![basicSettings_I](./Examples/basicSettings_I.png)![basicSettings_II](./Examples/basicSettings_II.png)

> use this example to enter your basic AI-related settings - they will be stored in the browser's storage and may then be used by other programs without having to re-enter them over and over again (see [Blockly workspace file](./Examples/basicSettings.json) - download it onto your computer and then upload it into the Blockly workspace)

![basicSettings UI](./Examples/basicSettings-UI.png)

> as a hint, here are the settings used by the author himself

### Text Completion (Proof-of-Concept) ###

![PoC](./Examples/TextCompletion.png)

> this is the "proof-of-concept" mentioned above - play around as you like! (see [Blockly workspace file](./Examples/TextCompletion.json) - download it onto your computer and then upload it into the Blockly workspace)

![PoC-UI](./Examples/TextCompletion-UI.png)

> this is what you may get as the result

### Chat Completion ###

![PoC](./Examples/ChatCompletion.png)

> here is an example for a simple ChatCompletion (see [Blockly workspace file](./Examples/ChatCompletion.json) - download it onto your computer and then upload it into the Blockly workspace)

![PoC-UI](./Examples/ChatCompletion-UI.png)

> this is what you the result may look like

### Text Summary ###

![TextSummarizer](./Examples/TextSummarizer.png)

> this example summarizes a given text (see [Blockly workspace file](./Examples/TextSummarizer.json) - download it onto your computer and then upload it into the Blockly workspace)

![TextSummarizer-UI](./Examples/TextSummarizer-UI.png)

> this is the author's run to let the AI summarize the beginnings of "Alice in Wonderland" - your mileage may vary, of course

### AI Research Tool ###

![AIResearchTool](./Examples/AIResearchTool.png)

> this is a demonstraton of the built-in "ResearchTool" for AI Agents: enter what you are looking for and let SearXNG and the AI look for relevant documents, read them for you and present a summary of what the system learned (see [Blockly workspace file](./Examples/AIResearchTool.json) - download it onto your computer and then upload it into the Blockly workspace)

![AIResearchTool-UI](./Examples/AIResearchTool-UI.png)

> it's definitely not easy to find a good answer for the question "to which programming languages has Joseph Weizenbaum's famous Eliza program been ported?" (even if you try yourself) - here is what the author's attempt produced as output: definitely incomplete, but not bad for just a few seconds of work...

### AI Web Search ###

![AIWebSearch_I](./Examples/AIWebSearch_I.png)
![AIWebSearch_II](./Examples/AIWebSearch_II.png)

> you don't have to use the built-in "ResearchTool", you may also implement a similar functionality yourself: this example illustrates how to use several AI Mezzanines to implement an AI-assisted web search (see [Blockly workspace file](./Examples/AIWebSearch.json) - download it onto your computer and then upload it into the Blockly workspace)
>
> By the way: the objective was "to which programming languages has Joseph Weizenbaum's famous "Eliza" program be ported?"

![AIWebSearch-UI](./Examples/AIWebSearch-UI.png)

> this is what the example may produce as output

### AI Search Phrase Generation ###

![SearchPhraseGenerator](./Examples/SearchPhraseGenerator.png)

> if you want to conduct a web research for a given topic, you may have to generate a search phrase first - this example does that for you (see [Blockly workspace file](./Examples/SearchPhraseGenerator.json) - download it onto your computer and then upload it into the Blockly workspace)

![SearchPhraseGenerator-UI](./Examples/SearchPhraseGenerator-UI.png)

> and here you see what a search phrase may look like

### AI Information Extraction ###

![InformationExtractor](./Examples/InformationExtractor.png)

> if you have a text that contains information you need for a given task, you want the AI to read that text and extract what is relevant - here is an example of how to do that (see [Blockly workspace file](./Examples/InformationExtractor.json) - download it onto your computer and then upload it into the Blockly workspace)

![InformationExtractor-UI](./Examples/InformationExtractor-UI.png)

> here you have an example for a useful information extraction 

### AI Information Validation ###

> letting the AI extract relevant information from a given text may sound nice, but in fact, the AI often produces complete nonsens - here is an example how you can let the AI validate the actual relevance of its output itself (see [Blockly workspace file](./Examples/InformationValidator.json) - download it onto your computer and then upload it into the Blockly workspace)

> t.b.w.

### AI Computation Tool ###

![AIComputationTool](./Examples/AIComputationTool.png)

> the "Computation Tool" takes an "Objective" and uses the already existing "Knowledge" to create and execute a JavaScript function that tries to compute the requested result

![AIComputationTool-UI](./Examples/AIComputationTool-UI.png)

> this is what you may get after running the above example

### AI Parameter List Generation ###

> letting the AI generate and execute a Javascript function to achieve a given objective first requires a well-defined list of parameters so that the function knows what data will be passed as its arguments and the AI knows what kind of argument list to create. Here is an example how you can generate such a parameter list (see [Blockly workspace file](./Examples/ParameterListGenerator.json) - download it onto your computer and then upload it into the Blockly workspace)

> t.b.w.

### AI Code Generation and Execution ###

> this examples shows how to let the AI generate a JavaScript function to compute the given objective based on a list of parameters (see [Blockly workspace file](./Examples/FunctionGenerator.json) - download it onto your computer and then upload it into the Blockly workspace)

> t.b.w.

### AI Task Decomposer (without existing knowledge) ###

> at the core of an AI agent there is a component which breaks down a given task into smaller steps which may then be worked through. This example demonstrates how the AI does so from scratch (see [Blockly workspace file](./Examples/TaskDecomposer_I.json) - download it onto your computer and then upload it into the Blockly workspace)

> t.b.w.

### AI Task Decomposer (using already existing knowledge) ###

> often, an AI agent does not have to start its work from scratch but may use already existing "knowledge" - here is an example for generating the remaining steps to achieve a given objective in such a situation (see [Blockly workspace file](./Examples/TaskDecomposer_II.json) - download it onto your computer and then upload it into the Blockly workspace)

> t.b.w.

### AI Knowledge Generator ###

> both the "ResearchTool" and the "ComputationTool" produce new "facts" which have to be added to existing knowledge for an AI agent to continue its work and (in the end) produce a response. This example shows how that can be done (see [Blockly workspace file](./Examples/KnowledgeGenerator.json) - download it onto your computer and then upload it into the Blockly workspace)

> t.b.w.

### AI Answer Generator ###

> every run of an AI agent should finally produce a response - this example demonstrates how to do so (see [Blockly workspace file](./Examples/AnswerGenerator.json) - download it onto your computer and then upload it into the Blockly workspace)

> t.b.w.

### AI Agent ###

![AI-Agent_I](./Examples/AI-Agent_I.png)
![AI-Agent_II](./Examples/AI-Agent_II.png)

> this example contains a full-blown AI agent (it's a bit like your own, personal "Copilot"): give it a "task" and watch how it decomposes it into smaller steps it is then working through. The agent has two "tools" at hand: a "ResearchTool" that can conduct web researches (like the [AI Web Search](#ai-web-search) from above) and a "ComputationTool" which creates and runs a JavaScript function that is used whenever some information has to be computed rather than looked up in the Internet. The outcome of each step is added to the agent's "knowledge" and stored in the browser - this gives the agent the possibility to skip over already completed steps when it was aborted and restarted later (provided that the "task" was not changed in between)

### Steps derived from a given Objective ###

![StepsDerivedFromText](./Examples/StepsDerivedFromText.png)

> this example demonstrates the decomposition of a given objective into smaller steps (see [Blockly workspace file](./Examples/StepsDerivedFromText.json) - download it onto your computer and then upload it into the Blockly workspace)

![StepsDerivedFromText-UI](./Examples/StepsDerivedFromText-UI.png)

> this is what you may get when asking for the steps to solve the problem "what is the total number of people living in all german cities whose names end with "dorf"?" (an objective which is so weird that you presumably won't find the solution by a simple web search)

## License ##

[MIT License](LICENSE.md)
