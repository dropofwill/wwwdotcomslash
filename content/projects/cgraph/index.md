+++
title = "C-Graph"
template = "project.html"

[extra]
subtitle = "interactive data-viz"
hero_img = "cgraph-hero.png"
description = "A function call graph visualizer for C"

role = "Sole frontend developer" 
tags = [ "Frontend", "Data Viz" ]
tech = [ "Node", "D3.js", "Browserify", "SVG" ]

links = [
    { title = "C-Graph", href = "http://cgraph.herokuapp.com" },
    { title = "Github", href = "https://github.com/brendan-w/cgraph" }
]

team = [ 
    { name = "Brendan Whitfield", link = "https://github.com/brendan-w/" }
]
+++

C-Graph takes a given Github repo, extracts the C files, and generates a function call graph. It then displays this as a force directed graph on the right and a panel of code on the left. This allows programmers to work their way through a code base as it would be executed (network) instead of how it is written (linear).

[More details available in this post](@/posts/c-graph-a-new-tool-to-grok-c-source-code.md)
