{:title "Issue w/ default-value using reagent and rendering multiple times"
 :layout :post
 :tags  ["reagent" "react" "render" "web" "frontend" "hybrid" "mobile" "app"]
 :toc true}

currently i am creating a hybrid mobile app using [clojurescript](https://github.com/clojure/clojurescript) and the amazing [reagent](https://reagent-project.github.io/) library

during development i faced an issue w/ the "default-value" of an "input" tag. the way to reproduce the issue is as follows:

<code data-gist-id="e64770bd276ddb99d60b81ac5b0f6ead" data-gist-file="reagent-default-1.cljs"></code>

where

- we have 2 pages "from" and "to" and control cycles between them (they are rendered one after the other in cycles), starting from "from"
- "to" has a "form" w/ an "input" (type=text) field that has the "default-value" set to "hi there"
- what i noticed is that the 1st time that "to" was rendered, "hi there" was shown in the "input"
- but if you
  - change the value in the input (to say "hello world")
  - go to "from" (by clicking "Submit")
  - come again to "to" (by clicking "Click Me")
  - then the value shown for "input" becomes "hello world", instead of the expected "hi there"
  - this was confusing because, i expected "hi there" to be shown since (according to me) "to" was being rendered "freshly" (everytime control moved from "from" to "to")
  - the reason for this is that, as mentioned in the "Default Value -> Note" on [react forms docs](https://facebook.github.io/react/docs/forms.html), the "defaultValue" works only on the initial render. it also says that "If you need to update the value in a subsequent render, you will need to use a [controlled component](https://facebook.github.io/react/docs/forms.html#controlled-components)."

so we need to maintain the state for the "input" component as follows

<code data-gist-id="e64770bd276ddb99d60b81ac5b0f6ead" data-gist-file="reagent-default-2.cljs"></code>

fortunately, react has come up w/ a new [version v0.4](https://facebook.github.io/react/blog/2013/07/11/react-v0-4-prop-validation-and-default-values.html) which says that the behavior discussed above was a common pattern and has been implemented. and we should hopefully see the same supported in the next version of reagent too!
