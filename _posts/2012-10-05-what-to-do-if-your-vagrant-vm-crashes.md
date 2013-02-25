---
title: What to do if your Vagrant VM crashes
layout: post
tags:
  - development
  - devops
---
 
<p>My vagrant VM crashed. I tried typing <code>vagrant halt</code> but it just tried to "gracefully" shut down the machine, and stayed like that, for a long time.</p>&#13;
<p>What I did was open up the VirtualBox Manager and power off the machine manually.</p>&#13;
<p>However, now when I tried to start my VM again, it started trying to import a new base box to create the virtual machine from scratch, which was not what I wanted. I guess it must have not saved the UUID of my VM back to the <code>.vagrant</code>. Here's what I had to do to fix that.</p>&#13;
<p><!-- more --></p>&#13;
<h3>1. Get VBoxManage running</h3>&#13;
<p>I needed to use the <code>vboxmanage</code> command to find the UUID of the existing virtual machine I wanted to associate with my vagrant directory. To do this I added the path containing <code>vboxmanage.exe</code> to my <code>PATH</code> variable, in my case this was <code>C:\Program Files\Oracle\VirtualBox</code>.</p>&#13;
<h3>2. Find the UUID of my virtual machine</h3>&#13;
<p>I ran <code>vboxmanage list vms</code> to list all VMs by UUID.</p>&#13;
<pre>"vagrant_1349442014" {00b9a111-b18b-4609-becd-f0b77eecab17}&#13;
"vagrant_1349448525" {758d639c-e9ad-48ed-bccb-b4ae423c52ef}</pre>&#13;
<p>And copied the UUID of the one I wanted: <code>00b9a111-b18b-4609-becd-f0b77eecab17</code></p>&#13;
<h3>Update my .vagrant file</h3>&#13;
<pre>vim .vagrant</pre>&#13;
<p>And update it with my new UUID:</p>&#13;
<pre>{"active":{"default":"00b9a111-b18b-4609-becd-f0b77eecab17"}}</pre>&#13;
<h3>Start vagrant again</h3>&#13;
<p><code>vagrant up</code></p>&#13;
<p>Voila!</p> 