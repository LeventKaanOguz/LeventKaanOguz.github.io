# Using GitHub Pages to Create a Blog

<!--more-->

## Prerequisites

* **GitHub Account:** You can open one from [here](https://github.com). Also, basic GitHub knowledge is recommended but it is not a prerequisite.
* **Hugo Extended Installation:** You should follow the instructions appropiate for your system [here](https://gohugo.io/installation/).
* **A Preffered Choice of Theme:** You can of course build your own theme but it is better to choose one from [here](https://themes.gohugo.io/). For instance, I use [LoveIt](https://hugoloveit.com/) theme.
* Love for phys... just kidding, the other thing we need is to desire for this website.

In this article, I will be using Windows 11 and Hugo Extended installation via Winget. You can use whatever OS you want; however, I highly encourage you to install extended version of Hugo. In this example, I will use my own name in code blocks or in many other places.


## Initialization

### GitHub Repositories
First things first, you need to create two GitHub repositories. One will be called `_Your_Username_.github.io` and other one will be `blog`. The `blog` repository will be the place we store the code and, so called, `LeventKaanOguz.github.io` repository will be used to deploy our website.

After creating your website using below section, you should create a `.\public\` folder under the main folder (like `blog\public`) and also create a folder under somewhere else as like `LeventKaanOguz.github.io` and push a README.md file. Also add `LeventKaanOguz.github.io` as a submodule to `blog\public`.


### Creating Website
You can create a website via Powershell (terminal shell in Windows) using

```powershell
hugo new site <name>
```

Change directory to new created folder and to the `.\themes\`. Now we need to install our theme. Almost all of the themes that are in [Hugo Themes](https://themes.gohugo.io/) uses GitHub, so you can clone that you want directly from GitHub. We will be using [LoveIt](https://hugoloveit.com/) theme, which is this website's theme. You can find detailed instruction on [their website](https://hugoloveit.com/).

To start your Hugo website in development mode, you should run `hugo serve` command. This will start your webserver at port `1313` (You can access it via [http://localhost:1313/](http://localhost:1313/)) and what you will see will pretty much some empty page without any posts.

To create a post you should use the command `hugo new posts/POST_NAME.md` and write down all your Markdown article.

## Deploying Your Website
Now only thing left is to deploy your website. The only thing you need to do is to push all the changes in `blog\posts` and now you are done.
