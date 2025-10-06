---
title: Revising an Essay in Markdown with Git Version Control
subtitle: A Recipe for Beginners
date: \today
bibliography: cited-items.json
abstract: |
  This tutorial provides a step-by-step guide to revising an essay in Markdown format, using the Git version control system to record the process.
  We begin by converting our Microsoft Word DOCX file to a Markdown file.
  We then edit the Markdown file and commit our changes with Git.
  We add metadata (title and author);
  impose a one-sentence-per-line format (this facilitates sentence- and paragraph-level revision at a later stage);
  add section headings and other structural elements;
  and replace [hard-coded](https://en.wikipedia.org/wiki/Hard_coding) citations with citation keys.
  Revisions of argument and style are guided by @BoothCraftResearch2024.
  This work is backed up by pushing our commits to a remote repository on GitHub.
  In the final step, we write an overview of the revision process, framed as a demonstration of skills.
---

\newpage

[Getting Started with Pandoc]: https://pandoc.org/getting-started.html

# Prerequisites {.unnumbered}

The following software is required:

- [Zotero](https://www.zotero.org/download/), a reference-management system
- [Better BibTeX for Zotero](https://retorque.re/zotero-better-bibtex/installation/index.html), a plugin that improves Zotero's generation of citation keys and export of bibliographic data
- [A text editor with support for Markdown](https://alternativeto.net/category/productivity/text-editor/?feature=markdown-support&license=free)
- [Pandoc](https://pandoc.org/installing.html), a command-line tool to convert documents from one format to another
- [GitHub Desktop](https://desktop.github.com/download/) or the [Git command line application](https://git-scm.com/book/en/v2/Getting-Started-The-Command-Line), to create and manage file histories

All are available as free downloads.
Other prerequisites:

- An essay written in a word-processing program (such as Microsoft Word, Google Docs, or LibreOffice), with at least one cited source.
- Full bibliographic details for cited items, entered in your Zotero library.
  See Zotero's documentation on [Additing Items to Zotero](https://www.zotero.org/support/adding_items_to_zotero).
- A [GitHub account](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github).
  Choose the free option.
- A basic grasp of Markdown syntax.
  See the [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/) and documentation of [Pandoc's Markdown](https://pandoc.org/MANUAL.html#pandocs-markdown).

# Create Your Markdown File and Git Repository

(@) Locate your Microsoft Word (DOCX) essay.
If your essay is a Google Doc, download a DOCX file from the File menu.
Select "File" \> "Download" \> "Microsoft Word (.docx)."

(@) Open the terminal, following the instructions in [Getting Started with Pandoc], Step 2.

(@) In the terminal, navigate to the directory (a.k.a. folder) containing the DOCX copy of your essay, following the instructions in [Getting Started with Pandoc], Step 3.

(@) Use Pandoc to convert your DOCX file to a Markdown file.
In the directory that contains your DOCX files, run the command

    > ```{.bash}
    > pandoc SOURCEFILE.docx --wrap=none -so DESTINATION.md
    > ```

    Replace SOURCEFILE with the name of your DOCX file.
    Choose a DESTINATION filename with no spaces.
    Hyphens and underscores are fine.

(@init) Create a new Git repository on your computer.
If you use GitHub Desktop, follow the instructions for [Creating a New Repository with GitHub Desktop](https://docs.github.com/en/desktop/overview/creating-your-first-repository-using-github-desktop#creating-a-new-repository).
If you use a bash terminal, use `mkdir` then enter the new directory and run `git init`.

(@) Move the Markdown file that you created with Pandoc into the new Git repository.
This can be done with Mac OS Navigator or Windows File Explorer, or with the terminal command `mv`.

(@commit) Commit the Markdown file to the Git repository.
If you use GitHub Desktop, follow the instructions for [Committing Changes with GitHub Desktop](https://docs.github.com/en/desktop/overview/creating-your-first-repository-using-github-desktop#part-5-making-committing-and-pushing-changes).
If you use the terminal, run the commands

    > ```{.bash}
    > git add FILENAME.md
    > git commit -m "YOUR COMMIT MESSAGE"
    > ```

    A good commit message is "Add my essay as a Markdown file."

# Add Some Structural Formatting and an Abstract

(@) Open your Markdown file in a text editor.

(@) Add your name and the title of essay in a metadata block at the top of the file:

    > ```{.yaml}
    > ---
    > title: YOUR ESSAY TITLE
    > author: YOUR NAME
    > ---
    > ```

    Be sure to include the three hyphens (`---`) before and after.
    For details, see the section [YAML metadata blocks](https://pandoc.org/MANUAL.html#extension-yaml_metadata_block) in the Pandoc manual.
    (Depending on the properties of your DOCX file, Pandoc may have extracted this metadata for you.)

(@) Commit the changes, as in (@commit).
Supply an informative commit message.
For example: "Add the essay title and my name as metadata."

(@) In your text editor, read the entire essay.
As you read, use the Enter key to put each sentence on its own line.
For example, if your text looked like this:

    > ```
    > This is a first sentence. This is a second sentence.
    > ```

    it should now look like this:

    > ```
    > This is a first sentence.
    > This is a second sentence.
    > ```

    This step could be automated.
    I recommend doing it manually, as a way of refamiliarizing yourself with your essay.
    Resist the urge to make additional changes at this point.

(@) Commit the changes, as in (@commit).
Supply an informative commit message.
For example: "Put each sentence on its own line."

(@headings) Add section headings.
Read @BoothCraftResearch2024 [section 11.2].
Then add Markdown-formatted section headings to express the structure of your essay.
At minimum, enter the section heading

    > ```{.markdown}
    > # Conclusion
    > ```

    before your conclusion and the heading

    > ```{.markdown}
    > # Bibliography
    > ```

    before the bibliography (or lists of works cited).

(@point) Identify your "point sentence" (or claim or thesis).
Read your introduction and locate the sentence in which you state your claim.
Move the cursor to the end of that sentence, then type `<!--My claim-->`.
This text is just for you: it won't render when you convert your Markdown to a "publication format" such as DOCX or PDF.

(@) Read @BoothCraftResearch2024 on "Abstracts" (the "Quick Tip" at the end of chapter 11).
Then compose a brief abstract for your essay.
Put the abstract in the YAML metadata block at the top of the file, like this:

    > ```{.yaml}
    > ---
    > title: YOUR ESSAY TITLE
    > author: YOUR NAME
    > abstract: |
    >   FIRST SENTENCE OF YOUR ESSAY ABSTRACT
    >   NEXT SENTENCE ...
    > ---
    > ```

    For explanation of the pipe character (`|`) and indenting, see the Pandoc Manual, section on [YAML Metadata Blocks](https://pandoc.org/MANUAL.html#extension-yaml_metadata_block).

(@) Commit the changes as in (@commit), supplying an informative commit message.

# Create a Remote Back-up on GitHub

(@) Create a remote repository on GitHub and push your local history (that is, the changes you committed in previous steps) to this new remote repository.

    If you use GitHub Desktop, follow the instructions for [Publishing Your Repository to GitHub with GitHub Desktop](https://docs.github.com/en/desktop/overview/creating-your-first-repository-using-github-desktop#part-4-publishing-your-repository-to-github).
    If you use the terminal, follow the instructions for [Importing a Git Repository with the Command Line](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github#importing-a-git-repository-with-the-command-line).
    Either way, you will be prompted to choose whether to make your files public (that is, visible to anyone on the web) or keep them private (that is, visible only to you and invited collaborators).
    If you keep your repository private, I will ask you to add me as a collaborator, so that I can review your work.
    See GitHub's documentation on [Inviting a Team or Person](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/managing-teams-and-people-with-access-to-your-repository#inviting-a-team-or-person).
    You can also [change the visibility of your repository](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/setting-repository-visibility) later.

    Your GitHub repository provides a remote back-up for your work and enables you to share your work and collaborate, if desired.
    But Git does not sync automatically.
    Instead, it acts on your command.
    The underlying principle is *deliberate intentionality*.

    GitHub Desktop will display a button to "Push Origin": see step 6 in [Making, Committing, and Pushing Changes](https://docs.github.com/en/desktop/overview/creating-your-first-repository-using-github-desktop#part-5-making-committing-and-pushing-changes).
    If you use the terminal, the command `git status` will report whether you have local commits that are not yet pushed to your remote repository.
    The command `git push` will send those commits to the remote repository.
    If Git needs additional information, the output of `git push` will prompt you to provide it.

# Revise Citations and Quotations

(@) In Zotero, create a new folder within your library.
Move your cited items into the new folder.

(@csljson) Right-click the folder containing your cited items, then select "Export Collection."
In the pop-up window, select "Better CSL JSON" and check the box for "Keep updated."
Save the file as `cited-items.json` (or something similar), within the same directory that holds your Markdown file.

(@) Commit `cited-items.json` to your repository as in (@commit).

(@) In your text editor, add the following line to the metadata block in your Markdown file:

    > ```{.yaml}
    > bibliography: cited-items.json
    > ```

(@keys) Replace all [hard-coded](https://en.wikipedia.org/wiki/Hard_coding) citations with citation keys, as described in the Pandoc Manual, under [Citation Syntax](https://pandoc.org/MANUAL.html#citation-syntax).
Citation keys are given in the file `cited-items.json`, which you exported from Zotero in (@csljson).

(@) Delete the list of works cited from the end of your essay (but keep the section heading added in (@headings)).

(@) Commit the changes.
A good commit message might be "Replace citations with citation keys."

(@) Review each of your quotations.
Verify that you have an appropriate citation for each, and verify that each quotation conforms to one of the standard formats, as described by @BoothCraftResearch2024 [section 12.4]:
"dropped-in" quotations should be introduced by a short phrase,
and quoted words and phrases should be woven into the grammar of your own sentence.
Block quotations should be coded with Markdown's syntax for block quotations (`>`).
Revise as necessary.

(@) Read @BoothCraftResearch2024 [section 12.6] and verify that each quotation is followed by appropriate commentary and explanation.
The authors advise that "The length of your explanation should be proportional to the length of your quotation."
Revise as necessary.

(@) Commit the changes and push them to GitHub.
A good commit message might be "Revise quoting sentences and discussion of quotes."

# Check Your Work by Generating a DOCX File with Pandoc {#check-your-work}

(@) Open the terminal, following the instructions in [Getting Started with Pandoc], Step 2, then navigate to the directory (a.k.a. folder) containing your Git repository, created in (@init).

(@test) Use Pandoc to create a DOCX file from your Markdown file and JSON bibliography.
In the directory that contains your Git repository, run the command

    > ```{.bash}
    > pandoc FILENAME.md --citeproc -o test.docx
    > ```

    Replace FILENAME.md with the name of your Markdown file.
    You can replace `test.docx` with any valid DOCX file name. I often use `temp.docx`.

    If the command is successful, a new DOCX file will show up in GitHub Desktop (or within the output of `git status` on the command line).
    Check whether the file exists, but do not commit it to your repository.
    We treat DOCX files as ephemeral: the record of truth is provided by your plain text files.

(@bugfix) Open the DOCX file with a word processing application such as Microsoft Word.
Inspect the file.
Does it look as you expected?

    Review the changes in your revision history. How does each one show up in the DOCX file?
    Pay particular attention to the citation keys entered in (@keys).
    These have been rendered in Chicago author-date format.
    (The citation style may be changed at a later stage: see the section [Update the Citation Style].)

    Where you find a formatting error, do not revise or edit the DOCX file (which is ephemeral).
    Instead, edit the Markdown.
    Consult the documentation for [Pandoc's Markdown](https://pandoc.org/MANUAL.html#pandocs-markdown) as necessary.

    If you find an error in your bibliographic data, edit this in Zotero.
    If you checked the box "Keep updated" in (@csljson), Zotero will automatically regenerate the JSON file containing your machine-readable bibliographic data.

(@) Repeat (@test) and (@bugfix) as necessary.

(@) Commit the changes to your Markdown file (and JSON file, if necessary), but exclude the DOCX file.
If you use GitHub Desktop, uncheck the box beside the DOCX file.
A good commit message is "Fix formatting bugs."

# Create a `.gitignore` File

(@) Create a `.gitignore` file to ignore DOCX files.
Open a text editor and create a new file in your Git repository.
Name the file `.gitignore` (this name must be exact).
Notice the leading period.

(@) On the first line of your `.gitignore` file, type `*.docx*`.
This instructs Git to ignore all DOCX files.
Save the `.gitignore` file.
For more on `.gitignore` files see GitHub's documentation on [Ignoring Files](https://docs.github.com/en/get-started/git-basics/ignoring-files).

(@) In GitHub Desktop (or on the command line), verify that the DOCX file no longer appears in the list of files to be committed to your repository.
The DOCX file still exists, but its presence is now concealed from Git.

(@) Commit the `.gitignore` file to your repository.
A good commit message is "Ignore DOCX files."

# Revise the Introduction and Conclusion

(@) Read @BoothCraftResearch2024 [sections 14.1--4] and verify that your introduction agrees with the "common structure of introductions" recommended there.
Revise as necessary.
Move the cursor to the end of the sentence that completes the statement of *context*, then type `<!--Context of my argument-->`.
Next, move the cursor to the end of the sentence that completes the statement of the *problem*, then type `<!--Problem addressed in my argument-->`.
Your *claim* (or "statement of response") was already identified above, in (@point).

(@) Read @BoothCraftResearch2024 [sections 14.6], on "Finding Your First Few Words."
Verify that the opening words of your essay follow the advice given there.
Revise as necessary.

(@) Read @BoothCraftResearch2024 [section 14.7], on "Writing Your Conclusion."
If your conclusion does not yet employ the strategies recommended in this section, revise it.

(@) Review the changes you have made in the past three steps, then commit the changes and push them to GitHub.
A good commit message might be "Revise introduction and conclusion."

# Revise a Sample Body Paragraph: Clarity and Flow {#clarity-and-flow}

(@firsttwo) Read @BoothCraftResearch2024 [section 15.2], on "The First Two Principles of Clear Writing."
Attend especially to sec. 15.2.4 ("Diagnosis and Revision") and 15.2.7 ("Creating Main Characters").
Select *one* body paragraph in your essay, run the diagnostic tests described in sec. 15.2.4, and revise accordingly.

(@) Read @BoothCraftResearch2024 [section 15.3], on the principle "Old Before New."
Re-read the paragraph you selected for revision in (@firsttwo).
Run the diagnostic tests for the principle "Old Before New" and revise accordingly.

(@) Read @BoothCraftResearch2024 [section 15.5], on the principle "Complexity Last."
Re-read the paragraph you selected for revision in (@firsttwo).
Revise according to the principle "Complexity Last."

(@) Review the changes you have made in the past three steps, then commit the changes and push them to GitHub.
A good commit message might be "Revise a sample paragraph for clarity and flow."

# Update the Citation Style

By default, Pandoc renders citations in Chicago's author-date system.
Another citation style can be specified as described in [Specifying a Citation Style](https://pandoc.org/MANUAL.html#specifying-a-citation-style).
This section walks you through the steps.

(@) Read @BoothCraftResearch2024 [section 12.8] or @ChicagoManualStyle2024 [sections 13.2--3] and decide whether Chicago's author-date style is appropriate for your essay.
If yes, skip the next steps in this section.

(@) Find the desired style in the GitHub repository [`citation-style-language/styles`](https://github.com/citation-style-language/styles).
You are probably looking for
[APA](https://github.com/citation-style-language/styles/blob/b61592ea58b94d790fa36708048153989840552c/apa.csl),
[Chicago notes-and-bibliography](https://github.com/citation-style-language/styles/blob/b61592ea58b94d790fa36708048153989840552c/chicago-notes-bibliography.csl),
or
[MLA](https://github.com/citation-style-language/styles/blob/b61592ea58b94d790fa36708048153989840552c/modern-language-association.csl).

(@) Download the file.
Navigate to one of the style pages linked in the previous step.
Click the three horizontal dots near the top right corner of the page.
This opens a menu for "More file actions."
Select "Download."

(@) Move the downloaded file into your Git repository.

(@) In your text editor, add the following line to the metadata block at the top of your Markdown file:

    > ```{.yaml}
    > csl: STYLE-NAME.csl
    > ```

    Replace `STYLE-NAME.csl` with the name of the CSL file you downloaded in the previous step.
    For additional discussion see [Specifying a Citation Style](https://pandoc.org/MANUAL.html#specifying-a-citation-style).

(@) Re-run the steps in the section [Check Your Work](#check-your-work)

(@) Commit the changes and push them to GitHub.

# Last Things

(@) Read your essay aloud, start to finish, at medium pace and volume.
This should be done when your roommate is away.
I call it "the test of declamation."
When you get hung up on a sentence, pause and improve its structure, returning to steps in the section [Revise a Sample Body Paragraph](#clarity-and-flow).

(@) Check spellings.
Generate a DOCX file as described in (@test).
Using the spell-check feature in Microsoft Word (or your preferred word-processing program), review the suggested corrections to spelling.
Correct errors in your Markdown file, using your text editor.
Alternatively, if you use the bash terminal, you may check spellings with the utility `aspell`.

(@) Review the changes, then commit the changes and push them to GitHub.
A good commit message might be "Revise style and fix spelling errors."

# Create a README for Your Repository

(@) Using a text editor, create a new file with the name `README.md`.
In this file, write a brief overview of the files in your repository.
Identify the context in which you first wrote your essay and describe the tools and techniques used in revision of it.
Write for a potential employer: present your work as a professional portfolio, demonstrating *what you can do*.

(@) Commit the file to your repository and push it to GitHub.
A good commit message is "Create REAMDE.md."

# Version Information {.unnumbered}

This tutorial is maintained in the GitHub repository [`icornelius/plain-text-tutorials`](https://github.com/icornelius/plain-text-tutorials).

# Licensing {.unnumbered}

**CC0 1.0 Universal.**
By marking this work with a CC0 public domain dedication, the creator is giving up their copyright and allowing reusers to distribute, remix, adapt, and build upon the material in any medium or format, even for commercial purposes.

[See the License Deed](https://creativecommons.org/publicdomain/zero/1.0/)

# Bibliography
