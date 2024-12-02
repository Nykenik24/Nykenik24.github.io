---
title: "Welcome to my blog!"
description: "Home."
---

```lua
function AboutMe() -- About me
    print([[
        I like doing little games and i'm learning game developing as a hobby. 
        I develop games in lua with Love2d (https://love2d.org), 
        and don't have intention of making commercial games (for now).
    ]])
    -- btw, i am from spain
end

function ProjectsAndGames() -- Projects and Games
    return { --all projects and games
        gauntlet_of_ageon = 'I am working in a dungeon crawler, roguelike game called "Gauntlet of Ageon".',
        --more info about gauntlet of ageon in projects/gauntlet_of_ageon/posts/the_game
    }
end

print("Note: No, posts are not written in lua")
AboutMe()
ProjectsAndGames()
```
{{< figure
    src="images/small_rice.png"
    alt="Photo of my desktop"
    caption="Photo of my desktop. My OS is [Archcraft](https://archcraft.io/)"
>}}

```lua
print([[
    In the footer you have links to social media and github account.
    You can also check blog posts and projects.
]])
print([[
    All the blog was made with Hugo static website framework (https://gohugo.io) with the
    Hugo congo theme.
]])
```

