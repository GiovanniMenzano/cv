# cv
Repository to automate the build and release of a latex cv/resume.
The source file must be compiled using xelatex engine. When not using GitHub Actions, to generate a PDF you can run "xelatex <filename.tex>" in a terminal.
Furthermore, you can use a site like [Overleaf](https://www.overleaf.com/) to build, edit and preview your document, I did that for first version of the cv.
The tex template is from [Resumake](https://www.resumake.io/), modified with some changes (fonts, color, styles, spacing) and additions (project descriptions, notes section, privacy section) according to my needs.
<br/>

The action has been coded starting from the one written by [Jason Zhang](https://medium.com/@jasonzhang02/automating-resumes-with-overleaf-github-and-github-actions-4f131a333939), changed in order to handle multiple pages pdf, multiple cv (in my case I have the Italian and English one) and a few minor changes to update it.
The Github action basically does the following:
- imports a couple of standard actions, like checkout@v3 to checkout my repository in the container where it's installed and upload-artifact@v3 to have a copy of the pdf in the workflow and be able to use it later;
- imports xu-cheng/latex-action@v2, customized to use xelatex engine, to actually compile my tex files;
- imports nanzm/get-time-action@v1.1 to use timestamps on files and releases;
- imports softprops/action-gh-release@v1 to create a release and upload my pdf files to it;
- installs ghostscript to be able to use pdf files with ImageMagick and converts my cv into png, so that I can show a preview into my readme file, as you can see below;
- finally it pushes the converted files back to the branch, using ad-m/github-push-action@master.
<br/>

![](https://github.com/GiovanniMenzano/cv/blob/main/cv_preview_0.png)
![](https://github.com/GiovanniMenzano/cv/blob/main/cv_preview_1.png)
