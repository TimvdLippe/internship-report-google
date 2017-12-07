# Internship report Tim van der Lippe

In the summer of 2017, I did an internship at the [Polymer](https://www.polymer-project.org/) team in the San Francisco office of Google.
This internship included training by top engineers about the inner-workings of Google as a company, how to use the tooling for the daily developer workflow as well as a real-world project.
The real-world project concerned the load time of large web applications, focused on one of the biggest users of Polymer: Youtube.

This report contains an overall impression of the working environment at Google in comparison to my university, a description of the full internship, the technical aspects of the task that was given as well as an insight in the way Google can do software engineering on a large scale.

## Working at Google

During the internship I experienced a different working environment in comparison to the environment at my university, [Delft University of Technology](https://www.tudelft.nl/).
There is a stark difference between prioritization and assignment of tasks between industry and university life.
In the 12 weeks, I was tasked to answer a (seemingly) simple question.
There was no pre-specified set of sub-tasks required to be able to answer this question, this was my own responsibility.
Of course I had (almost daily) meetings with my host and second reviewer, as well as other team members, who I could discuss approaches and problems with.
This ad-hoc approach allowed me to work on problems and discuss blocking issues right as I encountered them (or after an hour being stuck on the same issue).

The first 2 weeks consisted of training by top Google engineers in Mountain View, which explained how Google operates and introduces new hires into the Google workflow.
I was in a special position, as most of the specific workflow was not required knowledge for my internship.
As the Polymer team is primarily open source, my work was all on GitHub, which I was very familiar with as a result of my work during my courses.
Nonetheless, whenever terms were used in discussions with Google engineers, I was able to follow the conversation and understand the concepts they were talking about.
Besides that, the knowledge I obtained, during courses such as [Software Quality and Testing](http://studiegids.tudelft.nl/a101_displayCourse.do?course_id=34556&SIS_SwitchLang=en) and [Software Engineering Methods](http://studiegids.tudelft.nl/a101_displayCourse.do?course_id=43888&SIS_SwitchLang=en), was crucial to be able to have efficient and constructive discussions with my host and second reviewer.

### Testing at Google

The emphasis on testing is very prevalent at Google.
Besides work on my project tool, all of my contributions to (open source) projects required the existence of tests that either tested the new functionality or were regression tests to make sure bugs were fixed.
Full Test-Driven-Development (TTD) was not something I had to practice, although I mostly used TDD for debugging bug reports and verify that the issue was resolved.

Google internally runs most of the tests on every change.
Google uses a [Test Automation Platform (TAP)](https://research.google.com/pubs/pub45861.html) to test changes made by a developer.
Since there is an average of 1 commit per second in the [single repository](https://research.google.com/pubs/pub45424.html), running all tests on every single change list is infeasible and computationally impossible.
Instead, tests are only run in specific intervals focusing on running frequently-breaking tests.
Whenever tests broke, engineers had to do a deep-dive and triage the issue.
As engineering time is very expensive, Google put(s) a lot of effort into optimizing the triaging workflow.

During my internship, I experienced the debugging experience second-handed, when a team member was triaging a TAP failure.
The test that broke was in a project not owned by the Polymer team.
However, as the change list of the team member broke the test, it was their responsibility to figure out the root issue.
If the root issue cannot be found, instead of waiting and continuing the search, the change is rolled back to unblock all other engineers from working.
Rolling back changes is crucial, as Google operates in this single repository.
(An example of the importance of rolling back changes was [in response to company-wide outages](https://books.google.nl/books?id=tYrPCwAAQBAJ&lpg=PT227&ots=ixoA81UW7p&dq=google%20rollback%20change%20internal&hl=nl&pg=PT227#v=onepage&q=google%20rollback%20change%20internal&f=false)).
In my specific example, the engineer and I discussed and reasoned about the test failure.
Even though we had no experience with the test, nor the complete system, the team member and I were still able to deduce why the test failed.
Nonetheless, we were unable to fix the issue immediately, so we rolled back the change.

### Work-life balance

On a less technical note, my host and I also worked on my work-life balance.
During my study, I was used to working 7 days a week.
On weekdays, I would  start at 10 AM and work till 6 PM, eat dinner and sometimes work more between 8 PM and 10PM/1AM.
My work hours largely depended on the size of my assignments and sometimes because I was excited working on a particular assignment.
One occurrence I recall was working on the course [Concepts of Programming Languages](http://studiegids.tudelft.nl/a101_displayCourse.do?course_id=43899&SIS_SwitchLang=en) till 1 AM in the morning, as I suddenly had inspiration and was able to solve the assignment (even though the deadline was still days away).

Being used to these working hours, at the start of my internship I had trouble having a healthy work-life balance.
In the first couple of weeks, I would work hours similar to what I was used to during the university.
However, most of the Google engineers left at 6 PM, while a couple of team members and I would stick around.
We had a smallish group of engineers eating dinner every day in the office.
After dinner, we would go back to continue working in the office.

Roughly in the middle of my internship, my host started a discussion about my work-life balance.
Implicitly, it was impacting my work performance and I was working less efficiently as I could, but I was not aware of it being that impactful.
This discussion was tough and trying to change my working hours was hard, but in the last weeks of my internship I did change my day.
Instead of returning to the office after dinner, I would join colleagues in playing games (pool, pinball, table tennis).
Even though I reduced the total amount of working hours per day, I was more productive and able to resolve problems faster.
Learning to manage my work-life balance was very valuable and I think that without working in industry and having peers discussing these problems, it is hard to make sure you are working in a healthy manner.

### Conclusion

All in all, working at Google is not extremely different compared to university life.
However, priorities and aspects such as a work-life balance are very much different in industry compared to being a student.
The knowledge I obtained from my university courses were sufficient to be able to have thoughtful conversations with my colleagues.
However, practical experience outside course assignments and exams is required to be able to effectively write industry code.
Luckily I could obtain experience with my open source contributions which I did in parallel to my study.
(The open source contributions to Polymer eventually led the Polymer team to reach out to me for this internship)

## Description of real-world project

Aside from obtaining experience from working at Google, the most important part of the internship was the real-world project.
Load time of applications is of great concern for Youtube as well as various other big users of [Polymer](https://www.polymer-project.org/).
As such, Youtube requested the Polymer team for improvements to their load performance.
Earlier examples of improved load performance was the introduction of [`lazyRegister`](https://github.com/Polymer/polymer/releases/tag/v1.4.0).
`lazyRegister` specifically aimed to reduce the amount of registration and setup work Polymer did when registering elements.
As Youtube is a big application, it builds and uses a lot of [custom elements](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Custom_Elements) on every page.
However, not all elements are crucial to be fully available on first load.
Examples include elements that are in hidden visual components (drop down menus, dialogs, etc...) or are used in only a subset of the various pages.
Late registration was introduced to only do the necessary registration work once an element was instantiated and thus actually used.

The introduction of the `lazyRegister` shows that certain features of Polymer are targeted to specific use-cases of Polymer.
While it is very likely that every application benefits of applying late-registration, in some cases it might not be a big performance improvement.

In a similar fashion, the Polymer team identified computational work on load time that could be prevented.
This work concerned the metaprogramming of Polymer: in-memory representations of the definitions and thus behavior of custom elements.
On load, Polymer parses the definitions of custom elements, performs the transformation to the in-memory representation and uses this representation in all further interaction with the element.

The conversion to the in-memory representation is CPU intensive, with a primary factor of traversal of the templates of custom elements.
Templates use the [`<template>`](https://developer.mozilla.org/nl/docs/Web/HTML/Element/template)  tag to define the structural setup of the custom element.
Figure [1](#fig-example-template) shows an example of such an element.
Templates can contain other custom elements, such as `<custom-header>`, as well as bindings to properties, attributes and textContent.

<div id="fig-example-template"></div>

```html
<template>
   <custom-header title="Blogpost: [[title]]"></custom-header>
   <main>
       <h1>[[title]]</h1>
       <section>[[content]]</section>
       <custom-input value="{{value}}"></custom-input>
       <span>You typed "[[value]]"!</span>
   </main>
   <custom-footer></custom-footer>
</template>
```

<div>
Figure 1: Example of a template definition used in a Polymer custom element
</div>

### Polymer element definition

The template is captured inside a [`<dom-module>`](https://www.polymer-project.org/2.0/docs/api/elements/Polymer.DomModule) with a specific ID that corresponds to the Polymer element definition, as expressed in JavaScript.
A full example of a Polymer element definition with its corresponding template is shown in Figure [2](#fig-polymer-element-definition).

<div id="fig-polymer-element-definition"></div>

```html
<dom-module id="my-blogpost">
   <template>
       <custom-header>
       ...
   </template>
   <script>
       class MyBlogPost extends Polymer.Element {
           static get is() { return 'my-blogpost'; }

           static get properties() {
               return {
                   title: String,
                   content: {
                       type: String,
                       value: 'No content available'
                   }
               }
           }
       }
       customElements.define(MyBlogPost.is, MyBlogPost);
   </script>
</dom-module>
```

<div>
Figure 2: Example of a definition of a Polymer custom element
</div>

A custom element definition (invoked via [`customElements.define(name, constructor, options)`](https://developer.mozilla.org/en-US/docs/Web/API/CustomElementRegistry/define)) has two components: the name of the custom element and the class definition of its behavior.
In the example, the name of the custom element is `my-blostpost`, which corresponds to the `id` of the `<dom-module>`.
The encapsulated template inside the `<dom-module`>, of which Figure [1](#fig-example-template) is a more detailed example, is linked to the custom element definition.

### Bindings

On load time, Polymer traverses the template and looks for the bindings.
Bindings are denoted as `[[]]` and `{{}}`.
Square brackets indicate a one-way binding (parent to child) whereas angle brackets indicate a two-way binding (both parent to child as well as child to parent).
Between the brackets, several types of expressions can exist.
Most commonly, bindings contain a reference to a property as described in the custom element class definition.
In the example above, `<my-blogpost>` defines two properties: `title` and `content`.
While `content` has a default value, `title` has not.

Provided the usage as described in Figure [3](#fig-my-blogpost-simple-usage), the first blogpost will only define a `title` whereas the second blogpost provides content and thus overrides the default `content`.

<div id="fig-my-blogpost-simple-usage"></div>

```html
<my-blogpost title="Simple article"></my-blogpost>
<my-blogpost title="Article with content" content="Interesting content here"><my-blogpost>
```

<div style="text-align: center;">Figure 3: Example usage of the &lt;my-blogpost> element.</div>

<br>

The above figures show the interaction between the custom element definition, it's corresponding template and the various possibilities for instances of the custom element.
What the figures do not show, is the machinery required to obtain a working custom element.
This is where Polymer comes in.
In Figure [2](#fig-polymer-element-definition), the JavaScript class definition extends [`Polymer.Element`](https://www.polymer-project.org/2.0/docs/api/elements/Polymer.Element) which contains the logic that ensures that properties and bindings are updated whenever the user of the custom element updates the properties.

#### Binding update workflow

To illustrate how Polymer updates the bindings and properties, we will consider an example of an update workflow.
Given the first usage of `<my-blogpost>` in Figure [3](#fig-my-blogpost-simple-usage), the update workflow is triggered once either `title` or `content` is updated.
In this example, the `content` property is updated to `"This is some sample content"`.

Whenever a property is updated, a setter as defined by Polymer is triggered.
This setter performs a dirty-check (to prevent needless updates of properties) and updates an internal storage called `__data`.
In Polymer 2, the property is also added to a bag of changed properties.
In the event of updating a property twice in the same cycle, the bag ensures that effects are only run once.
After each update cycle, Polymer iterates through the bag of changed properties and triggers all corresponding effects.
While there is a wide variety of effects, one of the types of effects is updating the bindings.

Based on the bindings as defined in the template, all bindings that concern a changed property are updated to its correct values.
For example, given the binding `[[content]]`, whenever `content` is changed, the value of this binding is updated to the most recent value.

## Project description

Precisely the interaction between properties and which bindings should be updated is stored in the in-memory representation, derived from the template.
This in-memory representation contains data such as the type of binding, what its dependencies are (bindings can have multiple properties in it) and which node originally contained the binding.

The so-called binding metadata remains largely the same in between page loads.
As such, every time a user opens the page, the binding metadata has to be calculated.

The internship project addressed the question: "Is it beneficial to pre-compute and send the metadata to the user?".
This question can be divided into three parts:
1. How to send the metadata to the user?
1. Given the template definitions, how should the metadata be pre-computed?
1. Provided the technical feasibility, does the load time improve when applying these measures?

In this report, each question is addressed separately.

### How to send the metadata to the user?

The in-memory representation of the metadata is split up per effect type.
Moreover, the binding metadata is written to the `__templateInfo` field of the `<template>` element.
This JavaScript object contains a list of node metadata, including data to retrieve back the node, bindings on this node and potentially recursively a list of children metadata.
Binding metadata can be serialized using [`JSON.stringify()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify), which results in a String representing the object.
This String can be inserted into the code which is sent to the user.
Since the String represents the serialized form of an object, the browser will construct the object while parsing the String.

To be able to retrieve the binding metadata, while registering a custom element, the object must be referenced in a unique way.
A solution to this problem is creating a global map of custom element names to the binding metadata.
Thus, when registering the custom element, a simple lookup in this map with the current custom element name results in the binding metadata as parsed by the browser.

One issue with this approach is that function closures are not properly serialized by `JSON.stringify`.
As such, closures must be transformed into a reference to a closure before the browser parses the JavaScript object.

### How should the metadata be pre-computed?

There are several options to pre-computing the metadata and every option has downsides.

#### Compute and extract

A first solution would be to open the webpage in a browser, let Polymer compute all necessary bindings and then extract the metadata by iterating through all defined custom elements.
This solution worked well for addressing the third question as it does not require a full-blown tool to investigate the performance impact, but lacks correctness.
For example, every custom element that is unused on first load is disregarded in the extraction process.
This means that whenever a custom element is not yet used on the first page the user opens, its metadata will not be precomputed.

An advantage to this approach is that it can deal with user-defined effects.
Users of Polymer can define custom property effects and bindings and plug this into the metadata system.
Since computing the metadata at load time includes the user-defined effects, this approach is more flexible.

##### Compute per element

To counteract potential lazy-loading, instead of loading the webpage as a whole, the computation can be performed on a single element.
In this case, each element is serialized separately in the browser and the metadata is computed separately as well.

#### Re-implement transformation in build tool

Pre-computing the metadata is performed in the build tool.
As such, the environment of the pre-computation is different than the browser environment.
All Polymer tools are targeting the Node environment.
Since the Polymer library depends on browser APIs, which do not or partially exist in the Node environment, the transformation as-is could be reimplemented to work with Node.

Re-implementation introduces issues such as maintainability, where every change in Polymer must be reflected in the build tool.
Moreover, if a new feature is introduced, the build tool must be updated at the same time, otherwise the build tool is temporarily incompatible with Polymer.

#### Integrate Polymer into the build tool

Based on the previous solution, an option could be to integrate Polymer into the Node environment.
To achieve this, all functionality concerning the metadata must be able to run outside of a browser environment.
Moreover, the functionality should be consumable by the existing Node tooling.

In Polymer 2, this would not be possible as the full implementation of Polymer is written in HTML files and thus depend on the browser to be parsed and executed.
Coincidently, in the middle of the internship, [Polymer 3 was announced](https://www.polymer-project.org/blog/2017-08-22-npm-modules.html) where the full implementation is instead built in JavaScript files.
Instead of [HTML imports](https://developer.mozilla.org/en-US/docs/Web/Web_Components/HTML_Imports) to define dependencies/imports, the equivalent JavaScript exports and imports as [ES modules](https://jakearchibald.com/2017/es-modules-in-browsers/) are used.
Integration of Polymer 3 JavaScript definitions of the metadata transformation is possible if the transformation has no dependency on any browser API.
The transformation must thus be pure JavaScript which must run in both the browser as in Node.

A disadvantage to this approach is that there is no existing knowledge in the team and the feasibility of the integration is unknown.
There might be unforeseen limitations that prevent a deep integration for the library and the build tools.

## Initial performance tests
To answer the third question (evaluate the feasibility and usefulness of pre-building the effects and binding metadata in Polymer applications), several performance experiments were performed.

### Definition of timings
In this document, the reported timings concern different stages of the file loading process as well as the property metadata parsing and computation time.
The timeline in Figure [4](#fig-file-timings) shows the different timings that are used in this document and their inner relation.
*Note: the sizes of the timings are not representative for real-world performance measurements.*

<div id="fig-file-timings"></div>

![image](https://user-images.githubusercontent.com/5948271/31383384-25c8e43a-adbb-11e7-8ef5-f92b705259f2.png)

<div>
Figure 4: Timeline with relative position of timings used in this report
</div>

### Types of pre-building
There are multiple optimizations that can be performed on build time.
First of all, the bindings as defined in the templates of Polymer elements can be extracted to the in-memory representation of Polymer.
This process starts with [`_parseTemplate`](https://github.com/Polymer/polymer/blob/ca1ce19682b0003359090491d7e81a58d26b9a4a/lib/mixins/template-stamp.html#L198).
As such, the bindings are stripped from the template and the equivalent JSON representation is generated.

#### Before
```html
<template>
   <custom-element
       property="[[value]]"
   ></custom-element>
   <span>[[textBinding]]</span>
   <paper-input
       value="{{notifying}}"
   ></paper-input>
</template>
```

#### After
```html
<template>
   <custom-element
   ></custom-element>
   <span> </span>
   <paper-input
   ></paper-input>
</template>
```

In a similar fashion, the properties of an element are transformed into in-memory configuration by [`finalizeProperties`](https://github.com/Polymer/polymer/blob/ca1ce19682b0003359090491d7e81a58d26b9a4a/lib/mixins/element-mixin.html#L292).
It retrieves the [`properties`](https://www.polymer-project.org/2.0/docs/devguide/properties) object from the element and finds the corresponding run-time functions to process the effect whenever the property changes.

Lastly, all defined properties trigger [`Object.defineProperty`](https://github.com/Polymer/polymer/blob/ca1ce19682b0003359090491d7e81a58d26b9a4a/lib/mixins/property-accessors.html#L419-L430).
This call can be prevented by directly inlining the accessors for the property:

#### Before
```js
properties: {
   foo: {
       type: String,
       value: 'bar'
   }
}
```

#### After
```js
get foo() {
   return this.__data[property];
}
/** @this {PropertyAccessors} */
set foo(value) {
   this._setProperty(property, value);
}
```

### Results on [Youtube](https://www.youtube.com)
Calling `finalize` and `finalizeTemplate` (to create metadata from the properties and template respectively) takes 132ms on desktop.
Removing this cost by directly assigning the expected output instead of computing results in 44ms (33% of the original).
This test only takes into account CPU time spent on the computation.
The next test included parsing time of the metadata as well Polymer element definitions.
The baseline of the original increases to 165ms, whereas parsing + executing the bindings is about 99ms and thus about half of the original.

While these results were on a desktop, several tests were also run on a mobile device (Pixel 1).
The baseline on mobile phone for parsing + executing is 507ms. With the effect metadata included, the total time decreases to 222ms (44% of the original).

| Platform (parsing + execution) | Before | After | % of original |
|---|---|---|---|
| Desktop | 165ms | 99ms | 60% |
| Mobile | 507ms | 222ms | 44% |

### Results on [summit website](https://summit.polymer-project.org/)
The parsing + executing bindings tests were replicated on the summit website, as it was significantly smaller than Youtube. On desktop, the results are 5ms and 2ms respectively. On mobile, the difference is 27ms to 9ms.

| Platform (parsing + execution) | Before | After | % of original |
|---|---|---|---|
| Desktop | 5ms | 2ms | 40% |
| Mobile | 27ms | 9ms | 33% |

### Network time metadata binding of [Youtube](https://www.youtube.com)
While CPU time is reduced, the gain is negated by the increased network time for serving the extra metadata in the bundle.
Exporting all metadata on Youtube generates 880KB of metadata resulting in 47KB gzipped.
Applying several optimizations (see appendix for more information) and changes to the Polymer core library, the bundle could be reduced to 364KB.
Performance tests on desktop showed a marginal difference in network time.
On mobile with fast wifi, the load time of the file increases from 159ms to 190ms.
Throttling to fast 3G results in 4,73s and 4,91s respectively.
Slow 3G results in 16,96s and 17,49s.


| Network condition | Load file before | Load file after | % of original |
|---|---|---|---|
| Non-throttled | 159ms | 190ms | 119% |
| Fast 3G | 4730ms | 4910ms | 104% |
| Slow 3G | 16960ms | 17490ms | 103% |

Deducting network loss from the CPU gain results in a gain on mobile of 359ms on non-throttled wifi. Fast 3G has a gain of 193ms and slow 3G -304ms (e.g. a decrease in performance).

| Network condition | Relative gain |
|---|---|
| Non-throttled | 359ms |
| Fast 3G | 193ms |
| Slow 3G | -304ms |

### Polymer [material design element demos playground](https://ebidel.github.io/material-playground/)
Lastly, end-to-end tests were performed on the material-playground.
Measuring full-load of the page, 1000 runs result in 383ms originally and 350ms on desktop.
On mobile with non-throttled wifi, the difference is 1217ms originally to 1215ms.
This indicates that the gain of CPU time is completely negated by the loss of network time.
As described in the Possible improvements section the removal of property definitions and template bindings can improve the overall gain.

| Platform (end-to-end) | Before | After | % of original |
|---|---|---|---|
| Desktop | 383ms | 350ms | 91% |
| Mobile | 1217ms | 1215ms | 100% |

### Possible improvements
#### Removal of property definitions and template bindings
These results are slightly worse than the tool could achieve, as all templates and property definitions are not stripped from the Polymer element definitions.
This means that the increase in network time can be reduced by the removal of unnecessary metadata.
The impact of this improvement is unknown, but significant.

#### Metadata optimizations
There are several other metadata optimizations that can be applied.
Several options and examples are listed in the Appendix [metadata optimizations](#appendix-metadata-optimizations).

# Implementation of the tool
Based on the initial performance experiments and results, we determined there was potential benefit to pre-built Polymer metadata.
As such, the second half of my internship I built the tool that could apply this transformation.

## High-level implementation
The implementation of the tool is based on existing tooling developed by the Polymer team.
This solution proved to be the most feasible, as the existing tooling provided an existing framework to process and modify files.
Implementing a custom version of processing files would allow for more granularity, but requires new implementation of extracting AST’s of the HTML and JS parts and writing the modified AST’s to the new location was too large for the scope of the project.
The compatibility of the tool is therefore strictly limited to the compatibility of the existing tooling.

The existing Polymer tooling provided several hooks:
 * [Polymer-build](https://github.com/polymer/polymer-build) provided functionality to [process Node streams](https://github.com/Polymer/polymer-build/blob/eab4fd0aa43c0bc94c41eee65a5ddf5d516953d3/src/streams.ts) and a [FileMapUrlLoader](https://github.com/Polymer/polymer-build/blob/020fc23ff4662bb8b7ca384ae0b12c4de231a276/src/file-map-url-loader.ts) that implements loading and storing files in the stream.
 * [Polymer-analyzer](https://github.com/polymer/polymer-analyzer) implements analysis of file streams as well as [PolymerElement](https://github.com/Polymer/polymer-analyzer/blob/0bef8a7103d9296c4a179cfb9b2105779ef3ac53/src/polymer/polymer-element.ts) which contains metadata of its accompanying dom-module, JS ASTNode and tagName.

## Polymer core databinding updates
The tool was heavily relying on the size of the serialized format of the metadata.
As such, any “smart” optimizations on using the metadata which result in a smaller serialized form were crucial to obtain a performance benefit.
However, the metadata format was documented and treated as public API.
As such, any modifications or omissions of data in the metadata was considered a breaking change.
This made updating the logic to be able to handle the minimalistic output of the tool a lot harder.
In a future major version of Polymer, these modifications can be safely introduced, likely affecting only a very small subset of Polymer users.
This also has the result of less memory usage and less CPU time calculating all the metadata upfront.
For now, [a special version of Polymer](https://github.com/Polymer/polymer/pull/4782) is required to be able to parse the minimized serialized output.

## Tool workflow
The modification process is implemented as follows:
1. Read in all files.
1. Analyze the files with polymer-analyzer
1. Based on the analysis, obtain DFS traversal of HTML imports
    1. All files that were in the stream but not in the traversal, yield back in the stream
1. Launch Chrome Headless
1. For all documents of the DFS traversal:
    1. Execute all scripts in the document
        1. For all defined elements in the document:
        1. Define dom-module in the browser
        1. Obtain metadata (bindings, property-effects) from browser
        1. Write binding metadata in front of JS ASTNode of element
    1. Serialize all AST’s in the document back into a file
1. Yield potentially modified content from the file back in the stream

## Chrome Headless
The initial implementation of the tool did not make use of Chrome Headless, but instead used the output of Polymer-analyzer directly.
However, the output of Polymer-analyzer was not 100% correct, as [property metadata was sometimes incorrect](https://github.com/Polymer/polymer-analyzer/pull/719), [properties types were incorrectly determined](https://github.com/Polymer/polymer-analyzer/pull/725), and [the parser used by polymer-analyzer corrupts JavaScript comments](https://github.com/Polymer/polymer-analyzer/pull/722).
Since the tool is required to pre-built the metadata, omission or incorrectness in the metadata is not allowed as it will break the website after using the tool.
Therefore, we decided to switch from Polymer-analyzer to run the actual code in Chrome Headless.
Running the code means: 1. Evaluate scripts directly in the console using Page.evaluate 2. Serialize HTML content and append it to the body, inside a script as well.
As such, while we initially did not choose for the first option as described in [How should the metadata be pre-computed?](#how-should-the-metadata-be-pre-computed-), this requirement changed our choice from option 3 to 1.

Another benefit of this approach is that by running the actual user code, the tool is able to handle custom user overrides of template parsing APIs such as [`_parseBinding`](https://www.polymer-project.org/2.0/docs/api/elements/Polymer.Element#method-_parseBindings).
If the Polymer-analyzer would be used, the static analysis tool will very likely not be able to determine what the final output of parsing the template is, whereas running the code will guarantee this.

A downside to this approach is that the user code might be relying on external factors such as additional fetch requests, localStorage, etc…
This makes the tool more dangerous than a static analysis approach, although during testing no obvious incompatibilities were determined.
The tool can be improved by sandboxing various potentially dangerous API’s to prevent unwanted side-effects.

## Results
Based on the initial results of the performance tests, there was a measurable improvement in pre-building the metadata by skipping costly DOM-traversal.
However, the initial results lacked definitive proof of end-to-end performance tests, as the approach was not scalable to multiple projects.

After building the tool, we were able to obtain more definitive data on load-time performance and different aspects of the load process.
This experiment was performed on the material playground.
The provided data definitively proved that pre-building binding metadata saved 14ms on desktop and 39ms on mobile for the material playground, which had a load time of respectively 341ms and 874ms with the tool applied.

| Platform (parsing + execution) | Original bindings | Pre-built bindings | Absolute gain |
|---|---|---|---|
| Desktop | 51ms | 37ms | 14ms |
| Mobile | 142ms | 103ms | 39ms |

| Page load time | Original bindings | Pre-built bindings | Absolute gain |
|---|---|---|---|
| Desktop | 346ms | 341ms | 5ms |
| Mobile | 902ms | 874ms | 28ms |

The serialized metadata for property-effects was big enough to trump the benefit of skipping parsing cost of properties.
Moreover, the property metadata was still required for other aspects of the Polymer metadata system for, for example, default values.
Pre-building property metadata would thus be feasible if and only if all property metadata is pre-built.
We discovered this caveat late in the process and there was not enough time to incorporate these changes in the time scope of the project.
Section “Further possible improvements” lists all extra opportunities.

The final build that was tested thus exclude property effects and only pre-built bindings. Based on the extra network time and binding metadata, a net benefit of 5ms on desktop and 28ms on mobile was determined. This is roughly 1-3% of the full pageload.

# Conclusion
Pre-building binding metadata is a performance benefit for loading websites, albeit marginal.
Depending on the usecase of the website (available bandwidth, CPU speed, mobile vs desktop), pre-building binding metadata is advisable.
The developed tool, given the requirements of perfect pre-building, has several gotchas that have to be taken into account when adopting the tool.
This largely concerns running the actual user code in a browser, without control of external dependencies.

Pre-building property effect metadata was deemed unfeasible in its current state.
Over the course of the project, we discovered various other points in the Polymer core library that depended on the properties.
An initial investigation showed that this information can be pre-built as well, however due to time limitations this project did not include these advancements.

## Next steps
The next step in the project are fleshing out integration and resolve bugs to make the tool usable in production.
At the same time, once Youtube uses Polymer 2, more performance tests can be performed on that codebase and potentially integrated in the Youtube build pipeline.

As the tool relies on Polymer core changes, in a future major release several improvements as proposed in the Pull Request can be incorporated.
Additionally, instead of having a separate tool, integration in Polymer Build and eventually [Polymer CLI](https://github.com/polymer/polymer-cli) would greatly improve the usability by Polymer end-users.

## Other general remarks
### Performance measurements
Measuring the performance of websites was deemed to be very error-prone.
Sometimes we had pair debugging sessions with 2-3 engineers to be able to find out various issues with performance testing.
Since performance was the key result of this project, the measurements had to be correct to be able to draw the correct conclusions.
Over the course of the project, several updates to [the perf-tester developed by the Polymer team](https://github.com/PolymerLabs/perf-tester/) were introduced fixing several issues, as well as a proposal for a [node-based solution](https://github.com/PolymerLabs/perf-tester/pull/4) that can integrate with the [Chrome DevTools Protocol](https://chromedevtools.github.io/devtools-protocol/).
This node perf-tester was also used to perform the measurements on a mobile phone.

### Further possible improvements
Besides binding metadata, there are some other possible pre-building opportunities.
For property-effects metadata, the properties definition must be removed completely and no additional computation should be required.
This includes:
1. Computing default values
1. Flattened list of properties for each class
1. Computing observed attributes
1. Property effects for each property.

### Friction of Polymer-Analyzer and Polymer core
There is existing friction between the implementation and output of the analyzer vs what Polymer core actually does.
Examples of discrepancies are resolution of properties in conjunction with behaviors, user overridden metadata parsing as well as any usage of the JavaScript API that does not conform to the usual usage of Polymer.

```js
const Behavior = {
   properties: {
       prop: {
           type: Number,
           notify: true
       }
   }
}

Polymer({
   is: 'my-element',
   behaviors: [Behavior],
   properties: {
       prop: {
           type: Number,
           reflectToAttribute: true
       }
   }
});
```
Figure 1: Example that is broken with the Polymer analyzer. The analyzer will only return the property metadata as defined in the element and discard the metadata defined in the behavior.

Polymer Analyzer does a best guess and for 95% of the use cases, this guess is correct.
For the usages of the analyzer (in the linter, code editors and documentation creation) this does a well enough job.
However, if a perfect output (compared to Polymer core) is required, the analyzer is lackluster.
This was the very reason for the adoption of Chrome Headless in the tool to obtain the actual output on run-time.

To solve this friction, these are three proposed enhancements:
1. Integrate Polymer Core modules into the analyzer.
    As part of the project, we integrated Polymer Core in a Node environment and run in conjunction with the analyzer.
    Since Polymer Core is created under the assumption of the availability of browser (DOM) APIs, this required manual patching of the environment:
    ```js
     // Patch up the global scope to be able to import Polymer code
     class MutationObserver {
      observe() {
      }
      disconnect() {
      }
     }

     const dom = new JSDOM();
     const window: any = dom.window;
     Object.assign(global, {
      window: global,
      HTMLElement: window.HTMLElement,
      Node: window.Node,
      customElements: {define() {}},
      JSCompiler_renameProperty: () => {},
      document: window.document,
      MutationObserver,
      requestAnimationFrame: setTimeout,
      cancelAnimationFrame: clearTimeout
     });
     ```
    With Polymer 3 and the switch to ES Modules, factorizing Polymer Core to extract general logic from browser-touching code allows Polymer tooling including the Analyzer reuse Polymer Core implementation.

    One aspect to this integration is the usage of ES Modules in a Node environment. A fortunate aspect is that Polymer tooling is written in TypeScript, which means that integrating ES Modules requires minimal changes to the TypesCript config.

1. Switch all DOM AST representations from [Dom5](https://github.com/Polymer/dom5) + [Parse5](https://github.com/inikulin/parse5) to [JSDom](https://github.com/tmpvar/jsdom).
JSDom implements a large subset of all available DOM API’s and as such is mostly compatible with Polymer core code relying on the browser environment.

1. Make use of a type system instead of manually parsing JS AST’s.
One caveat to this approach is that it requires the elements to be written with a type system in mind.
As this is not the case for the majority of the elements, adopting this option is only possible in the far future.
What might be possible is to optionally use the type system, if it is available.
In this scenario, the Polymer tooling uses the type system if it exists and falls back to a best guess as it does currently.


### Appendix: metadata optimizations
#### Lazy computation
When Polymer registers a custom element definition, it calculates all required values used to process all property effects.
This means that derived data from for example the property name is computed before the data is actually required.
Even if the property effect is never executed, the metadata is computed.

A concrete example is [the event name of the notify-propertyeffect](https://github.com/Polymer/polymer/blob/ca1ce19682b0003359090491d7e81a58d26b9a4a/lib/mixins/property-effects.html#L2039).
This eventName is used for [dispatchNotifyEvent](https://github.com/Polymer/polymer/blob/ca1ce19682b0003359090491d7e81a58d26b9a4a/lib/mixins/property-effects.html#L325).
However, if this property never changed or only in very specific cases, computing the event name is not required up to the usage of the property.
A solution thus is to move the computation on the usage side as such:
```js
const eventName = info.eventName
   || (info.eventName = CaseMap.camelToDashCase(rootProperty) + '-changed');
dispatchNotifyEvent(inst, eventName, value, path);
```
This small modification has two effects: First of all, there are now strictly fewer computations performed during custom element registration than before.
This means that in total, the CPU time of loading a Polymer application is equivalent or slightly faster.
Secondly, it means that during the serialization of the metadata, the eventName is not required to be serialized.
This removes a large chunk of the serialized metadata and thus improves the network load time.
The tradeoff of this optimization is that whenever the property effect is executed, the existence of `info.eventName` is checked.

#### Omission of “duplicate” data: closures
All property effects have a corresponding function callback that is able to process the effect metadata and perform the correct action.
For every property effect, the function callback is different and as such was stored on the property effect.
A closer inspection of the metadata showed that in a majority of the property effects the function was always the same.
This means that storing (and serializing + retrieving back the closure) the function in the metadata is in most cases unnecessary.
As such, the following can be updated:

##### Before
```js
runEffects(this, this[TYPES.REFLECT], changedProps, oldProps, hasPaths);
```

##### After
```js
runEffects(this, this[TYPES.REFLECT], changedProps, oldProps, hasPaths, undefined, EFFECT_FUNCTIONS.runReflectEffect);
```

#### Omission of “duplicate” data: effect info
All effects store additional info that is used in the corresponding function callback to execute the correct effect.
In some instances, data in the info object was not required.
An example is `info.property` for notify property-effects.
The value is always equivalent to the corresponding property argument of runNotifyEffect; storing this in the info object is therefore duplicate and could be omitted:

```js
function runNotifyEffect(inst, property, props, oldProps, info, hasPaths);
```

#### Storage format of template nodes

The storage format of template nodes was based on a recursive search algorithm based on indices.
When a node in a template has to be found, a nested parentInfo is passed to findTemplateNode which recursively obtains the parent and then based on the indices traverses the children to obtain the final node.
Serializing the nested parentInfo results in a lot of bytes, whereas the only required information is the index of each parent.
Rewriting the algorithm as such to operate on an array of indices (integers) results in the same finding algorithm, but significantly reduces the amount of bytes required to serialize the representation.
The tradeoff for this change is that instead of passing on a parentInfo object, the array pointing to the parent node has now to be copied and the current index has to be appended:

##### Before
```js
let childInfo = { parentIndex, parentInfo: nodeInfo };
```

##### After
```js
let childInfo = {
   parentInfo: nodeInfo.parentInfo.slice().concat(parentIndex)
};
```
Snippet taken from [`_parseTemplateChildNodes`](https://github.com/Polymer/polymer/blob/ca1ce19682b0003359090491d7e81a58d26b9a4a/lib/mixins/template-stamp.html#L283).
