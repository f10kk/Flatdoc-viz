# ![icon](images/flatdoc-viz.png) Flatdoc-viz

## Introduction
**Flatdoc-viz** is a modification of the original [Flatdoc][flatdoc-link], 
seasoned with some bits from the modifications of [Flatdoc][flatdoc-link] used 
for the documentation of [Spark][spark-link], and added ~~hack~~ support for 
[GraphViz][graphviz-link] diagrams using [viz.js][viz-js-link].


Current version: [Flatdoc-viz 1.0 >][download-link]

![email][email-image] [flokk](mailto:key.flokk@gmail.com) |
![contact][contact-image] [google+](https://plus.google.com/u/2/100973429079913209557)

## What is it?
- a collection of javascript/html/css files to render a Markdown document as 
  full page document in a web-browser. 
- a complete package containing everything you need to display the document, 
  without requiring any internet connection.
- a nice rendered version of your Markdown document, with a side-bar showing the
  table of contents, directly usable as user documentation or whatever you can
  think of.
- exactly what you see now.


## Requirements
- A web-browser
- A web-server

The web-server can be very basic, since the only reason is to be able to load 
the markdown file with javascript, which is not enabled when the html file is
loaded directly (using **file://...**).

For example, I used:
```
    python -m http.server 8001
```

My documentation can be then viewed using 
```
    http://localhost:8001/doc.html
```

## Getting Started
You can directly use the provided html document and stylesheet, and replace the 
content of the readme.md with your markdown text. However, you will probably 
need to edit the doc.html to change at least some basic things like the title,
description, and icon. Modify the stylesheet to adapt the color and layout.

To view the rendered version of your Markdown document, you will need to start a
web-server and navigate to the html document used as template (doc.html).

The [Markdown][markdown-link] supported is mainly compatible to the 
[git-flavoured markdown][gfm-link].

Flatdoc-viz, like Flatdoc, use the [marked parser][marked-link], if you want 
to look at the supported markdown features.

For the [GraphViz][graphviz-link] diagrams, you just need to write the diagram 
definition in a code block in your markdown document, delimiting the block with 
triple back-ticks, using **viz** as code style.

Example (code of the diagram shown [further down](#what-did-i-use-viz-js)):

    ``` viz
        digraph G {

            subgraph cluster_0 {
                style=filled;
                color=lightgrey;
                node [style=filled,color=white];
                a0 -> a1 -> a2 -> a3;
                label = "process #1";
            }

            subgraph cluster_1 {
                node [style=filled];
                b0 -> b1 -> b2 -> b3;
                label = "process #2";
                color=blue
            }
            start -> a0;
            start -> b0;
            a1 -> b3;
            b2 -> a3;
            a3 -> a0;
            a3 -> end;
            b3 -> end;

            start [shape=Mdiamond];
            end [shape=Msquare];
        }
    ``` 

## What did I use?
### Flatdoc
This is the bigger part of this package, using some code-bits from the 
modifications done for the [Spark][spark-link] documentation to produce better 
ids for the table of content.

The package include [jquery][jquery-link] in the version used by 
[Flatdoc][flatdoc-link], to be able to use it offline. The Flatdoc project links 
directly to a [jquery online version][jquery-link].

Also, a default theme is included, together with the used fonts, again, to be 
able to have everything rendering offline.

### viz.js
This module is used to display [GraphViz][graphviz-link] diagrams.

Example (from the [viz.js project][viz-js-link]):
``` viz
    digraph G {

        subgraph cluster_0 {
            style=filled;
            color=lightgrey;
            node [style=filled,color=white];
            a0 -> a1 -> a2 -> a3;
            label = "process #1";
        }

        subgraph cluster_1 {
            node [style=filled];
            b0 -> b1 -> b2 -> b3;
            label = "process #2";
            color=blue
        }
        start -> a0;
        start -> b0;
        a1 -> b3;
        b2 -> a3;
        a3 -> a0;
        a3 -> end;
        b3 -> end;

        start [shape=Mdiamond];
        end [shape=Msquare];
    }
``` 

To render the diagram, I tweaked a bit the parser code, adding a highlighter for
**viz** code, and avoiding for this particular kind of code the use of *code* 
html tags, using a simple *div* instead (with the class name, in this case 
**lang-viz**, useful in the stylesheet).
 

[download-link]: http://example.com/download.zip 
[flatdoc-link]:  http://ricostacruz.com/flatdoc
[spark-link]:    http://docs.spark.io
[viz-js-link]:   https://github.com/mdaines/viz.js/
[graphviz-link]: http://graphviz.org/
[markdown-link]: https://daringfireball.net/projects/markdown/
[gfm-link]:      https://help.github.com/articles/github-flavored-markdown
[marked-link]:   https://github.com/chjj/marked
[jquery-link]:   http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js
 
[email-image]:   images/email.png
[contact-image]: images/contact.png