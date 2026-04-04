---
description: Mirror's unofficial Edgegap Hosting Plugin documentation.
---

# Edgegap's dediziertes Spielserver-Hosting – Plugin-Anleitung

Edgegap helps you build and launch a dedicated game server in the cloud directly from Unity’s editor, without almost any coding or Linux/Cloud usage whatsoever. Which helps make game server hosting easy!

_Thanks to Edgegap’s dedicated game server hosting plugin for Unity, Mirror users get 1.5 vCPU of cloud hosting for free with Edgegap’s free trial!_

## Overview

Integration of Edgegap is simple and takes a few minutes with 3 basics steps:

1. Installing Unity dependencies & Docker
2. Installing the Unity plugin & creating a free account on [Edgegap](https://app.edgegap.com/)
3. Configuring, building & pushing the server to Edgegap

Edgegap’s plugin walks you, step-by-step, making it the easiest way to add dedicated game server in Unity.

## Setting Up your Project

{% hint style="warning" %}
If you are installing a new project, rather than installing the latest version, we strongly recommend using the “LTS” (Long Term Service) version of Unity for your project, i.e., Unity 6.0 (6000.0.60f1) as of writing. This ensures compatibility with tools & services, and long-term support of Unity’s version for your projects.
{% endhint %}

**1. Installing Linux Build Support**

From your **Unity Hub**, select **Installs**, select the **Manage** icon next to the Unity version you intend to use in your project and click **Add Modules**:

Make sure to install all three of Unity’s Linux Build Support Modules. Namely:

* Linux Build Support (IL2CPP), Linux Build Support (Mono), Linux Dedicated Server Build Support,

Additionally, depending on your target platform OS, you will need to add:

* **Windows**: Windows Build Support (Mono)
* **Mac**: Mac Dedicated Build Support (IL2CPP) and Mac Dedicated Server Build Support
* **WebGL**: Web Build Support

{% hint style="info" %}
For users with new projects, which modules to add will be prompted when selecting which version to install. Make sure to add it there. However, you can return at any time to add them as shown above.
{% endhint %}

**2. Installing Docker**

Edgegap uses containers, which is a virtualization that ensures to can run on any hardware, anywhere in the world.

Any containerization tool should work, but the easiest is to use Docker Desktop:

[https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

Simply download it, install it, restart the dev machine, then open it (if it doesn’t open automatically at boot time. Then run it in the background.

## Installing the Unity plugin

From the top navigation menu in Unity, select **Window**, then **Package Manager**.

Within the Package Manager, click on the "+" icon, then select **Add Project from Git**.

Paste Edgegap's Unity plugin URL:

<[https://github.com/edgegap/edgegap-unity-plugin.git#partner/mirror-source](https://github.com/edgegap/edgegap-unity-plugin.git#partner/mirror-source)>

Select **Install**.

That’s it!

From the top navigation bar, select **Tools** and then open the plugin by clicking on **Edgegap Server Hosting**.

The plugin automatically opens up. Select **Sign in with Edgegap** to start the process of creating an account (or sign-in to sync with the platform, for users with active accounts).

## Create a Free Account on Edgegap

Signing up to Edgegap is easy and free. Use your own **Google** or **GitHub** account, or sign-up with an **email**.

You are now asked to name **Your Organization**.

Automatically, the **OneClick Token Create Successfully** screen appears. This is your token (blurred here). Simply copy it by clicking on the clipboard icon.

{% hint style="warning" %}
Do not share your token with anyone or on public channels like Discord, as they could deploy game servers on your behalf!
{% endhint %}

## Configuring, building & pushing the server to Edgegap

**1. Validate your Token**

Return to Unity and paste the token in the field under **1. Connect your Edgegap Account**. Then, select **Validate Token**.

**2. Building your Game Server**

After verifying successfully, you optionally can make sure that you have the Linux Server dependencies by clicking on **Install**.

Then, select **Edit Settings** to make sure the game scenes you want to include are included.

Under **Linux Server**, make sure the scenes are listed. If not, select **Open Scene List** and add them manually.

Additionally, doublecheck that your build set up. Specifically, select **Network Manager** from your project’s hierarchy, and the under **Network Manager**, ensure

1. Under **Configuration**, that **Don’t Destroy on Load** is selected (i.e., the ✔)
2. **Headless Start Mode** is set to **Auto Start Server**

Return to the plugin and select **Build Server** to start the build process. You should see “Build succeeded” in green when complete.

**3. Containerize your Game Server**

First, make sure Docker is running by selecting **Validate**. You should see “Docker is running” in green.

While you may want to change the image name, build path, and tags in the future, we recommend skipping this entirely and select **Containerize with Docker** button to start the containerization process.

After a short wait, you should see “Containerization succeeded” in green.

**4. (Optional) Test your Server Locally**

Optionally, you can test your container locally by selecting **Deploy Local Container**. You may configure the server image tag, and Docker run parameters, but we recommend skipping this initially.

If it succeeds, you should see “Container deployed successfully” in green.

The container should be visible within the “Container” tab in Docker Desktop.

**5. Upload to Edgegap**

Now we’ll upload the game server to Edgegap’s registry so they can deploy it to their cloud network.

Application name, server image name and server image tag are all pre-filled. While all can be edited, we suggest to keep things as-is for now.

Select **Upload Image and Create App Version** button, which automatically uploads the build to Edgegap’s platform.

{% hint style="info" %}
Older images on your dev machine can be uploaded. Find the docker image name and tag in Docker Desktop under images tab.
{% endhint %}

After a bit of loading, a new web browser will open. This is your application’s **Version** parameters. You can customize the version’s name, resources parameters, and more.

For now, click on **Submit** to create your version.

{% hint style="info" %}
Resources optimization is key to limit overall cloud usage. Edgegap offers vCPU fractioning, which means you can reduce your game server down to ¼ of a vCPU. When ready, make sure to check out Edgegap’s [analytics](https://app.edgegap.com/analytics/dashboards/list) and recommended [server builds optimization](https://docs.edgegap.com/learn/unity-games/getting-started-with-servers#optimize-server-builds) strategy
{% endhint %}

Then, the **Create Port** screen appears. Here you can change the **port**, and the **protocol type**. If you use KCPTransport the default port of 7777 and UDP.

{% hint style="info" %}
If you are working on a WebGL project, then use 7778 and WS protocol. For other transports, select the corresponding protocol an port configured in Network Manager in your server build.
{% endhint %}

Select **Submit** to create your deployment.

**6. Deploy to Cloud**

The final step is to select which version to deploy to Edgegap’s cloud network. Here, your latest application will be preset but can be changed. You must manually select **Application Version** by simply clicking on the drop down (the ▼ on the right) and the latest versions will be shown, here in the image highlighted in green:

Once selected, simply select **Deploy to Cloud**.

This automatically opens your deployments’ page on the Edgegap’s platform. After a few seconds, the deployment will change from “deploying” to “ready”.

Once that’s done, click on the deployment. This opens up the **Deployment Details** page. Scroll down and make sure to note the **Host URL** alongside the **External Port**.

Copy the Host URL using the clipboard.

{% hint style="info" %}
While internal ports for the server process are defined as part of app version, external ports are assigned at random once a deployment is created, so that a potential malicious party (hacker) is slowed down and detected before they can cause damage.
{% endhint %}

Back in Unity, select the **Network Manager** from your project’s hierarchy.

Within the **Inspect Tab**, make sure to set:

1. Paste the **Host’s URL** from the deployment to the **Network Address**
2. Replace the default **Port** (usually 7777) to the **External Port** from the deployment

Then launch the scene in Unity Editor, and test the project:

{% hint style="success" %}
It's important to understand the magic that is happening here.

Not only can you launch a game server with Two Clicks now.

You can even launch thousands of servers with another click on Edgegap's website! 🤩
{% endhint %}

To reduce costs (if you are paying), you can press **Stop Last Deployment** in the plugin once you are done.

## Troubleshooting Connection Issues

If your Server Status says **Ready** but you can't seem to connect, try this:

* On the Edgegap website, go to Deployments -> select your Deployment -> select **Container Logs**, check the log files to see if your game server launched or if there are issues.
* If it says "exec user process caused: no such file or directory": this can happen if you pushed an ARM build to Edgegap's x86 infrastructure. We already updated the plugin to properly cross compile from ARM so this generally should not happen anymore.
* If everything seems fine but you still can't connect, please talk to an Edgegap employee in the Mirror Discord's **#edgegap** channel.
