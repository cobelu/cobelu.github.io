---
layout: post
title: Rust Footguns - VSC's SNAFU
tags: [rust, software]
featured: false
hidden: false
---

VSC is fantastic... except when it's not.

## New Projects Get Stuck

I found that rust-analyzer often gets stuck for new projects while collecting metadata.
The following command helps fix this issue:

```bash
cargo check --workspace --message-format=json --manifest-path Cargo.toml --all-targets
```

## Workspaces in VSC are Broken

If you use VSC to write Rust (which I suggest you do), you may have issues using with VSC if you utilize workspaces.
Workspaces are a great way to manage multiple Rust projects in a single repo.
Unfortnately, VSC has trouble recognizing them.
Luckily, we can fix it pretty easily.

You will need a workspace-level `.vscode` folder.
In it, create a `settings.json` file, which will be specifically for your project.
Inside, it will look something like this:

```json
{
    "rust-analyzer.linkedProjects": [
        "./project1/Cargo.toml",
        "./project2/Cargo.toml",
        "./project3/Cargo.toml",
        ...
    ]
}
```

And *voilà*... VSC should recognize the workspace projects now!
