# LaTeX Slides

Here I store my [LaTeX](https://en.wikipedia.org/wiki/LaTeX) template for [beamer](https://en.wikipedia.org/wiki/Beamer_%28LaTeX%29) slides. It is loosely based on the corporate design of the University of Science and Technology of China (<a href="http://en.wikipedia.org/wiki/University_of_Science_and_Technology_of_China">USTC</a>) [中国科学技术大学].

## 1. Usage

1. [download](https://github.com/thomasWeise/latexSlides/archive/master.zip) the template
2. edit `slides.tex`
3. in order to produce a pdf of your slides, under Linux run
  1. `./scripts/latex.sh slides evince` if you are using `eps` figures
  2. `./scripts/pdflatex.sh slides evince` if you are using `pdf` figures
  3. `./scripts/xelatex.sh slides evince` if you have Chinese text (also: produces smaller output than `pdflatex`)
  4. `./scripts/lualatex.sh slides evince` if the above commands fail (LuaLaTeX is slightly better in dealing with memory allocation and stuff)  
  
## 2. Available Commands

### 2.1. Structural Commands

The following structural commands should be used in exactly this order (while `\appendices` and `\printSectionOutlines` are optional).

1. `\startPresentation{optional}` start the presentation and put the `optional` content on the outline slides, if any. After this, your slides should come.
2. `\printSectionOutlines` optional: a section outline should be printed at the beginning of each section
3. `\endPresentation` ends the presentation by putting a goodbye screen and the references
4. `\appendices` starts appendix sections. Maybe you want to have some more slides in store if someone asks questions. Can be left away if there are no appendices.

### 2.2. Put Objects at Specific Locations

Sometimes we want to locate stuff at specific positions on a slide. For this purpose, the following commands are used, which all operate on a `x-y` coordinate system where `x=0, y=0` is the top-left corner of the slide and `x=1, y=1` is the bottom-right corner.

1. `\locate{when}{what}{x}{y}` position the content (`what`) at the specified `x-y` coordinates. If `when` is not empty, wrap everything in an `\only<when>{...}`, i.e., only display something at the specified sub-slide id range. You may put an `\includegraphics` as contents.
2. `\locateWithCaption{when}{what}{caption}{x}{y}{width}` locate the content of `what` at the specified `x-y` coordinates. Put a `figure`-like `caption` below it. Reserve the given `width` (between `0` and `1`, relative to slide width) for everything. The `width` is reserved to know how to break the caption if it is longer than the contents (`what`).
3. `\locateGraphic[ref]{when}{arg}{path}{x}{y}` locate an `\includegraphics[arg]{path}` via `locate{when}{\includegraphics[arg]{path}}{x}{y}`. The optional argument `[ref]` can be a citation (`\citep`) or text describing the image source. It is printed with tiny, gray text in the bottom-left corner of the image (overlapping with the image). Arguments are passed forward as indicated. 
4. `\locateFramedGraphic{when}{arg}{path}{x}{y}` same as `\locateGraphic`, but puts a frame around the graphic.
5. `\locateFramedBox{when}{width}{what}{x}{y}{background}{foreground}` locate a framed box of  the given `width` (relative to the slide width) at coordinates `x-y` at sub-slides `when` (or always, if `when` is empty). The contents of the box are `what`. The box will use `background` as fill color (or white, if `background` is empty). The frame will be in color `foreground` (or blueish, if `foreground` is empty).
6. `\begin{lobateBox}{when}{x}{y}...\end{locateBox}` locate the contents of the environment at the specified `x-y` coordinates. If `when` is not empty, only display at the specified sub-slides.
7. `\begin{scaledBox}{width}{height} ... \end{scaledBox}` an environment which scales its contents to the given `width` and `height`. If `width==!`, then we scale proportionally according to `height`. If `height=!`, then we scale proportionally to `width`.

### 2.3. Listings

1. You can use all the normal commands from package [`listings`](http://ctan.org/pkg/listings).
2. `\begin{listingBlock}[width]{caption}...\end{listingBlock}` place a block with the specified `caption` which is supposed to contain a listing. The `width` can be specified relative to the paper width, if omitted, we use `0.95\paperwidth` as block width.
3. `\codeil[format]{text}` formats `text` as source code (with the optional `format`, which can be any format support by `listings`, such as `Java`, `XML`, `C`, ...)

### 2.4. Citations

1. `\citep{ref}` cite reference `ref` by number
2. `\scitep{ref}` cite reference `ref` by number, pre-pend non-breakable space. For use in text, like `bla bla blablabla\scitep{ref}`
3. `\citet{ref}` cite reference `ref` by author names followed by number
4. `\Citet{ref}` cite reference `ref` by author names followed by number at beginning of sections (make first character uppercase)
5. `\citete{authorRef}{refs}` cite references `refs` by number, but pre-pend the author names of reference `authorRef`. This is useful if a group of authors has produced several works, but the author order changes in these works.
6. `\Citete{authorRef}{refs}` like `\citete{authorRef}{refs}`, but capitalize first character.

### 2.5. Chinese

Include Chinese text with the command `\zh{chinese text}`. You then need to use the XeLaTeX script for compiling. `\zhb{chinese text}` puts the text into an `\mbox{...}`, which prevents line breaks. This makes sense when using Chinese words like university names or other things that should not be broken across lines in an otherwise English text, for instance.