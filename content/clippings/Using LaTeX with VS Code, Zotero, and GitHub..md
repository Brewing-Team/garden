---
title: "Using LaTeX with VS Code, Zotero, and GitHub."
source: "https://www.reddit.com/r/LaTeX/comments/10hrwd7/using_latex_with_vs_code_zotero_and_github/?show=original"
author:
  - "[[AcanthisittaMobile72]]"
published: 2023-01-21
created: 2025-10-15
description:
tags:
  - "clippings"
---
Hi Everyone,

After using online LaTeX editors such as Papeeria and Overleaf, I finally reach the bottleneck and needed to install it in my local machine. This enables me to work in collaboration with others using Zotero as bibliography management.

Here's my checklist about everything that I need to install in order to use LaTeX effectively with VS Code, Zotero and GitHub:

1. A LaTeX distribution: TeX Live is a widely used distribution that includes all of the necessary programs and files to typeset LaTeX documents.
2. A text editor: VS Code is a popular choice among LaTeX users, and it has a built-in extension that provides rich LaTeX support.
3. LaTeX Workshop Extension: An extension for VS Code that provides rich LaTeX support, such as autocompletion, linting, and building.
4. Git: A version control system that allows you to collaborate with others on the same LaTeX project.
5. GitHub Extension: An extension for VS Code that allows you to connect to GitHub and collaborate on LaTeX projects with others.
6. Zotero: A reference management software that allows you to store and organize your bibliographic references and citations, and can be integrated with LaTeX.
7. Zotero Connector: A browser extension that allows you to save references from webpages to your Zotero library.
8. LaTeX-Zotero-Integration package: A package that allows you to insert citations from your Zotero library into your LaTeX documents and automatically generate a bibliography. For VS Code: [**Citation Picker for Zotero**](https://marketplace.visualstudio.com/items?itemName=mblode.zotero)**. Other editors:** [**https://retorque.re/zotero-better-bibtex/citing/cayw/**](https://retorque.re/zotero-better-bibtex/citing/cayw/)
9. **For Windows,** install a [full Perl distribution](https://www.perl.org/get.html) (such as [Strawberry Perl](https://strawberryperl.com/)) and put it in your PATH, because the VS Code LaTeX extension uses `latexmk` by default, which is a Perl script. Credit to: [delta\_p\_delta\_x](https://www.reddit.com/user/delta_p_delta_x/) & [TUG](https://tug.org/texlive/windows.html#perl:~:text=Therefore%2C%20if%20you%20need%20to%20run%20other%20Perl%20scripts%20and%20the%20included%20Perl%20does%20not%20have%20all%20the%20modules%2C%20you%20need%20to%20install%20a%20full%20Perl%20distribution.).
10. CTAN (Comprehensive TeX Archive Network) is a vast collection of TeX-related resources that includes a wide variety of LaTeX packages, styles, and fonts.

Have I got everything covered or am I still missing some pieces?

---

## Comments

> **AcanthisittaMobile72** • [1 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5a7hz4/) •
> 
> On point 10, I meant for other LaTeX distribution like MacTex or MikTex if needed be.

> **GatesOlive** • [1 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5alrem/) •
> 
> How do you improve compilation and rendering times? In vs code with latex workshop I get 15 to 30 seconds of compiling and rendering while in the terminal it's too long if it takes 2 seconds
> 
> > **M3GT2** • [6 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5asukm/) •
> > 
> > This is because LaTeX Workshop runs more than one command. You can customize the build chain with recipes.
> > 
> > **delta\_p\_delta\_x** • [1 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5cr8lw/) •
> > 
> > Un-ironically: move to Linux or macOS. LaTeX on Windows is just horribly slow (~10-15x slowdown compared to Linux on the same machine, using the same distribution (MiKTeX)).
> > 
> > > **GatesOlive** • [1 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5crudi/) •
> > > 
> > > I'm already on Linux, but thanks!
> > > 
> > > > **AcanthisittaMobile72** • [1 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5djidv/) •
> > > > 
> > > > Wait what? You're already using LaTeX in VS Code on Linux and still get slow compiling and rendering? That news to me, which distro are you on if you don't mind me asking?
> > > > 
> > > > > **GatesOlive** • [1 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5djm4e/) •
> > > > > 
> > > > > Kubuntu 20.04

> **delta\_p\_delta\_x** • [9 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5ahwxm/) •
> 
> Perfect. This is exactly my workflow for LaTeX on VS Code, and it works amazingly.
> 
> If you're on Windows, make sure you grab a Perl distribution (such as [Strawberry Perl](https://strawberryperl.com/)) and put it in your PATH, because the VS Code LaTeX extension uses `latexmk` by default, which is a Perl script.
> 
> If you use MiKTeX, then step 9 is unnecessary (provided you configure MiKTeX properly when installing to automatically install missing packages).
> 
> > **Different-Thinker** • [2 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5b9gie/) •
> > 
> > You can also get latexindent in a Docker image, if you don’t want to deal with the hassle and environment variables of a Perl distribution on your computer.
> > 
> > > **\[deleted\]** • [2 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5boiq0/) •
> > > 
> > > At that point, wouldn't you rather use WSL? Setting up docker just to run a Perl script seems unnecessarily complicated.
> > > 
> > > > **Different-Thinker** • [2 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5dgsy1/) •
> > > > 
> > > > Yeah, I already had docker set up so it was just easier for me to go that route.
> 
> **AcanthisittaMobile72** • [1 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5ak8rn/) •
> 
> I choose Tex Live instead of MiKTeX, do I still need to get the Perl distribution?
> 
> > **delta\_p\_delta\_x** • [1 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5alrdi/) •
> > 
> > According to the TUG, [yes](https://tug.org/texlive/windows.html#perl:~:text=Therefore%2C%20if%20you%20need%20to%20run%20other%20Perl%20scripts%20and%20the%20included%20Perl%20does%20not%20have%20all%20the%20modules%2C%20you%20need%20to%20install%20a%20full%20Perl%20distribution.).
> > 
> > > **AcanthisittaMobile72** • [1 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5aox1p/) •
> > > 
> > > Thanks, I opted the strawberry perl since it's open-source compared to the commercial + community ActiveState Perl. I take that, adding perl to PATH will be the same as other application in Windows yes?
> > > 
> > > > **delta\_p\_delta\_x** • [2 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5ar0lh/) •
> > > > 
> > > > Presumably, yes. If I recall correctly, the installer prompts you for the option to add the binary to PATH, too.
> > > > 
> > > > > **AcanthisittaMobile72** • [1 points](https://reddit.com/r/LaTeX/comments/10hrwd7/comment/j5aseb7/) •
> > > > > 
> > > > > Awesome, thanks for the heads up!