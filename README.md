# marktex
Parses a restricted set of Markdown marking into Latex, plus some special extensions designed to be useful when writing a math lesson in Latex.

# Usage

The command below will convert your Markdown R - like syntax file to a pdf called "my_document", while cleaning LaTeX temporary files in the process (-c)

```bash
marktex -o my_document.pdf -c final_version.Rmd
```

# Syntax

Almost all Markdown is supported, with the exception of Hyperlinks right now (I just don't need them right now).
There is some limitations for lists : sub-lits are not yet implemented, and lists must be isolated by newlines from regular text.

Also, there is some special shortcut syntax, which I plan to organize better, so you can personalize it easily with some kind of conf file.
Anyway, here it is :

```latex
>(Linearity of summations)
Let $(u_n)$ and $(v_n)$ be two series, and $\lambda$ and $\mu$ be two reals, then
$$ \sum^{+\infty}_{n=0}(\lambda u_n + \mu v_n) = \lambda \sum^{+\infty}_{n=0} u_n + \mu \sum^{+\infty}_{n=0} v_n $$

[]
```

As you can see, `>(Title)` at the begining of a line means "begin a proposition with Title as its name". Then the content follow, and you must _close_ your proposition with []

The syntax is exactly the same for theorems, etc. except that :

    - Definitions uses `:(Title)`
    - Theorems uses `~(Title)`
    - Lemmas uses `>- ` WITHOUT a title
    - Proofs uses `¤`, without a title too. There must also be a whitespace after the `¤`.
    
    
A new chapter can be started using :
```latex
3) Pythagoras
=============
```

This will restart theorem/definition/proposition counters, and create a nice, big chapter title.
    
Also, you can use `þ` as a shortcut in math mode to say : `\displaystyle`.
You can delimitate a LaTeX only zone (almost no parsing) with `ł [you text here] ł`

Also, even when out of math mode, you can use `1^{st}` to put some text in superscript. Of course, for a single char, `3^d` will also work for instance.

Finally, you can add comments (which can be removed from the PDF simply by passing the `--no-comments` option) by delimiting text with `@@ text @@`.

Proofs can also be disabled by a command-line option.
