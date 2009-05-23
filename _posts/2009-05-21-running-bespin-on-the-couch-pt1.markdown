---
title: Running Bespin on the Couch, Part 1

layout: post
---

Sparked by a [thread][bespin_thread] on the CouchDB Users mailing list with promises of beer and internet groupies, I've started a project to get [Bespin][] running as a CouchApp on CouchDB. The long-term goal is to allow you to create and edit CouchApps from within Bespin, which is itself a CouchApp.

[bespin_thread]: http://mail-archives.apache.org/mod_mbox/couchdb-user/200905.mbox/%3Ce2111bbb0905201618u76a2ca5s464e9d22a1ac7004@mail.gmail.com%3E
[bespin]: https://bespin.mozilla.com

My first goal was to get Bespin's UI functioning as a CouchApp. Except for a few small things, that's already finished.

Here's a few screenshots of Bespin running as a CouchApp on my local CouchDB:

[![Index][index_image]][large_index_image]
*Index Page*

[![Help][help_image]][large_help_image]
*Help Menu*

[![Dashboard][dashboard_image]][large_dashboard_image]
*Dashboard*

[![Editor][editor_image]][large_editor_image]
*Editor*

[index_image]: http://thinkingconcurrently.com/images/bespin/index_small.png
[large_index_image]: http://thinkingconcurrently.com/images/bespin/index.png
[help_image]: http://thinkingconcurrently.com/images/bespin/help_small.png
[large_help_image]: http://thinkingconcurrently.com/images/bespin/help.png
[dashboard_image]: http://thinkingconcurrently.com/images/bespin/dashboard_small.png
[large_dashboard_image]: http://thinkingconcurrently.com/images/bespin/dashboard.png
[editor_image]: http://thinkingconcurrently.com/images/bespin/editor_small.png
[large_editor_image]: http://thinkingconcurrently.com/images/bespin/editor.png


Over the next few days I'll be focusing on porting their filesystem implementation to CouchDB and CouchApp conventions. If you'd like to get involved, fork my [bespin\_couch][bespin_couch] project and have at it! Also, if anyone knows how I can make the GitHub repo track upstream changes from Bespin's Mercurial repo I'd like to get that setup so I'm not just working off of a snapshot.

[bespin_couch]: http://github.com/bbrowning/bespin_couch/tree/master

I haven't had time to integrate Disqus with the blog yet so for now if you have any comments please send me a message on [GitHub][github_profile] or a reply to [@bbrowning][twitter_profile] on Twitter.

[github_profile]: http://github.com/bbrowning
[twitter_profile]: http://twitter.com/bbrowning