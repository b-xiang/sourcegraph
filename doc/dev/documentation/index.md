# Sourcegraph documentation guidelines

> NOTE: Adapted from [GitLab documentation guidelines](https://gitlab.com/gitlab-org/gitlab-ee/raw/master/doc/development/documentation/index.md).

- **General documentation**: written by the [developers responsible by creating features](#contributing-to-docs). Should be submitted in the same pull request containing code. Feature proposals (by Sourcegraph contributors) should also be accompanied by its respective documentation. They can be improved later.
- **[Technical articles](#technical-articles)**: written by any Sourcegraph staff member, Sourcegraph contributors, or any member of the community.
- **Indexes per topic**: kept up-to-date by developers and PMs in the same pull request containing code. They gather all resources for that topic in a single page (user and admin documentation, articles, and third-party docs).

## Contributing to docs

Whenever a feature is changed, updated, introduced, or deprecated, the merge
request introducing these changes must be accompanied by the documentation
(either updating existing ones or creating new ones). This is also valid when
changes are introduced to the UI.

The one responsible for writing the first piece of documentation is the developer who
wrote the code. It's the job of the Product Manager to ensure all features are
shipped with its docs, whether is a small or big change. At the pace Sourcegraph evolves,
this is the only way to keep the docs up-to-date. If you have any questions about it,
ask a Technical Writer. Otherwise, when your content is ready, assign one of
them to review it for you.

We use the [monthly release blog post](https://about.sourcegraph.com/blog) as a changelog checklist to ensure everything
is documented.

## Documentation structure

Follow through the [documentation structure guide](structure.md) for learning
how to structure Sourcegraph docs.

## Documentation directory structure

<!-- TODO(sqs): continue customizing below here -->

The documentation is structured based on the Sourcegraph UI structure itself,
separated by [`user`](https://github.com/sourcegraph/sourcegraph/tree/master/doc/user),
[`administrator`](https://github.com/sourcegraph/sourcegraph/tree/master/doc/administration), and [`contributor`](https://github.com/sourcegraph/sourcegraph/tree/master/doc/development).

In order to have a [solid site structure](https://searchengineland.com/seo-benefits-developing-solid-site-structure-277456) for our documentation,
all docs should be linked. Every new document should be cross-linked to its related documentation, and linked from its topic-related index, when existent.

The directories `/workflow/`, `/gitlab-basics/`, `/university/`, and `/articles/` have
been **deprecated** and the majority their docs have been moved to their correct location
in small iterations. Please don't create new docs in these folders.

### Documentation files

- When you create a new directory, always start with an `index.md` file.
Do not use another file name and **do not** create `README.md` files
- **Do not** use special chars and spaces, or capital letters in file names,
directory names, branch names, and anything that generates a path.
- Max screenshot size: 100KB
- We do not support videos (yet)

### Location and naming documents

The documentation hierarchy can be vastly improved by providing a better layout
and organization of directories.

Having a structured document layout, we will be able to have meaningful URLs
like `docs.gitlab.com/user/project/merge_requests/index.html`. With this pattern,
you can immediately tell that you are navigating a user related documentation
and is about the project and its pull requests.

Do not create summaries of similar types of content (e.g. an index of all articles, videos, etc.),
rather organize content by its subject (e.g. everything related to CI goes together)
and cross-link between any related content.

The table below shows what kind of documentation goes where.

| Directory | What belongs here |
| --------- | -------------- |
| `doc/user/` | User related documentation. Anything that can be done within the Sourcegraph UI goes here including `/admin`. |
| `doc/administration/`  | Documentation that requires the user to have access to the server where Sourcegraph is installed. The admin settings that can be accessed via Sourcegraph's interface go under `doc/user/admin_area/`. |
| `doc/api/` | API related documentation. |
| `doc/development/` | Documentation related to the development of Sourcegraph. Any styleguides should go here. |
| `doc/legal/` | Legal documents about contributing to Sourcegraph. |
| `doc/install/`| Probably the most visited directory, since `installation.md` is there. Ideally this should go under `doc/administration/`, but it's best to leave it as-is in order to avoid confusion (still debated though). |
| `doc/update/` | Same with `doc/install/`. Should be under `administration/`, but this is a well known location, better leave as-is, at least for now. |
| `doc/topics/` | Indexes per Topic (`doc/topics/topic-name/index.md`): all resources for that topic (user and admin documentation, articles, and third-party docs) |

---

**General rules & best practices:**

1. The correct naming and location of a new document, is a combination
   of the relative URL of the document in question and the Sourcegraph Map design
   that is used for UX purposes ([source][graffle], [image][gitlab-map]).
1. When creating a new document and it has more than one word in its name,
   make sure to use underscores instead of spaces or dashes (`-`). For example,
   a proper naming would be `import_projects_from_github.md`. The same rule
   applies to images.
1. Start a new directory with an `index.md` file.
1. There are four main directories, `user`, `administration`, `api` and `development`.
1. The `doc/user/` directory has five main subdirectories: `project/`, `group/`,
   `profile/`, `dashboard/` and `admin_area/`.
   1. `doc/user/project/` should contain all project related documentation.
   1. `doc/user/group/` should contain all group related documentation.
   1. `doc/user/profile/` should contain all profile related documentation.
      Every page you would navigate under `/profile` should have its own document,
      i.e. `account.md`, `applications.md`, `emails.md`, etc.
   1. `doc/user/dashboard/` should contain all dashboard related documentation.
   1. `doc/user/admin_area/` should contain all admin related documentation
      describing what can be achieved by accessing Sourcegraph's admin interface
      (_not to be confused with `doc/administration` where server access is
      required_).
      1. Every category under `/admin/application_settings` should have its
         own document located at `doc/user/admin_area/settings/`. For example,
         the **Visibility and Access Controls** category should have a document
         located at `doc/user/admin_area/settings/visibility_and_access_controls.md`.
1. The `doc/topics/` directory holds topic-related technical content. Create
   `doc/topics/topic-name/subtopic-name/index.md` when subtopics become necessary.
   General user- and admin- related documentation, should be placed accordingly.

If you are unsure where a document should live, you can ping `@axil` or `@marcia` in your
pull request.

### Changing document location

Changing a document's location is not to be taken lightly. Remember that the
documentation is available to all installations under `help/` and not only to
Sourcegraph.com or http://docs.gitlab.com. Make sure this is discussed with the
Documentation team beforehand.

If you indeed need to change a document's location, do NOT remove the old
document, but rather replace all of its contents with a new line:

```
This document was moved to [another location](path/to/new_doc.md).
```

where `path/to/new_doc.md` is the relative path to the root directory `doc/`.

---

For example, if you were to move `doc/workflow/lfs/lfs_administration.md` to
`doc/administration/lfs.md`, then the steps would be:

1. Copy `doc/workflow/lfs/lfs_administration.md` to `doc/administration/lfs.md`
1. Replace the contents of `doc/workflow/lfs/lfs_administration.md` with:

    ```
    This document was moved to [another location](../../administration/lfs.md).
    ```

1. Find and replace any occurrences of the old location with the new one.
   A quick way to find them is to use `git grep`. First go to the root directory
   where you cloned the `gitlab-ce` repository and then do:

    ```
    git grep -n "workflow/lfs/lfs_administration"
    git grep -n "lfs/lfs_administration"
    ```

NOTE: **Note:**
If the document being moved has any Disqus comments on it, there are extra steps
to follow documented just [below](#redirections-for-pages-with-disqus-comments).

Things to note:

- Since we also use inline documentation, except for the documentation itself,
  the document might also be referenced in the views of Sourcegraph (`app/`) which will
  render when visiting `/help`, and sometimes in the testing suite (`spec/`).
- The above `git grep` command will search recursively in the directory you run
  it in for `workflow/lfs/lfs_administration` and `lfs/lfs_administration`
  and will print the file and the line where this file is mentioned.
  You may ask why the two greps. Since we use relative paths to link to
  documentation, sometimes it might be useful to search a path deeper.
- The `*.md` extension is not used when a document is linked to Sourcegraph's
  built-in help page, that's why we omit it in `git grep`.
- Use the checklist on the "Change documentation location" PR description template.

#### Alternative redirection method

Alternatively to the method described above, you can simply replace the content
of the old file with a frontmatter containing a redirect link:

```yaml
---
redirect_to: '../path/to/file/README.md'
---
```

It supports both full and relative URLs, e.g. `https://docs.gitlab.com/ee/path/to/file.html`, `../path/to/file.html`, `path/to/file.md`. Note that any `*.md` paths will be compiled to `*.html`.

### Redirections for pages with Disqus comments

If the documentation page being relocated already has any Disqus comments,
we need to preserve the Disqus thread.

Disqus uses an identifier per page, and for docs.gitlab.com, the page identifier
is configured to be the page URL. Therefore, when we change the document location,
we need to preserve the old URL as the same Disqus identifier.

To do that, add to the frontmatter the variable `redirect_from`,
using the old URL as value. For example, let's say I moved the document
available under `https://docs.gitlab.com/my-old-location/README.html` to a new location,
`https://docs.gitlab.com/my-new-location/index.html`.

Into the **new document** frontmatter add the following:

```yaml
---
redirect_from: 'https://docs.gitlab.com/my-old-location/README.html'
---
```

Note: it is necessary to include the file name in the `redirect_from` URL,
even if it's `index.html` or `README.html`.

## Linting

To help adhere to the [documentation style guidelines](styleguide.md), and to improve the content
 added to documentation, consider locally installing and running documentation linters. This will
 help you catch common issues before raising pull requests for review of documentation.

The following are some suggested linters you can install locally and sample configuration:

- `proselint`
- `markdownlint`

NOTE: **Note:**
This list does not limit what other linters you can add to your local documentation writing
 toolchain.

### `proselint`

`proselint` checks for common problems with English prose. It provides a
 [plethora of checks](http://proselint.com/checks/) that are helpful for technical writing.

`proselint` can be used [on the command line](http://proselint.com/utility/), either on a single
 Markdown file or on all Markdown files in a project. For example, to run `proselint` on all
 documentation in the [`gitlab-ce` project](https://github.com/sourcegraph/sourcegraph), run the
 following commands from within the `gitlab-ce` project:

```sh
cd doc
proselint **/*.md
```

`proselint` can also be run from within editors using plugins. For example, the following plugins
 are available:

- [Sublime Text](https://packagecontrol.io/packages/SublimeLinter-contrib-proselint)
- [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=PatrykPeszko.vscode-proselint)
- [Others](https://github.com/amperser/proselint#plugins-for-other-software)

#### Sample `proselint` configuration

All of the checks are good to use. However, excluding the `typography.symbols` checks might reduce
 noise. The following sample `proselint` configuration disables the `typography.symbols` checks:

```json
{
  "checks": {
    "typography.symbols": false
  }
}
```

A file with `proselint` configuration must be placed in a
 [valid location](https://github.com/amperser/proselint#checks). For example, `~/.config/proselint/config`.

### `markdownlint`

`markdownlint` checks that certain rules ([example](https://github.com/DavidAnson/markdownlint/blob/master/README.md#rules--aliases))
 are followed for Markdown syntax. Our [style guidelines](styleguide.md) elaborate on which choices
 must be made when selecting Markdown syntax for Sourcegraph documentation and this tool helps
 catch deviations from those guidelines.

`markdownlint` can be used [on the command line](https://github.com/igorshubovych/markdownlint-cli#markdownlint-cli--),
 either on a single Markdown file or on all Markdown files in a project. For example, to run
 `markdownlint` on all documentation in the [`gitlab-ce` project](https://github.com/sourcegraph/sourcegraph),
 run the following commands from within the `gitlab-ce` project:

```sh
cd doc
markdownlint **/*.md
```

`markdownlint` can also be run from within editors using plugins. For example, the following plugins
 are available:

- [Sublime Text](https://packagecontrol.io/packages/SublimeLinter-contrib-markdownlint)
- [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)
- [Others](https://github.com/DavidAnson/markdownlint#related)

#### Sample `markdownlint` configuration

The following sample `markdownlint` configuration modifies the available default rules to:

- Adhere to the [style guidelines](styleguide.md).
- Apply conventions found in the Sourcegraph documentation.

```json
{
  "default": true,
  "header-style": { "style": "atx" },
  "ul-style": { "style": "dash" },
  "line-length": false,
  "no-trailing-punctuation": false,
  "ol-prefix": { "style": "one" },
  "blanks-around-fences": false,
  "hr-style": { "style": "---" },
  "fenced-code-language": false
}
```

For [`markdownlint`](https://github.com/DavidAnson/markdownlint/), this configuration must be
 placed in a [valid location](https://github.com/igorshubovych/markdownlint-cli#configuration). For
 example, `~/.markdownlintrc`.

## Testing

We treat documentation as code, thus have implemented some testing.
Currently, the following tests are in place:

1. `docs lint`: Check that all internal (relative) links work correctly and
   that all cURL examples in API docs use the full switches. It's recommended
   to [check locally](#previewing-locally) before pushing to Sourcegraph by executing the command
   `bundle exec nanoc check internal_links` on your local
   [`gitlab-docs`](https://gitlab.com/gitlab-com/gitlab-docs) directory.
1. [`ee_compat_check`](../automatic_ce_ee_merge.md#avoiding-ce-gt-ee-merge-conflicts-beforehand) (runs on CE only):
    When you submit a pull request to Sourcegraph Community Edition (CE),
    there is this additional job that runs against Enterprise Edition (EE)
    and checks if your changes can apply cleanly to the EE codebase.
    If that job fails, read the instructions in the job log for what to do next.
    As CE is merged into EE once a day, it's important to avoid merge conflicts.
    Submitting an EE-equivalent pull request cherry-picking all commits from CE to EE is
    essential to avoid them.

## Branch naming

If your contribution contains **only** documentation changes, you can speed up
the CI process by following some branch naming conventions. You have three
choices:

| Branch name | Valid example |
| ----------- | ------------- |
| Starting with `docs/` | `docs/update-api-issues`     |
| Starting with `docs-` | `docs-update-api-issues`     |
| Ending in `-docs`     | `123-update-api-issues-docs` |

If your branch name matches any of the above, it will run only the docs
tests. If it doesn't, the whole test suite will run (including docs).

## Danger bot

Sourcegraph uses [danger bot](https://github.com/danger/danger) for some elements in
code review. For docs changes in pull requests, the following actions are taken:

1. Whenever a change under `/doc` is made, the bot leaves a comment for the
   author to mention `@gl-docsteam`, so that the docs can be properly
   reviewed.

## pull requests for Sourcegraph documentation

Before getting started, make sure you read the introductory section
"[contributing to docs](#contributing-to-docs)" above and the
[tech writing workflow](https://about.gitlab.com/handbook/product/technical-writing/workflow/)
for Sourcegraph Team members.

- Use the current [pull request description template](https://github.com/sourcegraph/sourcegraph/blob/master/.gitlab/merge_request_templates/Documentation.md)
- Use the correct [branch name](#branch-naming)
- Label the PR `Documentation`
- Assign the correct milestone (see note below)

NOTE: **Note:**
If the release version you want to add the documentation to has already been
frozen or released, use the label `Pick into X.Y` to get it merged into
the correct release. Avoid picking into a past release as much as you can, as
it increases the work of the release managers.

### Cherry-picking from CE to EE

As we have the `master` branch of CE merged into EE once a day, it's common to
run into merge conflicts. To avoid them, we [test for merge conflicts against EE](#testing)
with the `ee-compat-check` job, and use the following method of creating equivalent
branches for CE and EE.

Follow this [method for cherry-picking from CE to EE](../automatic_ce_ee_merge.md#cherry-picking-from-ce-to-ee), with a few adjustments:

- Create the [CE branch](#branch-naming) starting with `docs-`,
  e.g.: `git checkout -b docs-example`
- Create the EE-equivalent branch ending with `-ee`, e.g.,
  `git checkout -b docs-example-ee`
- Once all the jobs are passing in CE and EE, and you've addressed the
feedback from your own team, assign the CE PR to a technical writer for review
- When both PRs are ready, the EE pull request will be merged first, and the
CE-equivalent will be merged next.
- Note that the review will occur only in the CE PR, as the EE PR
contains the same commits as the CE PR.
- If you have a few more changes that apply to the EE-version only, you can submit
a couple more commits to the EE branch, but ask the reviewer to review the EE pull request
additionally to the CE PR. If there are many EE-only changes though, start a new PR
to EE only.

## Previewing the changes live

NOTE: **Note:**
To preview your changes to documentation locally, follow this
[development guide](https://gitlab.com/gitlab-com/gitlab-docs/blob/master/README.md#development-when-contributing-to-gitlab-documentation) or [these instructions for GDK](https://gitlab.com/gitlab-org/gitlab-development-kit/blob/master/doc/howto/gitlab_docs.md).

The live preview is currently enabled for the following projects:

- https://github.com/sourcegraph/sourcegraph
- https://gitlab.com/gitlab-org/gitlab-ee
- https://gitlab.com/gitlab-org/gitlab-runner

If your branch contains only documentation changes, you can use
[special branch names](#branch-naming) to avoid long running pipelines.

For [docs-only changes](#branch-naming), the review app is run automatically.
For all other branches, you can use the manual `review-docs-deploy-manual` job
in your pull request. You will need at least Maintainer permissions to be able
to run it. In the mini pipeline graph, you should see an `>>` icon. Clicking on it will
reveal the `review-docs-deploy-manual` job. Hit the play button for the job to start.

![Manual trigger a docs build](img/manual_build_docs.png)

NOTE: **Note:**
You will need to push a branch to those repositories, it doesn't work for forks.

The `review-docs-deploy*` job will:

1. Create a new branch in the [gitlab-docs](https://gitlab.com/gitlab-com/gitlab-docs)
   project named after the scheme: `$DOCS_GITLAB_REPO_SUFFIX-$CI_ENVIRONMENT_SLUG`,
   where `DOCS_GITLAB_REPO_SUFFIX` is the suffix for each product, e.g, `ce` for
   CE, etc.
1. Trigger a cross project pipeline and build the docs site with your changes

After a few minutes, the Review App will be deployed and you will be able to
preview the changes. The docs URL can be found in two places:

- In the pull request widget
- In the output of the `review-docs-deploy*` job, which also includes the
  triggered pipeline so that you can investigate whether something went wrong

In case the Review App URL returns 404, follow these steps to debug:

1. **Did you follow the URL from the pull request widget?** If yes, then check if
   the link is the same as the one in the job output.
1. **Did you follow the URL from the job output?** If yes, then it means that
   either the site is not yet deployed or something went wrong with the remote
   pipeline. Give it a few minutes and it should appear online, otherwise you
   can check the status of the remote pipeline from the link in the job output.
   If the pipeline failed or got stuck, drop a line in the `#docs` chat channel.

TIP: **Tip:**
Someone that has no merge rights to the CE/EE projects (think of forks from
contributors) will not be able to run the manual job. In that case, you can
ask someone from the Sourcegraph team who has the permissions to do that for you.

NOTE: **Note:**
Make sure that you always delete the branch of the pull request you were
working on. If you don't, the remote docs branch won't be removed either,
and the server where the Review Apps are hosted will eventually be out of
disk space.

### Technical aspects

If you want to know the hot details, here's what's really happening:

1. You manually run the `review-docs-deploy` job in a CE/EE pull request.
1. The job runs the [`scripts/trigger-build-docs`](https://github.com/sourcegraph/sourcegraph/blob/master/scripts/trigger-build-docs)
   script with the `deploy` flag, which in turn:
   1. Takes your branch name and applies the following:
      - The slug of the branch name is used to avoid special characters since
        ultimately this will be used by NGINX.
      - The `preview-` prefix is added to avoid conflicts if there's a remote branch
        with the same name that you created in the pull request.
      - The final branch name is truncated to 42 characters to avoid filesystem
        limitations with long branch names (> 63 chars).
   1. The remote branch is then created if it doesn't exist (meaning you can
      re-run the manual job as many times as you want and this step will be skipped).
   1. A new cross-project pipeline is triggered in the docs project.
   1. The preview URL is shown both at the job output and in the pull request
      widget. You also get the link to the remote pipeline.
1. In the docs project, the pipeline is created and it
   [skips the test jobs](https://gitlab.com/gitlab-com/gitlab-docs/blob/8d5d5c750c602a835614b02f9db42ead1c4b2f5e/.gitlab-ci.yml#L50-55)
   to lower the build time.
1. Once the docs site is built, the HTML files are uploaded as artifacts.
1. A specific Runner tied only to the docs project, runs the Review App job
   that downloads the artifacts and uses `rsync` to transfer the files over
   to a location where NGINX serves them.

The following Sourcegraph features are used among others:

- [Manual actions](../../ci/yaml/README.md#manual-actions)
- [Multi project pipelines](https://docs.gitlab.com/ee/ci/multi_project_pipeline_graphs.html)
- [Review Apps](../../ci/review_apps/index.md)
- [Artifacts](../../ci/yaml/README.md#artifacts)
- [Specific Runner](../../ci/runners/README.md#locking-a-specific-runner-from-being-enabled-for-other-projects)

## Sourcegraph `/help`

Every Sourcegraph instance includes the documentation, which is available from `/help`
(`http://my-instance.com/help`), e.g., <https://gitlab.com/help>.

The documentation available online on docs.gitlab.com is continuously
deployed every hour from the `master` branch of CE, EE, Omnibus, and Runner. Therefore,
once a pull request gets merged, it will be available online on the same day,
but they will be shipped (and available on `/help`) within the milestone assigned
to the PR.

For instance, let's say your pull request has a milestone set to 11.3, which
will be released on 2018-09-22. If it gets merged on 2018-09-15, it will be
available online on 2018-09-15, but, as the feature freeze date has passed, if
the PR does not have a "pick into 11.3" label, the milestone has to be changed
to 11.4 and it will be shipped with all Sourcegraph packages only on 2018-10-22,
with Sourcegraph 11.4. Meaning, it will only be available under `/help` from Sourcegraph
11.4 onwards, but available on docs.gitlab.com on the same day it was merged.

### Linking to `/help`

When you're building a new feature, you may need to link the documentation
from Sourcegraph, the application. This is normally done in files inside the
`app/views/` directory with the help of the `help_page_path` helper method.

In its simplest form, the HAML code to generate a link to the `/help` page is:

```haml
= link_to 'Help page', help_page_path('user/permissions')
```

The `help_page_path` contains the path to the document you want to link to with
the following conventions:

- it is relative to the `doc/` directory in the Sourcegraph repository
- the `.md` extension must be omitted
- it must not end with a slash (`/`)

Below are some special cases where should be used depending on the context.
You can combine one or more of the following:

1. **Linking to an anchor link.** Use `anchor` as part of the `help_page_path`
   method:

    ```haml
    = link_to 'Help page', help_page_path('user/permissions', anchor: 'anchor-link')
    ```

1. **Opening links in a new tab.** This should be the default behavior:

    ```haml
    = link_to 'Help page', help_page_path('user/permissions'), target: '_blank'
    ```

1. **Linking to a circle icon.** Usually used in settings where a long
   description cannot be used, like near checkboxes. You can basically use
   any font awesome icon, but prefer the `question-circle`:

    ```haml
    = link_to icon('question-circle'), help_page_path('user/permissions')
    ```

1. **Using a button link.** Useful in places where text would be out of context
   with the rest of the page layout:

    ```haml
    = link_to 'Help page', help_page_path('user/permissions'),  class: 'btn btn-info'
    ```

1. **Using links inline of some text.**

    ```haml
    Description to #{link_to 'Help page', help_page_path('user/permissions')}.
    ```

1. **Adding a period at the end of the sentence.** Useful when you don't want
   the period to be part of the link:

    ```haml
    = succeed '.' do
      Learn more in the
      = link_to 'Help page', help_page_path('user/permissions')
    ```

## General Documentation vs Technical Articles

### General documentation

General documentation is categorized by _User_, _Admin_, and _Contributor_, and describe what that feature is, what it does, and its available settings.

### Technical Articles

Technical articles replace technical content that once lived in the [Sourcegraph Blog](https://about.gitlab.com/blog/), where they got out-of-date and weren't easily found.

They are topic-related documentation, written with an user-friendly approach and language, aiming to provide the community with guidance on specific processes to achieve certain objectives.

A technical article guides users and/or admins to achieve certain objectives (within guides and tutorials), or provide an overview of that particular topic or feature (within technical overviews). It can also describe the use, implementation, or integration of third-party tools with Sourcegraph.

They should be placed in a new directory named `/article-title/index.md` under a topic-related folder, and their images should be placed in `/article-title/img/`. For example, a new article on Sourcegraph Pages should be placed in `doc/user/project/pages/article-title/` and a new article on Sourcegraph CI/CD should be placed in `doc/ci/examples/article-title/`.

#### Types of Technical Articles

- **User guides**: technical content to guide regular users from point A to point B
- **Admin guides**: technical content to guide administrators of Sourcegraph instances from point A to point B
- **Technical Overviews**: technical content describing features, solutions, and third-party integrations
- **Tutorials**: technical content provided step-by-step on how to do things, or how to reach very specific objectives

#### Understanding guides, tutorials, and technical overviews

Suppose there's a process to go from point A to point B in 5 steps: `(A) 1 > 2 > 3 > 4 > 5 (B)`.

A **guide** can be understood as a description of certain processes to achieve a particular objective. A guide brings you from A to B describing the characteristics of that process, but not necessarily going over each step. It can mention, for example, steps 2 and 3, but does not necessarily explain how to accomplish them.

- Live example: "[Static sites and Sourcegraph Pages domains (Part 1)](../../user/project/pages/getting_started_part_one.md) to [Creating and Tweaking Sourcegraph CI/CD for Sourcegraph Pages (Part 4)](../../user/project/pages/getting_started_part_four.md)"

A **tutorial** requires a clear **step-by-step** guidance to achieve a singular objective. It brings you from A to B, describing precisely all the necessary steps involved in that process, showing each of the 5 steps to go from A to B.
It does not only describes steps 2 and 3, but also shows you how to accomplish them.

- Live example (on the blog): [Hosting on Sourcegraph.com with Sourcegraph Pages](https://about.gitlab.com/2016/04/07/gitlab-pages-setup/)

A **technical overview** is a description of what a certain feature is, and what it does, but does not walk
through the process of how to use it systematically.

- Live example (on the blog): [Sourcegraph Workflow, an overview](https://about.gitlab.com/2016/10/25/gitlab-workflow-an-overview/)

#### Special format

Every **Technical Article** contains a frontmatter at the beginning of the doc
with the following information:

- **Type of article** (user guide, admin guide, technical overview, tutorial)
- **Knowledge level** expected from the reader to be able to follow through (beginner, intermediate, advanced)
- **Author's name** and **Sourcegraph.com handle**
- **Publication date** (ISO format YYYY-MM-DD)

For example:


```yaml
---
author: John Doe
author_gitlab: johnDoe
level: beginner
article_type: user guide
date: 2017-02-01
---
```

#### Technical Articles - Writing Method

Use the [writing method](https://about.gitlab.com/handbook/product/technical-writing/#writing-method) defined by the Technical Writing team.

[gitlab-map]: https://gitlab.com/gitlab-org/gitlab-design/raw/master/production/resources/gitlab-map.png
[graffle]: https://gitlab.com/gitlab-org/gitlab-design/blob/d8d39f4a87b90fb9ae89ca12dc565347b4900d5e/production/resources/gitlab-map.graffle
