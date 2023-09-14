**The Input Events spec**

[Level 1](https://rawgit.com/w3c/input-events/v1/index.html)

[Level 2](http://w3c.github.io/input-events/)

Level 1 and 2 each have three implementations (Chrome, Firefox and Safari). Level 2 is close to the consensus reached within the Editing Taskforce at the end of 2016. Level 1 is a subset that was split off in early 2017, when the Chromium team announced that it would not implement the entire specifition. At this time Safari had already implemented the full specification. We also did not want to give up level 2 of the spec, because it actually resolves a lot of issues and there has been no counter-proposal to effectively solve these issues from the Android team or others. Given that Chromium team told the Editing Taskforce that it either had to release a spec with their proposed changes or they would drop the spec entirely, it was decided to split the specification in two levels. By 2022, most of level 2 has been implemented in Chromium, and level 2 was adjusted remove three IME-specific input types. With this change, the implementations in all three browsers are following level 2. 

Even though the specs look somewhat similar, they have to be handled quite differently by JavaScript editors:

* Level 1 gives the JS editor information about proposed changes from the user, but it makes the related DOM change be non-cancelable in many cases. The event is therefore only useful in combination with a way to roll back the DOM after the DOM change has been made, most likely a DOM-diffing library. In the case of IME, it is extra difficult to handle as DOM changes cannot be reverted before the composition has finished.

* Level 2 gives the JS editor information information about the proposed changes from the user and let's the JS author cancel the changes the browser otherwise would have done. There is one exception to this and that is IME, which cannot be canceled due to various technical constraints. A JS editor based on level 2 will therefore continue to rely on other techniques, such as DOM-diffing libraries or rolling browser-made DOM-changes back, to handle IME correctly. A test of trying to create an editor using the event was conducted by the CKEditor team in the second half of 2016 before it was implemented in browsers.
