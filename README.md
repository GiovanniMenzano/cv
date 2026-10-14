# cv
Repository to automate the build and release of a latex cv/resume.
The source file must be compiled using xelatex engine. When not using GitHub Actions, to generate a PDF you can run "xelatex <filename.tex>" in a terminal.
Furthermore, you can use a site like [Overleaf](https://www.overleaf.com/) to build, edit and preview your document, I did that for first version of the cv.
The tex template is from [Resumake](https://www.resumake.io/), modified with some changes (fonts, color, styles, spacing) and additions (project descriptions, notes section, privacy section) according to my needs.
<br/>

The action has been coded starting from the one written by [Jason Zhang](https://medium.com/@jasonzhang02/automating-resumes-with-overleaf-github-and-github-actions-4f131a333939), changed in order to handle multiple pages pdf, multiple cv (in my case I have the Italian and English one) and a few minor changes to update it.
The Github action basically does the following:
- imports a couple of standard actions, like checkout@v3 to checkout my repository in the container where it's installed and upload-artifact@v4 to have a copy of the pdf in the workflow and be able to use it later;
- imports xu-cheng/latex-action@4.1.0, customized to use xelatex engine, to actually compile my tex files;
- generates release dates and timestamps with the system `date` command, using the Europe/Rome time zone;
- imports softprops/action-gh-release@v3.0.3 to create a release and upload my pdf files to it;
- installs Poppler and converts the English CV into PNG previews at 225 DPI with `pdftoppm`, keeping the numbered filenames used below;
- finally it commits the preview images only when they have changed, then pushes back to the branch with Git.

### Workflow dependency changes

The following dependencies were replaced to keep the workflow simpler:

- [`nanzm/get-time-action`](https://github.com/nanzm/get-time-action) was replaced with the system `date` command. One step now generates both release timestamps and dates, using `Europe/Rome` to account for daylight saving time.
- [`ad-m/github-push-action`](https://github.com/ad-m/github-push-action) was replaced with `git push`. My workflow only pushed to its current branch, no need for external pipelines.
- Ghostscript and ImageMagick were replaced with Poppler's `pdftoppm` for preview image generation. Doing this I also avoided the ImageMagick policy changes.

`actions/upload-artifact` was also updated from `v3` to `v4` after GitHub retired `v3`.
<br/>

![](https://github.com/GiovanniMenzano/cv/blob/main/cv_preview_0.png)
![](https://github.com/GiovanniMenzano/cv/blob/main/cv_preview_1.png)
