# Architecture Documentation

[![Azure Static Web Apps CI/CD](https://github.com/RealPage-Architecture/arch-docs/actions/workflows/azure-static-web-apps-zealous-wave-0ba715f10.yml/badge.svg)](https://github.com/RealPage-Architecture/arch-docs/actions/workflows/azure-static-web-apps-zealous-wave-0ba715f10.yml)

This is a documentation project built with [Hugo](https://gohugo.io/), and the [Hugo Relearn Theme](https://themes.gohugo.io/themes/hugo-theme-relearn/).

It enables us to write all of our documentation with standard [Markdown syntax](https://mcshelby.github.io/hugo-theme-relearn/cont/markdown/index.html), with a few awesome [Shortcodes](https://mcshelby.github.io/hugo-theme-relearn/shortcodes/index.html).

To make a contribution, follow the standard git-based pull-request workflow:

* create a branch
* make your changes
* commit your branch locally
* push your branch to the server/remote
* submit a pull request to merge the changes to `main`

**N O T E:** When a pull request is created, the branch that originated the pull request will be
built and deployed to a temporary server to simplify the review process. See "Build and deploy job" -> expand the "Build and deploy" step and
you should see a line something like:

> Visit your site at: https://zealous-wave-0ba715f10-53.centralus.3.azurestaticapps.net (prefix is always "zealous-wave", the rest of the subdomain will vary).

## Getting Started

1. Install Hugo **Extended** (it's very lightweight) and Go
    * **MacOS:** Use brew:  `brew install go` and `brew install hugo`
    * **Windows:**  Use Chocolatey (or scoop or winget): `choco install hugo-extended` and install *go* as per https://go.dev/doc/install
    * More information / details / options: [https://gohugo.io/getting-started/installing](https://gohugo.io/getting-started/installing)
3. Clone this repo.
4. To run with "watch for changes": `hugo serve` from root directory of repo
5. Browse to [http://localhost:1313](http://localhost:1313)

### Getting Started Using Docker

To avoid having to install any additional software on your development workstation you could clone repo and test
changes from a docker container.  Here's how:

1. Install [Docker and Docker Compose](https://docs.docker.com/compose/install/)
1. Clone this repo.
1. run `docker-compose up` from root directory of repo
1. Browse to [http://localhost:1313](http://localhost:1313). docker-compose mounts a cloned repo so any changes automatically take effect in the docker container instance of hugo.

## Editing Documents

All documents are written in Markdown, and located within the `Content` folder.

The reference documents you might need to refer to during content creation:

* [Markdown Syntax](https://mcshelby.github.io/hugo-theme-relearn/cont/markdown/index.html)
* [Code Highlighting](https://mcshelby.github.io/hugo-theme-relearn/cont/syntaxhighlight/index.html)
* [File Attachments](https://mcshelby.github.io/hugo-theme-relearn/shortcodes/attachments/index.html)
* [Mermaid Diagrams](https://mcshelby.github.io/hugo-theme-relearn/shortcodes/mermaid/index.html)
* [Notices](https://mcshelby.github.io/hugo-theme-relearn/shortcodes/notice/index.html)

## Custom Shortcodes

**N O T E:** The custom shortcodes are in the `layouts/shortcodes` directory.

### Stream Videos

[Microsoft Stream Videos](https://web.microsoftstream.com) can be embedded into
pages here with the following shortcode:

```text
{{% stream-video <guid> %}}
```

`<guid>` above is the ID for a Stream video.  If you click on a video within MS Stream
to watch it, you will see a URL that looks something like this:

[https://web.microsoftstream.com/video/d4a28b9a-5247-4543-b5ea-8f0b7fc96819?list=studio](https://web.microsoftstream.com/video/d4a28b9a-5247-4543-b5ea-8f0b7fc96819?list=studio)

In the above example, the **guid** following `/video` but before the `?` is what you
need for the shortcode, so the `<guid>` value would be:

`d4a28b9a-5247-4543-b5ea-8f0b7fc96819`  and the full shortcode syntax would be:

```text
{{% stream-video d4a28b9a-5247-4543-b5ea-8f0b7fc96819 %}}
```

### Lucidchart Diagrams

Any diagrams you create in Lucidchart can be embedded onto pages as well.

The shortcode is:

```text
{{% lucid <guid> <id> %}}
```

To get the **guid** and **id** values, choose the **"Share->Embed"** option within Lucidchart.

You should see a dialog that looks similar to this:
![lucid-share](lucid-share.png =800x)

The path value following `embeddedchart/` is the **guid** you need, and
the value following `id=` is the **id**.

**NOTE: Make sure to *Activate Embed Code* with the button shown!**

For this screenshot, the whole shortcode would be:

```text
{{% lucid a1a24334-ce3f-4f35-9c91-c26a81602cd7 y4ZiBM-uqnrd %}}
```

## VS Code Snippet for Notices

A [Visual Studio Code snippet](https://code.visualstudio.com/docs/editor/userdefinedsnippets) has been created to make creating notices easier.  There are
4 types:

* `note` (blue)
* `info` (yellow)
* `tip` (green)
* `warning` (red)

To use the snippet, you need to first **enable quickSuggestions for Markdown** (one time only):

1. Go to `Preferences->Settings` then search for `quickSuggestions`
2. Follow the link to `Edit in settings.json`
3. Toward the bottom of the file, paste in the following JSON:

```json
"editor.quickSuggestions": null,
    "[markdown]": {
      "editor.quickSuggestions": {
        "comments": "on",
        "strings": "on",
        "other": "on"
      }
    },
```

4. Close and save the settings.

Then you can type `note` followed by `<tab>` and you should see a choice list for the type of notice.  Pick the one you want, then hit tab and you should be able to type your notice.  Check it out!

![snippet](Hugo-Notice.gif)

**NOTE:** If you're curious, the snippet is defined in the `.vscode/notices.code-snippets` file in this repo.

## VS Code extension to lint Markdown syntax issues

Markdown syntax is reasonably flexible, but straying too far from the standard syntax can cause issues for some parsers.  
To ensure better compatibility, please install the VS Code **markdownlint** extension (by David Anson with extension ID **davidanson.vscode-markdownlint**) and then remedy issues that it identifies while creating or editing Markdown files.  
Warning examples [green boxes can be corrected, red box is not correctable]:
![snippet](markdownlint-warning-examples.gif)

**NOTE:** It is **not** always possible to remedy all warnings.  
As an example, item 4 in the above section warns about list prefix misnumbering because the linter incorrectly interprets the json block in item 3 as the end of the list.

## Creating New Documents

See [https://gohugo.io/getting-started/quick-start/#step-4-add-some-content](https://gohugo.io/getting-started/quick-start/#step-4-add-some-content)

```bash
hugo new path/to/file-name.md # creates a new page in the content folder: `path/to/file-name.md` with the correct boilerplate code
```

Then open the file and, in the top section, change `draft: true` to
`draft: false` (or remove the line entirely) if you want the page to be visible when published.

## Updating the Relearn Theme

The Relearn theme has been included as a `git submodule` and so updating it to the
most recent version is as you would do for any submodule:

```bash
git submodule update --recursive --remote
```

One thing I could not figure out how to do was more generically override the margins.

I had to modify `themes/hugo-theme-relearn/static/css/theme.css` for the following block:

```css
#body .flex-block-wrapper {
    margin-left: auto;
    margin-right: auto;    
    width: 100% !important;
}
```

The change was to add the `!important` and to remove the `max-width` setting.
