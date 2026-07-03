---
title: 'emdy.dev'
description: 'A simple Git-first web based Markdown editor'
pubDate: '2026-06-15'
heroImage: '../../assets/emdy-fox1.png'
imgWidth: 250
---

[https://emdy.dev](https://emdy.dev)

emdy was a project born of necessity. I needed a simple Markdown web editor that supported Git natively and did not require a login. A sort of hybrid between Github/Gists, Notion, and Pastebin. Surprisingly enough, nothing seemed to fit the bill quite to the extent I was hoping for. Now, there's Emdy :)

Emdy projects are backed by real Git repos, do not require a login to create/edit/share, and can store other non-Markdown files (and supports custom themes).

## Background

For the past few months, I've been working more and more with LLMs and agents in both coding and personal assistant style tasks. Like many others exploring this space, I had sort of landed on Markdown as being a common ground between myself and these agents. Markdown is great because it is a format that is easy and familiar enough for me to manipulate directly myself and structured and token-efficient enough for LLMs to work with and understand as well. Recently, I started needing to be able to share some of these research documents being created with Claude with my signifcant other, but the question was how? Notion and Google Docs both support Markdown, but when I tried to paste in some of these larger Markdown docs I started running into issues around formatting or internal heading links not working correctly. I know there's also Obsidian, but from what I understand that requires a paid tier in order to sync documents across devices. Pastebin works for quick sharing, but is hard to read and can't be edited easily. I could go on, but you get the idea.

## Enter Emdy

I've been reading and seeing more about the rise of bespoke, customized software recently. Why settle for terminals, IDEs, frameworks, libraries, or any other piece of software that might have rough edges or that don't fit your workflow quite the way you'd like? Frontier models have become great at diving deep into existing codebases and tweaking things or cobbling together entirely new things from existing packages and concepts. Emdy is nothing revolutionary, but it's exactly what *I* was looking for in a workflow, so I built it with the help of Claude Code.

![Gen AI is transforming custom software development](/src/assets/genai-transforming-software.png)

## Coding with Claude

This was the first greenfield project that I've worked on that was pretty much 100% written by Claude with heavy steering from myself. Based on what I've been seeing and reading elsewhere, combined with my own experimentation and trials, I ended up with a system for creating tasks in a backlog and handing them off to Claude Code for work. I only worked in a single Claude Code instance at a time and each line of code was reviewed by me personally. I know and understand Emdy in its entirety and can (and have) worked in the codebase myself as well. It is well maintained and readable. Tech debt was scheduled in as needed to ensure the codebase was still usable from a human perspective at all times.

Emdy consists of a Typescript monorepo using vanilla npm workspaces. The directory and file structure that enables Claude to effectively work in the project is shown below:

* `CLAUDE.md` - Single line file: `@AGENTS.md`
* `AGENTS.md` - Detailed instructions for Claude: description of related doc files (more on that below), task development lifecycle details, monorepo details, styling/code preferences, development/testing guidelines, unit/integration/e2e testing guidance, and hard rules (e.g: do not attempt to commit or deploy changes, tests must pass)

The overall development flow went something like this:

1. Add task to the `docs/TASKS.md` file using a checklist format and a medium level of verbosity based on the task: `* [ ] Add relevant icons to buttons`
2. 