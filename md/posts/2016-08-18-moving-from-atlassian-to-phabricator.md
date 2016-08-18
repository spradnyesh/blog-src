{:title "moving from atlassian products to phabricator"
 :layout :post
 :tags  ["phabricator" "atlassian" "jira" "confluence" "bitbucket"]
 :toc true}

one of the most important tools that one needs when setting up the infrastructure in a new-company/startup is a system that allows the following features

* user management
* projects
* wiki/documentation
* ticketing (w/ support for sprints)
* code repository hosting
* code review
* communication (chatting)
* continuous-integration
* integration of the above systems =>
  * able to reference documentation from ticket and vice-versa
  * able to reference ticket in commit message (automated)
  * able to reference code commit in ticket (automated)
  * able to reference doc/ticket/commit in chats
  * able to reference tickets in CI runs and vice-versa

while we've been using [atlassian](https://www.atlassian.com/) products ([jira](https://www.atlassian.com/software/jira), [confluence](https://www.atlassian.com/software/confluence) and [bitbucket](https://www.atlassian.com/software/bitbucket)) for about 4-5 months now, it has become restrictive due to the following reasons
* paid costs escalate very quickly
* critical components (like code-review) are absent or get missed if we try to keep costs under control

due to this we started looking at alternatives, and [phabricator](https://www.phacility.com/phabricator/) turned out to be an awesome alternative due to
* support all needed features out-of-box (or via plugins like ([sprint][https://github.com/wikimedia/phabricator-extensions-Sprint]))
* free to host (supports unlimited users)
* excellent integration across its sub-systems
* good [documentation](https://secure.phabricator.com/book/phabricator/)
* good support over [stackoverflow](http://stackoverflow.com/questions/tagged/phabricator), etc

i have started setting up the system, and will write another post shortly about the steps and hiccups. so stay tuned :)
