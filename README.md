# LaTeX Slides

Here I store my [LaTeX](https://en.wikipedia.org/wiki/LaTeX) template for [beamer](https://en.wikipedia.org/wiki/Beamer_%28LaTeX%29) slides. It is loosely based on the corporate design of the University of Science and Technology of China (<a href="http://en.wikipedia.org/wiki/University_of_Science_and_Technology_of_China">USTC</a>) [中国科学技术大学].

## Usage

1. [download](https://github.com/thomasWeise/latexSlides/archive/master.zip) the template
2. edit `slides.tex`
3. in order to produce a pdf of your slides, under Linux run
  1. `./scripts/latex.sh slides evince` if you are using `eps` figures
  2. `./scripts/pdflatex.sh slides evince` if you are using `pdf` figures
  