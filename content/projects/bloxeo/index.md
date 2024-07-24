+++
title = "Bloxeo"
template = "project.html"

[extra]
subtitle = "real-time collaboration"
description = "A platform for brainstorming, organizing, and refining ideas in a distributed manner."

hero_img = 'bloxeo-landing-page.png'
images = [ "bloxeo-hero.png" ]

role = "Lead backend developer"
tags = ["Backend", "Collaborative"]
tech = ["NodeJS", "MongoDB", "Redis", "WebSockets"]
links = [
    { "title" = "Bloxeo server github", "href" = "https://github.com/IGME-Research-Studio/bloxeo-server"},
    { "title" = "Bloxeo client github", "href" = "https://github.com/IGME-Research-Studio/bloxeo-client"},
    { "title" = "Bloxeo design deck", "href" = "bloxeo-deck.pdf" },
]
team_name = "Server team"
team = [
    { name = "Eric Kipnis", link = "https://github.com/erickipnis/" },
    { name = "Braxton Frederick", link = "https://github.com/brfrederick/" },
    { name = "Nick Minnoe", link = "https://github.com/nickMinnoe/" },
    { name = "Chad Karon", link = "https://github.com/ckaron0912/" },
    { name = "Isaiah Smith", link = "https://github.com/jordankid93/" },
    { name = "Peter Gyory", link = "https://github.com/petroochio/" }
]

+++

Bloxeo is a web-based collaborative brainstorming application that creates an experience making your creative process not only easier and more fun, but more productive.  Assemble a team and work off of each other’s ideas. Generate ideas into a growing bank of idea blocks. Build on the best ideas to reach that eureka moment.

To achieve this on the backend we built a system that solved many classic collaborative 'multi-player' problems. State synchronization, distributed timers, conflict resolution, handling poor network connections, etc.
