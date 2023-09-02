---
layout: post
title: Visual Studio Code Server Tunnels
---

Following on from the previous [post]({{site.baseurl}}/improved-blog-workflow/), I have been experimenting with VS Code Tunnels:
[![vsc-tunnels-arch](https://code.visualstudio.com/assets/docs/remote/vscode-server/server-arch-latest.png)]({{site.baseurl}}/vs-code-tunnels)
*from [code.visualstudio.com](https://code.visualstudio.com/docs/remote/vscode-server)*

It felt like a good time to push forward with this - given the increasing popularity of VS Code:
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr"></p>
<a href="https://twitter.com/driscollis/status/1696897522122326159"></a>
</blockquote> <script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

## Use case
I wanted to start using the [CML](https://www.cisco.com/c/en/us/products/cloud-systems-management/modeling-labs/index.html#~overview) (Cisco Modeling Labs) [API](https://developer.cisco.com/docs/virl2-client/), in order to build and interact with labs, using my Raspberry Pi, without using an intermediary Windows host to run VS Code.

By setting up a tunnel, I get the benefits of [Visual Studio Code for the Web](https://code.visualstudio.com/docs/editor/vscode-web), while working directly within a local folder on the Pi, with a responsive terminal, in order to seamlessly test modified code between changes.

## Setup steps
- Install VS Code on Raspberry Pi [link](https://code.visualstudio.com/docs/setup/raspberry-pi)

```
$ sudo apt install code
```

- disable telemetry (optional)

```
$ code --telemetry | grep -c true
416

$ sudo sed -i 's/true/false/g' /usr/share/code/resources/app/telemetry-core.json
$ sudo sed -i 's/true/false/g' /usr/share/code/resources/app/telemetry-extensions.json

$ code --telemetry | grep -c true
0
```

Don't forget to do the same on the client side [link](https://code.visualstudio.com/docs/getstarted/telemetry#_disable-telemetry-reporting)

- start tunnel (accepting license terms for first use)

```
$ code tunnel --accept-server-license-terms

* Visual Studio Code Server
*
* By using the software, you agree to
* the Visual Studio Code Server License Terms (https://aka.ms/vscode-server-license) and
* the Microsoft Privacy Statement (https://privacy.microsoft.com/en-US/privacystatement).
*
To grant access to the server, please log into https://github.com/login/device and use code XXXX-XXXX
```

(Bear in mind if you are running 'code tunnel' over an SSH session, the tunnel will be dependent on that session, so you may wish to run in background (append & (not on first usage as you need the device code and tunnel URL)) or over a screen/tmux session to remove the dependency on the SSH session)

- enter device code at github URL

```
[2023-09-02 16:23:11] info Creating tunnel with the name: raspberrypi

Open this link in your browser https://vscode.dev/tunnel/raspberrypi/home/pi/cml/virl
```

- Open vscode.dev link

```
[2023-09-02 16:24:53] info [tunnels::connections::relay_tunnel_host] Opened new client on channel 2
[2023-09-02 16:24:53] info [russh::server] wrote id
[2023-09-02 16:24:53] info [russh::server] read other id
[2023-09-02 16:24:53] info [russh::server] session is running
[2023-09-02 16:24:53] info [rpc.0] Checking /home/XX/.vscode/cli/servers/Stable-xxxx/log.txt and /home/pi/.vscode/cli/servers/Stable-xxxx/pid.txt for a running server...
[2023-09-02 16:25:13] info [rpc.0] Downloading Visual Studio Code server -> /tmp/.tmpgVb1UQ/vscode-server-linux-arm64.tar.gz
[2023-09-02 16:25:23] info [rpc.0] Starting server...
[2023-09-02 16:25:23] info [rpc.0] Server started
[2023-09-02 16:36:06] info [rpc.0] Disposed of connection to running server.
```

- Develop
![vscode-web-tunnel]({{ site.baseurl }}/images/vscodeweb-tunnel.jpeg "VS Code Web Tunnel screenshot")

## Benefits/Tradeoffs
An SSH remote session would be highly preferred over the tunnel traffic traversing a Microsoft proxy, however VS Code for the Web does not currently have this option. So, in the absence of a full local GUI install, a tunnel provides a compromise - giving the benefit of a full install, with the security/performance tradeoff of an external proxy. 

One big benefit of using tunnels vs connecting directly to a Github repo, is that extensions are installed on the server, removing the previous limitation of only web compatible extensions. This means I now have a working spell checker on Visual Studio Code for the Web, which is great - I have updated the previous [post]({{ site.baseurl }}/improved-blog-workflow/).

## Conclusion
A VS Code Tunnel provides an easy, convenient way to develop on remote, or even local (CLI only) hosts, for scenarios where SSH remote host is not an option, such as Visual Studio Code for the Web.

This is the most convenient option for the iPad Pro for now, in the absence of either a native VS Code iPadOS app, or SSH remote host option on VS Code for the Web.

However, if you have access to a host with a full local GUI install of VS Code, and you can connect via SSH to the machine you want to work on, then using the first host as a jumpbox removes the security/performance tradeoffs of a tunnel. In my particular case, there is no noticeable performance impact from RDP'ing to a local Windows machine with a full VS Code install and using SSH remote host, or from using a tunnel with the Web version. But, since some iPad apps (including the Microsoft RDP client), are not able to be stretched to complete full screen on Studio Display with Stage Manager - using Safari with the Web version for complete full screen on the larger display provides the nicest user experience.

I plan to compare this with [Github Codespaces](https://github.com/features/codespaces) at some point and write up in a future post.