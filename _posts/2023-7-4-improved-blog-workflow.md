---
layout: post
title: Improved Blog Workflow
---

Since starting the blog nearly 2 months ago, I've used the following setup:
[![Old Blog Workflow]({{ site.baseurl }}/images/old_blog_workflow.jpeg "Old Blog Workflow")]({{ site.baseurl }}/improved-blog-workflow/)

- RDP from iPad to local Windows machine with Visual Studio Code
- Open remote folder via SSH on local Raspberry Pi running Ubuntu
- Blog files are added/edited
- Stage, commit and push up to Github
- Action triggered to rebuild and deploy the blog in [Github Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages)
  
While this may appear convoluted, it works great and allows everything to be done from Visual Studio Code.

I could've instead used WSL (Windows Subsystem for Linux) and pushed to Github from the Windows machine, however, as a project I wanted to build the blog specifically on my Raspberry Pi, to add to the extensive functionality it already provides (LED clock coloured based on room temperature, humidity/pressure monitoring, console jumphost for physical prod and lab firewalls, Telegraf ICMP/SSH/SNMP monitoring for virtual lab devices in EVE-NG or CML, etc).

But since discovering [Visual Studio Code for the Web](https://code.visualstudio.com/docs/editor/vscode-web) - [vscode.dev](https://vscode.dev/), things have become a lot easier. All the functionality* required from Visual Studio Code for a simple blog works great in the local browser. I can drag and drop files such as images straight into their respective folder, changes are auto saved + staged, and I can commit + push with the single press of a button (with the ability to add a commit message!) - there is no longer any need for a terminal:

![New Blog Workflow]({{ site.baseurl }}/images/new_blog_workflow.jpeg "New Blog Workflow")

![VSC Web Push]({{ site.baseurl }}/images/vscweb-push.jpeg "VSC Web Push")

* Not quite ALL - Code Spell Checker [extension](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) is not yet available for VSC on the web and I was not able to find an alternative that is. 
 
That said, the improvements are worth this tradeoff and I can live with copy/pasting into another app to spell check before I commit+push, at least until a compatible extension emerges.

Next steps will be testing [VS Code Server](https://code.visualstudio.com/docs/remote/vscode-server) and [Tunnels](https://code.visualstudio.com/docs/remote/tunnels) to evaluate the feasibility of extending this new workflow to other use cases/projects, where code needs to be run/tested/saved/deployed in a local environment before being pushed up to Github. I plan to then compare this with [Github Codespaces](https://github.com/features/codespaces), to gain some first hand experience of the usability advantages/limitations, and refine my setup accordingly.

In the meantime I will enjoy the new blog workflow, and will update here once I'm aware of a compatible spell checker extension, and if/when the workflow changes.