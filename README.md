# LaTeX Slides

Here I store my [LaTeX](https://en.wikipedia.org/wiki/LaTeX) template for [beamer](https://en.wikipedia.org/wiki/Beamer_%28LaTeX%29) slides. It is loosely based on the corporate design of the University of Science and Technology of China (<a href="http://en.wikipedia.org/wiki/University_of_Science_and_Technology_of_China">USTC</a>) [中国科学技术大学].

## Usage

1. [download](https://github.com/thomasWeise/latexSlides/archive/master.zip) the template
2. edit `slides.tex`
3. in order to produce a pdf of your slides, under Linux run
  1. `./scripts/latex.sh slides evince` if you are using `eps` figures
  2. `./scripts/pdflatex.sh slides evince` if you are using `pdf` figures
  3. `./scripts/xelatex.sh slides evince` if you have Chinese text
  
## Available Commands

### Put Objects at Specific Locations

Sometimes we want to locate stuff at specific positions on a slide. For this purpose, the following commands are used, which all operate on a `x-y` coordinate system where `x=0, y=0` is the top-left corner of the slide and `x=1, y=1` is the bottom-right corner.

1. `\locate{when}{what}{x}{y}` position the content (`what`) at the specified `x-y` coordinates. If `when` is not empty, wrap everything in an `\only<when>{...}`, i.e., only display something at the specified sub-slide id range. You may put an `\includegraphics` as contents.
2. `\locateWithCaption{when}{what}{caption}{x}{y}{width}` locate the content of `what` at the specified `x-y` coordinates. Put a `figure`-like `caption` below it. Reserve the given `width` (between `0` and `1`, relative to slide width) for everything. The `width` is reserved to know how to break the caption if it is longer than the contents (`what`).


### Citation

1. `\citep{ref}` cite reference `ref` by number
2. `\scitep{ref}` cite reference `ref` by number, pre-pend non-breakable space. For use in text, like `bla bla blablabla\scitep{ref}`
3. `\citet{ref}` cite reference `ref` by author names followed by number
4. `\Citet{ref}` cite reference `ref` by author names followed by number at beginning of sections (make first character uppercase)
5. `\citete{authorRef}{refs}` cite references `refs` by number, but pre-pend the author names of reference `authorRef`. This is useful if a group of authors has produced several works, but the author order changes in these works.
6. `\Citete{authorRef}{refs}` like `\citete{authorRef}{refs}`, but capitalize first character.

### Chinese

Include chinese text with the command `\zh{chinese text}`.