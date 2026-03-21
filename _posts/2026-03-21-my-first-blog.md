---
layout: post
title: "My First Blog Post"
date: 2026-03-21 12:00:00 -0000
categories: welcome
---


# use tmux

```bash
# Start a new tmux session
tmux new -s mysession

# Run your program
./your_program

# Detach with Ctrl+B, then D

# Later, reattach:
tmux attach -t mysession
```