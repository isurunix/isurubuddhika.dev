---
title: "Writing my resume in Typst"
date: 2026-01-02T16:16:00+05:30
draft: false,
categories: ["general"]
tags: ["typst", "resume", "rendercv", "cv"]
showShareButtons: true
showBreadcrumbs: true
---

For a while, I have been wanting to maintain my CV/Resume in a simple text format, which allows me to version control it and
maintain it easily.  
I have been trying several things, like using markdown to PDF converters together with GitHub actions, and I recently tried creating.
My own markdown to PDF resume generator supporting live preview and predefined themes.  
But somehow none of these exercises gave me the maintainable resume/CV I was aiming for.

And that is when I stumbled upon [RenderCV](https://news.ycombinator.com/item?id=46344616) on HN. I have fiddled with [Typst](https://typst.app/) way earlier while looking for LaTeX alternatives, and at that I didn't pay much attention (at that time I was looking at it to write a paper which I had no intention of writing). But looking at RenderCV and its usage of Typst had me asking the question, Why don't I write my CV/resume in Typst. And since I was actually looking at staying away from fancy, colorful themed templates and creating something simpler, yet soothing to the eye it seems to a good decision.
So with that in mind, I started moving my CV to a Typst file.

I decided to start with Typst web app since I wanted to experiment and find out what works for me and to be honest, it was quite easier than I assumed. I thought there would be a steeper learning curve where I would have to learn Typst syntax, and it would take at least a few days to get it up to a working template. But it seems the typst documentation is pretty neat, and it didn't take that long for me to come up with something that works for me.

I had to look at the documentation and even took some inspiration from a few existing templates out there (kudos to [@mattrighetti](https://github.com/mattrighetti) for the the top [linkBar](https://typst.app/project/rhCQsMr64hPuS8ttVjKWOm) implementation), and finally, I managed to have something that seems nice.  
But I have to say that the code/template is not neatly organized, or might not be used in the way Typst was expected to be used. But for the time being, it feels like a workable solution. I have a separate template for all different reusable code blocks/functions, which helps me to keep my main file clutter-free and more focused on the actual content of the CV, and this would probably allow me to try out different theming options and templates in the future.

And if you are wondering why I didn't simply use RenderCV and have it as a simple YAML file, well, I did feel like it had too many dependencies to have. While it's a great piece of software, I wanted to keep things as simple as possible. So instead of that I choose to go with pure typst. Maybe I would give RenderCV a try in the future, but I feel like I'd be sticking with my barebones typst template for a while.

So finally, I moved everything from Typst webapp to a git repo so I can maintain it offline, and my next action would be to come up with a GitHub action so I can automatically build the PDF on each change. I already have a few actions under my radar and will probably be implementing them next. But for now, all the content is in Git, and I can locally render it into a PDF. And I can simply edit and render it locally with VS Code with the help of the Tinymist Typst extension.

If you are interested in giving it a try or adopting Typst for you resume you can simply clone my repo at [github.com/isurunix/resume](https://github.com/isurunix/resume) and start hacking. Add the below configuration to your workspace or user settings to make sure the fonts are rendered correctly.

```json
{
    // other settings

    "tinymist.fontPaths": [
        "${workspaceFolder}/fonts"
    ]
}
```

