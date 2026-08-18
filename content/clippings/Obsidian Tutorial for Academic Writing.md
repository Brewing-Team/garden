---
title: "Obsidian Tutorial for Academic Writing"
source: "https://medium.com/better-humans/obsidian-tutorial-for-academic-writing-87b038060522"
author:
  - "[[Leonardo Castorina]]"
published: 2025-03-02
created: 2025-05-26
description: "Obsidian is a powerful note-taking app that I use on a daily basis. In a previous article, I wrote about how to set up Obsidian for Productivity, specifically for scientific research: In this…"
tags:
  - "clippings"
---
[Sitemap](https://medium.com/sitemap/sitemap.xml)

[![Better Humans](https://miro.medium.com/v2/resize:fill:76:76/1*c_2w6a-GqcYDbmJFO8Frgw.png)](https://medium.com/better-humans?source=post_page---post_publication_sidebar-7038e003d060-87b038060522---------------------------------------)

Better Humans is one of the largest and oldest Medium’s publications on self-improvement and personal development. Our goal is to bring you the world’s most helpful writing on human potential.

[Follow publication](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fcollection%2Fbetter-humans&operation=register&redirect=https%3A%2F%2Fmedium.com%2Fbetter-humans%2Fobsidian-tutorial-for-academic-writing-87b038060522&collection=Better+Humans&collectionId=7038e003d060&source=post_page---post_publication_sidebar-7038e003d060-87b038060522---------------------post_publication_sidebar------------------)

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*tgvnP1YoKlW_GrRzyfK0yA.png)

O bsidian is a powerful note-taking app that I use on a daily basis. In a previous article, I wrote about how to set up Obsidian for Productivity, specifically for scientific research:## [How to Boost Your Productivity for Scientific Research Using Obsidian](https://universvm.medium.com/how-to-boost-your-productivity-for-scientific-research-using-obsidian-fe85c98c63c8?source=post_page-----87b038060522---------------------------------------)

Tools and workflows for managing your zettelkasten, projects, reading lists, notes, and inspiration during your PhD.

universvm.medium.com

[View original](https://universvm.medium.com/how-to-boost-your-productivity-for-scientific-research-using-obsidian-fe85c98c63c8?source=post_page-----87b038060522---------------------------------------)

## Table of Contents

In this article, I will show you how to use Obsidian for Academic Writing. We will cover the following topics:

1. [**Writing Notes from Papers**](https://medium.com/better-humans/#4099)  
	— [A. Connecting Zotero to Obsidian](https://medium.com/better-humans/#e2e2)  
	— [B. Literature Notes Templates](https://medium.com/better-humans/#536b)  
	— [C. Importing Highlights from Zotero](https://medium.com/better-humans/#91bc)
2. [**Writing a Manuscript**](https://medium.com/better-humans/#e70a)— [A. Insert a Citation in Markdown](https://medium.com/better-humans/#fca2)  
	— [B. Copy MLA Citations to Text](https://medium.com/better-humans/#764d)  
	— [C. LaTeX-like Figures and Section Referencing](https://medium.com/better-humans/#fae5) (**NEW: Added Jan/2023**)
3. [**Exporting your Text (with citations)**](https://medium.com/better-humans/#0907)— [A. Converting Links (Obsidian to Markdown notation)](https://medium.com/better-humans/#5fef)  
	— [B. Exporting to PDF, Word, LaTeX](https://medium.com/better-humans/#0c27)
4. [**Creating Academic Documents**](https://medium.com/better-humans/#de53) (**NEW: Added Dec/2022**)  
	— [A. Academic PDF (.pdf) / LaTeX (.tex) Export with Plugin](https://medium.com/better-humans/#cb65) **(NEW: Added Jun/2023)**  
	— [B. PDF (.pdf) Export with CSS](https://medium.com/better-humans/#20fd)  
	— [C. Bibliography (.bib) Export with Pandoc](https://medium.com/better-humans/#c058)  
	— [D. PDF (.pdf) Export with Custom Pandoc Template](https://medium.com/better-humans/#487f) (LEGACY)  
	— [E. LaTeX (.tex) Export with Custom Pandoc Template](https://medium.com/better-humans/#bd57) (LEGACY)
5. [Batch Edit & Update Notes](https://medium.com/better-humans/#e02c) **(NEW: Added Dec/2023)  
	**— [5A. Installing Obsidian Metadata and Backing up Vault](https://medium.com/better-humans/#f22a)  
	— [5B. Moving Metadata into Frontmatter](https://medium.com/better-humans/#810e)

## Quick Links

These are some quick links and shortcuts in case you need fast access

- [**Zotero**](https://www.zotero.org/)
- **Zotero Plugins:**  
	– [Zotfile](http://zotfile.com/)  
	– [BetterBibtex](https://retorque.re/zotero-better-bibtex/)
- **Obsidian Plugins:**  
	– [Citations](https://github.com/hans/obsidian-citation-plugin)  
	– [Pandoc Reference List](https://github.com/mgmeyers/obsidian-pandoc-reference-list)  
	– [Obsidian Enhancing Export](https://github.com/mokeyish/obsidian-enhancing-export)  
	– [Obsidian Link Converter](https://github.com/ozntel/obsidian-link-converter)  
	– [Obsidian Metadata](https://github.com/natelandau/obsidian-metadata)
- [**Pandoc**](https://pandoc.org/installing.html)**\-** [Pandoc-Crossref](https://github.com/lierdakil/pandoc-crossref) (for dynamic figure and section referencing)
- **Obsidian Shortcuts**:  
	– Preferences: CMD +,  
	– Command Palette: CMD + P

## 1\. Writing Notes from Papers

Z otero is a great open-source reference manager commonly used in academia. Only a few people know that it can be used for highlighting papers and annotating ideas on the PDF document itself. With some tweaks, we can get Zotero to sync this information with Obsidian, so as to have a more convenient space to take notes.

[**Table of Contents**](https://medium.com/better-humans/#469d)  
— 1 [A. Connecting Zotero to Obsidian](https://medium.com/better-humans/#e2e2)  
— 1 [B. Literature Notes Templates](https://medium.com/better-humans/#536b)  
— 1 [C. Importing Highlights from Zotero](https://medium.com/better-humans/#91bc)

## 1A. Connecting Zotero to Obsidian

To connect Zotero to Obsidian we need to export a.bib file which includes all the information about your papers. It’s essentially a JSON-looking file that looks like this:

```hs
@article{castorina2021,
  title = {{{PDBench}}: Evaluating Computational Methods for Protein-Sequence Design},
  shorttitle = {{{PDBench}}},
  author = {Castorina, Leonardo V and Petrenas, Rokas and Subr, Kartic and Wood, Christopher W},
  year = {2023},
  month = jan,
  journal = {Bioinformatics},
  volume = {39},
  number = {1},
  pages = {btad027},
  issn = {1367-4811},
  doi = {10.1093/bioinformatics/btad027},
  url = {https://academic.oup.com/bioinformatics/article/doi/10.1093/bioinformatics/btad027/6986968},
  urldate = {2023-01-26},
  langid = {english},
}
```

To do this, install the plugins:

• **Zotfile**: [http://zotfile.com/](http://zotfile.com/)  
• **BetterBibtex**: [https://retorque.re/zotero-better-bibtex/](https://retorque.re/zotero-better-bibtex/)

**Zotero > Tools > Add-ons > Gear Icon > "Install Add-on from file"** then Select the.xpi files and they will be installed.

Then, export your library as a.bib file by:

**Right Click on the library** > **Export Library > Select "BetterBibLatex" and Keep Updated (see below)**

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*OEiNbtOrlCY9I1S2WmUncQ.png)

Choose a path of your choice. It is a good idea to keep it in the cloud if you use multiple machines.

I would recommend you select your Zotero library to export and set it to automatically export “ **On Change** ”. This way your library is always updated as soon as new papers are added to your library. I suggest you export it to a folder you sync with a cloud service. In this case, I am using iCloud, but you could use any other cloud service.

Another option I would recommend is “ **Export Notes** ”. Essentially all your highlights and additional notes on papers will be converted to a field in the bibliography file which we can then access from Obsidian.

Check that you did everything correct, by going to the Better BibTex Preferences:

**Zotero > Preferences (shortcut: CMD +,) > Better BibTex > Open Better BibTex Preferences > Automatic Export**

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*-6RwEj-QxpIhcR_GAo9xcg.png)

## 1B. Literature Notes Templates

Now onto Obsidian, we will need the [Citations Plugin](https://github.com/hans/obsidian-%20citation-plugin). To install simply go to:

**Obsidian > Preferences > Community Plugins > Browse**  
Then type “Citation” in the search bar and click on “Enable”:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*2bMqpmfIrnFKhbbEx4diyg.png)

Once enabled, close the tab and go to the plugin page:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*SepYG9lL5dMgnQ0aZldKPg.png)

Set “ **Citation Database** ” format to “ **BibLaTeX** ” and for the “ **Citation database path** ” the path to your.bib file.

You can then scroll down to the template settings and customise how your literature notes will be created:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*YSW9-YS1gz3YnBDogFPwMA.png)

I use the following template:

```hs
---
Year: "{{year}}"
Author: "{{authorString}}"
Tags: 
  - '#paper'
URL: "{{URL}}"
DOI: "{{DOI}}"
Cite Key: "[@{{citekey}}]"
Links: 
  - 
---
# {{title}}
#### ({{year}}) - {{authorString}}

## Abstract

\`\`\`
{{abstract}}
\`\`\`

## Notes
{{note}}
```

An example of a note generated with this template is shown below:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*SUhPO0YORLy-JbvftZGsNQ.png)

## 1C. Importing Highlights from Zotero

What you’ve seen so far is great, however, if you do most of your highlighting on Zotero PDF files, we can also export them as part of the notes section in the template.

This is especially useful if you highlight on Zotero using a tablet and use their sync utility to sync with your laptop.

Start by opening a PDF file of a paper in Zotero, and highlight and annotate your document:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*FbgYZjdWx2acwQoitSjOgw.png)

In Zotero then find the paper you have highlighted, right-click, and then select “ **Add Note from Annotations** ”:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*iEreUUWE2rRvdpC9FyyNUA.png)

You will now see the annotations appearing as a note under the citation:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*jnVfPX8uLWPqUgdWfxZ-SQ.png)

In Obsidian, open the command palette with:

**CMD + P > “Citations: Refresh Citation Database”**

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*YIOMP00EQ_p6Sg_R16_6sw.png)

This allows your new papers and annotations to be re-loaded in Obsidian from the bibliography file.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*PQcWBha5ZrG8xORLX8ihtA.png)

If you’re having trouble with the annotations appearing empty, I would suggest exporting the bibliography file again from the preferences menu in Zotero and clicking “ **Export Now** ”:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*Nig7FtEiKPvIAqHdzegBlg.png)

## 2\. Writing a Manuscript

O verleaf and Latex are pretty well-established tools for writing papers. Here, I want to make the case for Obsidian for writing papers. For instance, you can convert your documents from **markdown** (Obsidian document format) to **Word, LaTeX,** or **PDF**, with live citations.

I find this especially useful at the early stages of writing when all my literature notes and ideas are in Obsidian, and the shape of the manuscript will change a lot. This is also great if you are making a poster in Inkscape, Sketch, or PowerPoint, as you can export your poster content to a Word document (including the citations).

If you want to proceed you’ll need to install [**Pandoc**](https://pandoc.org/installing.html). In my experience, installing Pandoc with [Brew](https://brew.sh/) is much easier if you are on macOS.

[**Table of Contents**](https://medium.com/better-humans/#469d)  
— 2 [A. Insert a Citation in Markdown](https://medium.com/better-humans/#fca2)  
— 2 [B. Copy MLA Citations to Text](https://medium.com/better-humans/#764d)  
— 2 [C. LaTeX-like Figures and Section Referencing](https://medium.com/better-humans/#fae5)

## 2A. Insert a citation in Markdown

If you have installed the **Citations** plugin in Obsidian, inserting a citation is as simple as:

**CMD + P > Citations: Insert Markdown Citations**

You’ll see a menu like the one below:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*vCgdjDx2b9axQYalJUrfWg.png)

In this menu you can search through your bibliography file. You can then add citations to a document. You can customise the way they look from the Citations plugin preferences.

## 2B. Copy MLA citations to text

If you create a literature note with the Citations plugin or you include a markdown citation in a document, you can use the [Pandoc Reference List](https://github.com/mgmeyers/obsidian-pandoc-reference-list) plugin to display active citations for the document:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*e9x6_4vgb2XkbLiqYUSE2Q.png)

This can then easily be copied (with formatting) into Word:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*alLslU75yWryeXjASagDHQ.png)

Your in-text citations will also be rendered when you hover on them. This is through the Pandoc References List plugin:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*xiATsBY8fHTJWGos0v-BwA.png)

You can install the plugin from Obsidian preference pane as explained earlier. I set up the plugin as such:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*sqtrmXdsP3JK8ueIZRsInA.png)

Make sure the path to the Bibliography file and pandoc are correct. If you are unsure about the pandoc path, open the terminal and type:

```hs
>>> which pandoc
/usr/local/bin/pandoc
```

## 2C. LaTeX-like Figures and Section Referencing \[NEW\]

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*vVfy0oL4uRyMHMNE3g9v1A.png)

If you have worked with LaTeX before, you will know about how easy it is to reference figure numbers, even if you were to insert new figures down the line. Something similar can be achieved with Markdown and Obsidian using Pandoc-Crossref ([https://github.com/lierdakil/pandoc-crossref](https://github.com/lierdakil/pandoc-crossref)).

The easiest way is to install using Homebrew on MacOS, (though it can similarly be installed in Linux and Windows):

```hs
brew install pandoc-crossref
```

Keep in mind that this works only if you also installed pandoc with brew.

Now, all you need is to write **{#fig:your\_fig\_name}** next to your figures as such:

```hs
![your nice caption](your_img_path.png){#fig:your_fig_name}
```

And in-text, reference the figure with: **@fig:your\_fig\_name**

Same thing can be done with sections:

```hs
# Your Section {#sec:your_section}
```

## 3\. Exporting Your Text

E xporting your notes will require:

- [Pandoc](https://pandoc.org/installing.html) (mentioned in **Section 2**)
- [Pandoc-Crossref](https://github.com/lierdakil/pandoc-crossref) (for dynamic figure/section references)
- [Obsidian Link Converter](https://github.com/ozntel/obsidian-%20link-converter)
- [Obsidian Enhancing Export](https://github.com/mokeyish/obsidian-%20enhancing-export)

As mentioned in the previous section, you can install the Obsidian Plugins from the community plugins under the preference panel.

[**Table of Contents**](https://medium.com/better-humans/#469d)  
— 3 [A. Converting Links (Obsidian to Markdown notation)](https://medium.com/better-humans/#5fef)  
— 3 [B. Exporting to PDF, Word, LaTeX](https://medium.com/better-humans/#0c27)

## 3A. Converting Links (Obsidian to Markdown notation)

First, we will use the Obsidian Link Converter to convert all links to markdown. **I suggest you do this for the current file only**. This is necessary due to compatibility issues with Pandoc. To do this:

**CMD + P > click the option to convert links in your active file to markdown.**

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*r777W9iySY6BEOoMYuAQLA.png)

This command converts image links from this format:

```hs
![Screenshot 2022-07-04 at 13.05.14.png]
```

to this:

```hs
![Screenshot 2022-07-04 at 13.05.14.png](../Images/Screenshot%202022-07-04%20at%2013.05.14.p
```

## 3B. Exporting to PDF, Word, LaTeX

The Enhancing Export plugin is very customisable and allows you to set different settings for each support file extension. These are the settings I use for Word, PDF, and Latex.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*XwY_grjkhE4xc_Q8voZZWQ.png)

Make sure you add the following **Extra Arguments**:

- **resource-path** which is where you keep the images or bibliography file used in your document. Personally, I keep all my Obsidian images in a folder called “Images,” which makes it easier. You can also have resource paths as long as you specify them. **Example**:
```hs
--resource-path ~/Library/Mobile\ Documents/iCloud\~md\~obsidian/Documents/knowledgebase/Images/
```

This leads the resource path to be in the Images folder inside Obsidian (in iCloud).

**NB: Notice that the path contains "\\" before a space. These are escape characters. If you have problems with your path, try using:**

```hs
--resource-path="YOUR_PATH_HERE"
```
- **bibliography** which is where you specify your bibliography file if you want your citations to be rendered. **Example:**
```hs
--bibliography="export-data.bib"
```
- **pdf-engine** is the path to pdflatex. To find it, simply type " **which pdflatex** " in your terminal. **Example**:
```hs
--pdf-engine=/Library/TeX/texbin/pdflatex
```
- **filter** if you have used latex-like references to images, you will need to add the pandoc-crossref as a filter **BEFORE** citeproc
```hs
--filter pandoc-crossref
```
- **number-section** ensures that each section is numbered accordingly
```hs
--number-sections
```
- **citeproc** tells pandoc to render the citations. We just add it as a flag like this:
```hs
--citeproc
```
- **reference\_title** controls the name of the references section:
```hs
-M reference-section-title=References
```

Examples of the full Extra Arguments configs (for PDF, Word and LaTeX):

```hs
--resource-path ~/Library/Mobile\ Documents/com~apple~CloudDocs/ 
--resource-path ~/Library/Mobile\ Documents/iCloud\~md\~obsidian/Documents/knowledgebase/Images/ 
--csl https://raw.githubusercontent.com/csthiago/zotero-citation-styles/master/ieee.csl
--bibliography="export-data.bib" 
--pdf-engine=/Library/TeX/texbin/pdflatex
--filter pandoc-crossref
--number-sections
--citeproc
-M reference-section-title=References
```

Once you are done, you will see that the document will contain all your images and citations. If you exported to latex, all the citations will be rendered from your.bib file.

Note that you can pass a.csl file for citation styles. You can either use a file or a URL as above. You can find other styles in the repository: [https://github.com/csthiago/zotero-citation-styles](https://github.com/csthiago/zotero-citation-styles)

Once you found the style you are interested in, click on it, then click on "Raw" and copy the URL:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*F7cPVFb9-ZZpjnKV9oMAtQ.png)

## 4\. Creating Academic Documents

Section 3 showed you how you can produce a document. Here we will look into styling these into professionally-looking academic documents.  
There are two ways to do this: with an Export Plugin or with CSS

[**Table of Contents**](https://medium.com/better-humans/#469d)  
— 4 [A. Academic PDF (.pdf) / LaTeX (.tex) Export with Plugin](https://medium.com/better-humans/#cb65)  
— 4 [B. PDF (.pdf) Export with CSS](https://medium.com/better-humans/#20fd)  
— 4 [C. Bibliography (.bib) Export with Pandoc](https://medium.com/better-humans/#c058)  
— 4 [D. PDF (.pdf) Export with Custom Pandoc Template](https://medium.com/better-humans/#487f) (LEGACY)  
— 4 [E. LaTeX (.tex) Export with Custom Pandoc Template](https://medium.com/better-humans/#bd57) (LEGACY)

## 4A. Academic PDF (.pdf) / LaTeX (.tex) Export with Plugin

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*nHsu04oEUOItICJvO9YkGw.gif)

Demo of Obsidian Enhancing Export templates

The advantage of using this solution over CSS is that figures and references are rendered in full, much like latex. I developed a feature of the Obsidian Enhancing Export plugin which allows the selection of academic templates from a dropdown menu (see.gif).

If you followed the steps in **Section 3b**, simply run:

**CMD + P > "Obsidian Enhancing Export: Export To…" > Set Type as "PDF"**

From the dropdown select your template of choice and that should be it. At the time of writing there are two templates available: Dissertation and NeurIPS (academic). Refer to this repository for more information on how to use each one of them: [https://github.com/universvm/obsidian-pandoc-templates](https://github.com/universvm/obsidian-pandoc-templates)

## 4B. PDF (.pdf) Export with CSS

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*NDEQ8M8V1HoJfmcQFf57-A.png)

Sample exported document using the CSS style: https://github.com/NicklasVraa/Obsidian-academic-export

This involves adding a custom.css file to Obsidian. Simply go to this website:

[https://raw.githubusercontent.com/NicklasVraa/Obsidian-academic-export/main/academic-pdf-export.css](https://raw.githubusercontent.com/NicklasVraa/Obsidian-academic-export/main/academic-pdf-export.css)

And save the file.

Now go to **Obsidian > Preferences > Appearance > CSS Snippets**

Click on the Folder icon and drag your [academic-pdf-export.css](https://raw.githubusercontent.com/NicklasVraa/Obsidian-academic-export/main/academic-pdf-export.css) file to it. Your preferences should now look like this:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*i0XAY8TKevMlst3J1h24Aw.png)

Custom CSS file in Obsidian

Now, open a note and use the command pallette (CMD/CTRL + P) to select "Export to PDF". Your output should now be nicely formatted.

## 4C. Bibliography (.bib) Export with Pandoc

If using the methods above you may wonder how to export a.bib file containing uniquely the citations used in your document and filter out any entries that are not referenced in the document.

As before we go into the Export Setting preferences. In "Choose Template" select "Extra Arguments":

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*U_4zFb8tiAOJdOfNZIVMwQ.png)

For the command, paste the following and adapt as for the previous section:

```hs
--to=biblatex
--resource-path ~/Library/Mobile\ Documents/com~apple~CloudDocs/ 
--bibliography="export-data.bib"
```
- The **— to=biblatex** flag selects the output file extension to “.bib”
- You can reuse the same **— resource-path** and **— bibliography** as before.

And there you have it! It should now export to a.bib file in your selected output path. As before:

**CMD + P > “Obsidian Enhancing Export: Export To…” > Set Type as “Bibliography”**

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*eUPL4smClQjq9S3AOS-fUg.png)

## 4D. PDF (.pdf) Export with Custom Pandoc Template (LEGACY)

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*pFx4grit-e0GW5PXo_F7zw.png)

An example of a more sophisticated academic document using pandoc template https://github.com/universvm/obsidian-pandoc-templates/tree/main/dissertation

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*b3TJ4anKjyokTPCjOvp5Iw.png)

Another example of a a thesis-like academic document using pandoc template https://github.com/universvm/obsidian-pandoc-templates/tree/main/dissertation

If you followed the guide above and have Pandoc setup, using a custom template is also relatively simple. We essentially just need to add the custom template to Pandoc.

First download the file pandoc template file from here: [https://github.com/universvm/obsidian-pandoc-templates/tree/main/dissertation](https://github.com/universvm/obsidian-pandoc-templates/tree/main/dissertation)

Then, open a terminal and type:

```hs
pandoc --version
```
![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*BW4Fm-kC2rtRLnfU18RVJA.png)

You will find your **user data directory** path. Open that path, and if it does not exist create a folder called "pandoc" in there.

Now, create another folder called "templates" and place the **eisvogel.tex** file in there. Your folder should look like this:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*qm4sDQRpZ075Obl11EsaqQ.png)

Back to Obsidian, go to Preferences > Export Settings and under Choose Setting create a new one called "Academic PDF":

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*bu7UtSG9W8GeudCGXnuiBQ.png)

In the extra arguments we want to select the template like this:

```hs
--number-sections
--resource-path ~/Library/Mobile\ Documents/com~apple~CloudDocs/
--resource-path ~/Library/Mobile\ Documents/iCloud\~md\~obsidian/Documents/knowledgebase/Images/
--filter pandoc-crossref
--citeproc
--bibliography="export-data.bib"
--pdf-engine=/Library/TeX/texbin/pdflatex
--template eisvogel.tex 
-M reference-section-title=References
--csl https://raw.githubusercontent.com/csthiago/zotero-citation-styles/master/ieee.csl
--metadata link-citations
```

Now, open a note, open the command palette and click on **Obsidian Enhancing Export: Export To….** select **Academic PDF** and click on **Export.**

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*vlaHWdGZ0_ugPFMvPKyGEA.png)

To produce the document in the screenshot I added the following before my note (YAML):

```hs
---
title: "Thesis Title"
subtitle: "Another Subtitle"
titlepage: True
toc: true
toc-own-page: True
author: [Example Author]
date: "2022-02-12"
keywords: [Markdown, Example]
titlepage-text-color: "000000"
titlepage-rule-color: "FFFFFF"
titlepage-rule-height: 0
toc-title: Table of Contents
caption-justification: justified
titlepage-logo: /Users/your_name/Documents/logo.pdf
abstract: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec eu accumsan nisl. Phasellus suscipit varius arcu nec congue. Ut non pharetra dui. Phasellus gravida lectus eget maximus tincidunt. Nam ut ex vel enim elementum malesuada. Proin sit amet iaculis velit, non feugiat nulla. In facilisis tempor posuere. Nunc id dui eget lacus accumsan finibus. Ut id ex condimentum, egestas leo quis, tincidunt neque. Proin tincidunt, odio a sagittis rutrum, erat mi volutpat lorem, non iaculis odio sem in dui.
acknowledgements: Donec nec sapien porttitor, pharetra odio ac, suscipit nulla. Nulla mattis purus a facilisis vestibulum. Curabitur orci lorem, convallis ut odio quis, bibendum malesuada ligula. Pellentesque ultrices velit et hendrerit vulputate. Duis lobortis quis dui et condimentum. Aenean elementum id ex sit amet placerat. Vivamus a rhoncus dui, id volutpat nibh. Ut suscipit et augue eget imperdiet. Phasellus mattis vitae lectus nec pulvinar. Nulla pulvinar risus finibus tortor aliquam lacinia. Curabitur sagittis id turpis non varius.
text1: Doctor of Philosophy
text2: School of Informatics
text3: University of Edinburgh
text4: 2022
---
```

There are a lot more configs you can use. The full list is available here: [https://github.com/Wandmalfarbe/pandoc-latex-template](https://github.com/Wandmalfarbe/pandoc-latex-template)

The version you installed is a slightly modified version of the above to allow for an Abstract, Acknowledgement and general styling.

## 4E. LaTeX (.tex) Export with Custom Pandoc Template \[LEGACY\]

Should you want to export to a.tex file so that you can upload to Overleaf you can simply create a new export option but selecting "Latex" as Template:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*_kJi_SvYD4HKk8FWryZVMg.png)

And in the extra arguments use:

```hs
--resource-path ~/Library/Mobile\ Documents/com~apple~CloudDocs/ 
--resource-path ~/Library/Mobile\ Documents/iCloud\~md\~obsidian/Documents/knowledgebase/Images/  
--bibliography="export-data.bib" 
--template eisvogel.tex 
--extract-media ~/Desktop/images 
--natbib
```

Note that:

- The **extract-media** flag will output all the figures contained in the LaTeX document in the *~/Desktop/images* path. This way you can upload only the relevant images rather than your entire Obsidian folder.
- The **natbib** flag will ensure that natbib is used for citations with the correct \\cite{} command.

## 5\. Batch Edit & Update Notes (Advanced)

There will be times where you may need to update *a lot* of notes. For example either because you changed the format of your notes or to convert old links to the new Obsidian Frontmatter. For example, your notes might have these types of link:

```hs
Year:: 2017
Author:: Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Lukasz Kaiser, Illia Polosukhin
Tags:: #paper #ml/transformers 
URL:: http://arxiv.org/abs/1706.03762
DOI:: 10.48550/arXiv.1706.03762
Cite Key:: [@vaswani2017]
Links:: [Attention](../2.%20Notes/Attention.md) [Transformers](../2.%20Notes/Transformers.md)
```

As of December 2023, Obsidian has introduced native YAML properties. These are properties for a document that works very much in the same way as the one above, but they look like this:

To do this we will use [Obsidian Metadata](https://github.com/natelandau/obsidian-metadata). A Python tool to edit your notes.

**!!!Make sure you backup your vault before doing any of this!!!**

[**Table of Contents**](https://medium.com/better-humans/#469d)  
— [5A. Installing Obsidian Metadata and Backing up Vault](https://medium.com/better-humans/#f22a)  
— [5B. Moving Metadata into Frontmatter](https://medium.com/better-humans/#810e)

## 5A. Installing Obsidian Metadata and Backing up Vault

If you have Python setup in your laptop, installing is as simple as:

```hs
pip install obsidian-metadata
```

Then, open a Terminal and navigate to your vault. My Vault is synced to iCloud so I used this command:

```hs
cd "/Users/leo/Library/Mobile Documents/iCloud~md~obsidian/Documents/"
```

Make sure that you enclose the path with "" so that spaces are interpreted correctly.

Once installed, check that you have access to the program by running:

```hs
obsidian-metadata
```

It should return something like this:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*5YkdBrKaEVG08u2l-RdtDw.png)

Let's back up the vault by going to **Vault Action** and then **Backup Vault**

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*gXeWto33gGv6L_V1zgXuPg.png)

This should create a file called "YOUR\_VAULT\_NAME.bak". **Do not proceed until this is created.**

## 5B. Moving Metadata into Frontmatter

Navigate down to the "Reorganize Metadata" section and click Enter:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*DJD1jL0vYvpHoW94jQZc-w.png)

Now move to "Transpose inline to frontmatter" and again click Enter.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*HLN71AabAT8chPYSGhSgHg.png)

Now onto moving the properties from inline to YAML. I suggest you use " **Transpose a key** " and repeat this process for every key to ensure that your notes look good.

Be very careful with the "Transpose all Inline Metadata to Frontmatter", especially if you do not have a backup.

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*8OIFX9DudMTrx_m3gzrpOQ.png)

Now type the name of the key, for example "DOI"

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*EoI0QjQZylRrJJZtzYdooA.png)

Before moving on, select "Review Changes". Ideally you should see all the files you have edited using this tool:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*gI2AC4vkANcOfLupWL040A.png)

If you are satisfied, go back to the original menu by pressing "CTRL+C" and select **Commit Changes.**

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*Ky953ErdHdum_9yFQ3Ykug.png)

You will be asked whether you want to backup. **If you have not done so, this is your last chance to backup your vault. Please do not proceed unless you have a backup.**

You will be asked to commit the changes:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*c6nyESIiMqqVU8c4iHoLOg.png)

Your note should hopefully look like this:

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*5pPlJAMFRuHTFZAXO_pOWQ.png)

If anything has gone wrong during this operation, simply find the "YOUR\_VAULT\_NAME.bak" file in your folder. You can safely move your vault gone wrong somewhere else and the backup to "YOUR\_VAULT\_NAME".

## Conclusion

In this article, I showed my entire workflow for writing academically using Obsidian while syncing everything with iCloud.

The workflow is meant to help you deal with installing and setting up plugins and is the result of hours of work and research through forum posts.

First, we saw how to connect Zotero, a popular reference manager, to Obsidian and sync literature notes and highlights into notes files.

Then, I explained how I use markdown citations to help me build a draft for a manuscript. The citations can then be rendered using pandoc and exported to text, which is helpful if you’re creating a poster with InkScape or PowerPoint.

Finally, we set up the Obsidian Enhancing Export plugin with Pandoc to generate Latex, Word, and PDF documents to then import to Overleaf or send to other authors as a draft.

Cherry on top is a short tutorial on how to create academically-looking (and visually pleasing) documents with CSS and pandoc templates.

I hope you enjoyed the article and if you are having any problems feel free to comment! I'd like to thank Discord users FeralFlora, pseudometa, and everyone that helped me test these workflows!

## ☕️ Support My Work!

I’m Dr. Leucine, sharing insights on 🧠 knowledge management with Obsidian and 🍥 protein design. If you find my content helpful, consider buying me a coffee to keep the ideas flowing!

[👉 Buy me a coffee](https://buymeacoffee.com/drleucine)

## Further Readings

If you are interested in my work, I wrote about productivity apps and Obsidian:## [20+ MacOS Apps to Boost Your Productivity](https://universvm.medium.com/20-macos-apps-to-boost-your-productivity-74accb372c9c?source=post_page-----87b038060522---------------------------------------)

A collection of 20+ apps to significantly boost your productivity on MacOS

universvm.medium.com

[View original](https://universvm.medium.com/20-macos-apps-to-boost-your-productivity-74accb372c9c?source=post_page-----87b038060522---------------------------------------)## [How to Boost Your Productivity for Scientific Research Using Obsidian](https://universvm.medium.com/how-to-boost-your-productivity-for-scientific-research-using-obsidian-fe85c98c63c8?source=post_page-----87b038060522---------------------------------------)

Tools and workflows for managing your zettelkasten, projects, reading lists, notes, and inspiration during your PhD.

universvm.medium.com

[View original](https://universvm.medium.com/how-to-boost-your-productivity-for-scientific-research-using-obsidian-fe85c98c63c8?source=post_page-----87b038060522---------------------------------------)

Edit: My article " [**How to Boost Your Productivity for Scientific Research Using Obsidian**](https://betterhumans.pub/how-to-boost-your-productivity-for-scientific-research-using-obsidian-fe85c98c63c8) " article won the Student-Pick Prize of the Obsidian October 2022 Contest!

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*RtWlfW3Tou760Nq3nDv4lw.jpeg)

[![Better Humans](https://miro.medium.com/v2/resize:fill:96:96/1*c_2w6a-GqcYDbmJFO8Frgw.png)](https://medium.com/better-humans?source=post_page---post_publication_info--87b038060522---------------------------------------)

[![Better Humans](https://miro.medium.com/v2/resize:fill:128:128/1*c_2w6a-GqcYDbmJFO8Frgw.png)](https://medium.com/better-humans?source=post_page---post_publication_info--87b038060522---------------------------------------)

[Last published Mar 24, 2025](https://medium.com/better-humans/what-if-you-gave-more-energy-to-the-friendships-that-give-back-ec0428efe3f6?source=post_page---post_publication_info--87b038060522---------------------------------------)

Better Humans is one of the largest and oldest Medium’s publications on self-improvement and personal development. Our goal is to bring you the world’s most helpful writing on human potential.

Science enthusiast, protein designer. PhD in AI.

## Responses (24)

Write a response[What are your thoughts?](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Fmedium.com%2Fbetter-humans%2Fobsidian-tutorial-for-academic-writing-87b038060522&source=---post_responses--87b038060522---------------------respond_sidebar------------------)

```hs
This is a great tutorial, Leo. I think this will have a positive effect on the learning process of students. After all, such online services like Paperspoint in which I, as a student, can get support in writing content and in which professional…
```

14

```hs
This is amazing! Thanks a lot for sharing, I saved it for later 🙏🏼
```

3

## More from Leonardo Castorina and Better Humans

## Recommended from Medium

[

See more recommendations

](https://medium.com/?source=post_page---read_next_recirc--87b038060522---------------------------------------)