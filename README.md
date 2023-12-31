# Multi-school SoP
A $\LaTeX$ template for writing statement-of-purpose for many schools at the same time.

Note that this template is tested with a Linux system (including WSL) with TeX Live.
It needs Perl 5 (preinstalled on most Linux distributions) and `pdflatex` to work.

You don't need any knowledge on Perl to use this template.

You are called "Nikola Tesla" in the template,
and you're responsible to change it to your name.

The template has the following pre-built features: 

- Use `\fullcite` to include a citation in the body of the document,
- Palatino font,
- Based on `article` but has smaller page margins.

You are encouraged to change it to fit your own preferences.

## Motivation

It is pure pain to write $n$ different documents for $n$ schools,
where:

- Most of the contents are the same,
- Every document has a small portion of school-specific content,
- Whenever you want to make some small changes,
  you have to change all $n$ documents.

This template is designed to solve this problem,
and you can even have a PDF contains all school-specific content
(so you can send it to your senpais for review)
and a PDF with no school-specific content.

There will be $n+2$ PDFs generated.

## Build and run

Go to the `src` directory, and run `perl build-sop.pl` to compile the documents.

Currently, the template assumes you're applying to UPenn, UIUC, and U of T.
It compiles to the following files:

```
src/sop-penn.pdf
src/sop-uiuc.pdf
src/sop-uoft.pdf
src/sop-all.pdf
src/sop-null.pdf
```

As the name suggests, `sop-null.pdf` contains no school-specific content,
and `sop-all.pdf` contains all school-specific content.

In `sop.tex`, you can use:

```tex
\ifdefined\includePenn
Replace with UPenn-specific content here
\fi
```

This will only appear in `sop-all.pdf` and `sop-penn.pdf`.

## Adding a new school

You probably want to add more schools, here's how.
Open `build-sop.pl`, and you'll see this line:

```perl
my @schools = qw/Penn Uiuc UofT/;
```

You can add more school names (no whitespace allowed), for instance if you want
to apply to CMU, change it to

```perl
my @schools = qw/Penn Uiuc UofT CMU/;
```

And now you can use `\ifdefined\includeCMU` in `sop.tex`,
and it will only appear in `sop-all.pdf` and `sop-cmu.pdf`.

Note that the bibliography is shared among all schools,
and it will be compiled from the first element in your `@schools` array.
This means you don't want to have citations in your school-specific content,
or it will mess up the bibliography generation.
This is a limitation of the current implementation,
but it is good for compilation speed.
