## LivePerson Developers' Community

**As of August 2018, please open all Pull Requests DIRECTLY TO THE MASTER BRANCH**

This repository generates LivePerson's Developers' Community, which can be found at https://developers.liveperson.com. The site is generated using [Jekyll](https://jekyllrb.com/). If you find an issue with the documentation, site structure, meta or anything else, please open an issue and we'll respond as soon as possible!

**Table of Contents**

[Updating the Documentation](https://github.com/LivePersonInc/developers-community#updating-the-documentation)<br>
[Building the Site Locally](https://github.com/LivePersonInc/developers-community#building-the-site-locally)<br>
[Template](https://github.com/LivePersonInc/developers-community#template)<br>
[Licensing](https://github.com/LivePersonInc/developers-community#licensing)<br>

### Updating the Documentation

All pages on the site correspond to a Markdown file (.md) which can be found inside the "pages" folder, under the "documents" folder. To update a file, please branch off of the `master` branch, edit the file in question and create a Pull Request **back to the master branch**. There's no need for the old Development branch, so please don't create pull requests to it.

#### Updating/Creating Headers

Jekyll uses a [front-matter](https://jekyllrb.com/docs/frontmatter/) to arrange and define the various documents in the site. This is the text which appears in between the "---" at the top of each document. It's technically a YAML snippet, so all [YAML formatting](http://www.yamllint.com/) and rules apply to it. Our headers are usually comprised of the following key/value pairs:

* `pagename`: This is the name of the page that will appear at the top of the document.

* `keywords`: This replaces the keywords found in the `<meta>` tag of the page. Leave it unpopulated.

* `documentname`: This key can have either "Documents" or "Solutions". This designates which part of the site the document is under.

* `categoryname`: This is the category to which the document's API belongs (for example, the "Create Users" method belongs to the Users API which is under Contact Center Management. Therefore, its level2 is "Contact Center Management".

* `documentname`: This is the API to which the document belongs.

* `subfoldername`: This is a sub-folder to which the document belongs, if there is one.

* `root-link`: **DEPRECATED. No longer needed as the sidebar is now alphabetically organized and displays all document links**. This key accepts a Boolean value. If set to `true`, the document will be the "top" document for the API and all links to the API from the navigation will lead to it.

* `level-order`: **DEPRECATED. No longer needed as the sidebar is now alphabetically organized**. This key accepts an integer. If `root-link` is set to `true`, this key positions the parent API among its category. It is sequential, so 1 will display before 2 and 2 before 3 and so on. Thus, if the Users API (which is under Contact Center Management) has an "Overview" page that has `root-link` set to `true` and `level-order` set to `1`, it will appear before the Skills API (which is also under Contact Center Management) which has an "Overview" page that has `root-link` set to `true` but a `level-order` set to `2`.

* `order`:  **DEPRECATED. No longer needed as the sidebar is now alphabetically organized and the site hierarchy is determined by a manually updated YAML file. See below for more info**. This value accepts an integer. It arranges the documents inside the API. It is sequential, so 1 will display before 2 and 2 before 3 and so on. Note that it doesn't discriminate between folders, so even if you have `level4` defined for some documents, they are still placed on the same sequence as the rest of the documents.

* `permalink`: this key defines the link at which the document can be found. The format of this value **MUST BE** as follows. Any other value format will cause the sidebar to malfunction:

  * If the page has a `subfoldername` value: documentname - subfoldername - pagename. For example: `mobile-app-messaging-sdk-for-android-advanced-features-audio-messages.html`

  * If the page does not have a `subfoldername` value: documentname - pagename. For example: users-api-overview.html

* `indicator`: this key sets the Chat or Messaging indicator (or both) on a document. It accepts `chat`, `messaging` or `both` as its value.


#### Adding New Documents to the Sidebar

Once you've created a new document, you'll need to have it manually added. We chose a manual process for the side for a few reasons. First, it reduces the fragility of the sidebar (the extra, manual step gives us another layer of QA). Secondly, it increases the flexibility of the sidebar (we write code once and then maintain a YAML file, making it easier to add options). Lastly, it decreases site build times (since the `forloops` needed to build a sidebar in a site of our size and complexity are time and resource consuming).

The sidebar's YAML file can be found in the `_data` folder. It's called `documentsupdated.yaml`. **However, only the project's maintainer should edit this file directly. Please do not open Pull Requests with changes to this file but instead contact the project's maintainer directly. As of August 2018, this is Eden Kupermintz, the owner of this repository. You can reach him at edenk [at] liveperson [dot] com.**

### Building the Site Locally

If you have not already done so, make sure your computer has Ruby installed. Here's a helpful guide on how best do that on [Mac](http://railsapps.github.io/installrubyonrails-mac.html) (you can stop once Ruby is installed, you don't need Rails) and on [any other system](https://www.ruby-lang.org/en/documentation/installation/).

Once you have installed Ruby, clone this repository to your machine. Once done, navigate to it using Terminal or your preferred command line interface. Follow the steps below to run the site from your machine. **If you're on Windows, don't forget to run your CLI as an admin**.

**First time install**

0. Run `gem install bundler`. This will install Ruby's package manager which is required for all following commands.
1. Run `bundle install`. This will install all the gems/plugins that the site depends on.
2. Run `bundle exec jekyll build`. This builds the `_site` folder for the first time on your machine. The `bundle exec` prefix makes sure that bundler "watches" your build and installs any dependencies that might be missing. It's a precaution and is thus not mandatory.
3. Run `bundle exec jekyll serve`. This builds the site and serves it over localhost:4000 (by default, you can change the `port` parameter in `config.yml` to whatever port you'd prefer).
4. Navigate to http://localhost:4000/ (or the port you chose) and you'll see the site.

**OSX Installation**

0. We recommend installing a standalone Ruby Installation and RVM
1. See this for an example: [Stack Overflow](https://stackoverflow.com/questions/39381360/how-do-i-install-ruby-gems-on-mac)


**Serving the site after the first install**

You have two options to run the site after the first install:

* **Using gulp.js**. [Gulp](https://gulpjs.com/) is a toolkit for automating painful or time-consuming tasks. By simply typing in `gulp` in your command line, it takes care of all the build commands needed to serve the site. It also watches the root directory and will automatically refresh your browser once any changes were built. Gulp and its dependencies is installed locally in the project, so there's no further installation needed from your end.

* **Using Jekyll's standard commands**. All you need to run in consequent builds of the site is `bundle exec jekyll serve`. You can add the suffix `--incremental` to enable incremental building of the site. This saves build times since the regeneration feature is enabled by default (the site rebuilds every time you hit "save"). When `--incremental` is used, Jekyll won't rebuild the entire site on every save, only the affected sections. If you'd like the project to automatically open in a new tab, you can add the `-o` flag to the end of the above command.

**Note**: changes that alter site navigation or other changes that change the site as a whole might not show up when using `--incremental`. If that occurs, simply "kill" the build and run `bundle exec jekyll serve` without the suffix. **This is also true for gulp: you will need to kill your gulp instance and then run the direct Jekyll command**.

### Template

Since LivePerson maintains a few types of developer products, this template only applies to REST APIs. Other documents' structure will be determined on a case by case basis. For REST based APIs, the following template **must** be followed while it is only recommended for non-REST based products (for example, you're probably going to include an overview with any document but your product might not have methods).

#### Overview

The overview will contain a textual summary of what the API is capable of, including at least three use cases for the API. It will also describe the authentication method needed for the API, if one exists, and list any known limitations, if they exist.

[Here is a good example](https://github.com/LivePersonInc/developers-community/blob/master/pages/documents/ContactCenterManagement/AgentGroupsAPI/Introduction/overview.md) of an overview document which follows this template.

#### Methods

Each method for the API will have [its own page](https://github.com/LivePersonInc/developers-community/tree/master/pages/documents/ContactCenterManagement/AgentGroupsAPI/methods). Each page will contain a short description of what the method does.

It will then list the request format, including the method, the endpoint URL for it, any requisite headers, and the query parameters of the URL, if they exist. It will the list the request body and its format, breaking down each element in the body in a table and explaining what it does, whether its mandatory and if any notes exist for it.

It will then list an example of the response, breaking down its headers, body, and error codes, if they exist, in a table below the example.

[See this page](https://github.com/LivePersonInc/developers-community/blob/master/pages/documents/ContactCenterManagement/AgentGroupsAPI/methods/create-agent-groups.md) for an example of a method page which follows this template (though note that since all methods in this API share very similar body and entity structures, they are referred to commonly in an appendix).

#### Miscellaneous

Any other considerations, like special security measures, considerations, further limitations, example apps, and the such will be included in their own sections following the methods.

### Licensing

All usage of the contents, documentation or code found in this repository is subject to the [LivePerson API Terms of Use](https://www.liveperson.com/policies/apitou). Please use the link above to read them carefully before utilizing the site.
