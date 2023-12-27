---
layout: post
title: Jekyll Build on Windows
date: 2023-10-17 11:34 +0800
categories: [Windows, Jekyll]
tags: [installation and depoly]
---

## Instructions[^1]

### Installing Ruby and Jekyll

> **The easiest way** to install Ruby and Jekyll is by using the [RubyInstaller](https://rubyinstaller.org/) for Windows.
> RubyInstaller is a self-contained Windows-based installer that includes the Ruby language, an execution environment, important documentation, and more.
{: .prompt-tip }

1. Download and install a latest **Ruby+Devkit** version from [RubyInstaller Downloads](https://rubyinstaller.org/downloads/). Use default options for installation.

   > *WHICH VERSION TO DOWNLOAD?*
   >
   > If you don’t know what version to install and you’re getting started with Ruby, we recommend that you use the **Ruby+Devkit 3.2.X (x64)** installer. It provides the biggest number of compatible gems and installs the MSYS2 Devkit alongside Ruby, so gems with C-extensions can be compiled immediately. The 32 bit (x86) version is not recommended, unless custom 32 bit native DLLs or COM objects have to be used.
   {: .prompt-tip }

   > *HOW TO UPDATE?*
   >
   > Ruby can be updated to the latest patch version (e.g. from 3.1.0 to 3.1.3) by running the new installer version. Installed gems are not overwritten and will work with the new version without re-installation. It’s sufficient to use the RubyInstaller without Devkit for these update installations. The Devkit can be updated separately using the `ridk install` command.
   >
   > If the new Ruby version is from a different stable branch, then please use a new target directory for installation. That is to say, a previous RubyInstaller-3.1.x installation **should not** be updated by installing RubyInstaller-3.2.x into the same directory. This is because gems with C extensions are not compatible between ruby-3.1 and 3.2. Find out more in the [FAQ](https://github.com/oneclick/rubyinstaller2/wiki/FAQ#user-content-update-install).
   {: .prompt-tip }

2. Run the **`ridk install`** step on the last stage of the installation wizard. This is needed for installing gems with native extensions. From the options input **number 3** to choose **`MSYS2 and MINGW development tool chain`**.

3. Open a new **Start Command Prompt with Ruby** from the start menu, so that changes to the `PATH` environment variable becomes effective. Install Jekyll and Bundler using:

   ```bash
   gem install jekyll bundler
   ```

4. Check if Jekyll has been installed properly: 

   ```bash
   jekyll -v
   ```
   
   > You may receive an error when checking if Jekyll has not been installed properly. Reboot your system and run **`jekyll -v`** again. If the error persists, please open a [RubyInstaller issue](https://github.com/oneclick/rubyinstaller2/issues/new).
   {: .prompt-tip }

That’s it, you’re ready to use Jekyll!

------

### Build & run local Jekyll site[^2]

1. Create a new Jekyll site at **`./myblog`**.

   ```bash
   jekyll new myblog
   ```

2. Create the "myblog" folder in the, for example, **`D:\Jekyll\myblog`** directory.

   ```bash
   mkdir D:\Jekyll\myblog
   ```

3. Change into your new directory.

   ```bash
   cd /d D:\Jekyll\myblog
   ```

4. Build the site and make it available on a local server.

   ```bash
   bundle exec jekyll serve
   ```

5. Browse to [http://localhost:4000](http://localhost:4000/)

    > If you are using Ruby version 3.0.0 or higher, step 5 [may fail](https://github.com/github/pages-gem/issues/752). You may fix it by adding `webrick` to your dependencies: `bundle add webrick`
    {: .prompt-warning }

    > Pass the `--livereload` option to `serve` to automatically refresh the page with each change you make to the source files: `bundle exec jekyll serve --livereload`
    {: .prompt-tip }

    > If you encounter any errors during this process, check that you have installed all the prerequisites in [Requirements](https://jekyllrb.com/docs/installation/#requirements). If you still have issues, see [Troubleshooting](https://jekyllrb.com/docs/troubleshooting/#configuration-problems).
    {: .prompt-tip }

------

### Use alternative Jekyll theme[^3]

#### Prerequisites

Follow the instructions in the [Jekyll Docs](https://jekyllrb.com/docs/installation/) to complete the installation of the basic environment. [Git](https://git-scm.com/downloads) also needs to be installed.

#### Installation

Sign in to GitHub and use [**chirpy template**](https://github.com/cotes2020/chirpy-starter/generate) to generate a brand new repository and name it **`USERNAME.github.io`**, where **`USERNAME`** represents your GitHub username.

> Replace the bundler default source with running the *<u>following command</u>*[^4] to fix network download issue when `bundle`.
{: .prompt-danger }

```bash
bundle config mirror.https://rubygems.org https://mirrors.tuna.tsinghua.edu.cn/rubygems
```

Then clone it to your local machine and run:

```bash
bundle
```
#### Tutorial Wiki[^5]

- Jekyll-Compose plugin

Add this line to your application's Gemfile:

```bash
gem 'jekyll-compose', group: [:jekyll_plugins]
```

And then execute:

```bash
bundle
```

Create your new post using:

```bash
bundle exec jekyll compose "My New Post" --post
```



## References

[^1]: [https://jekyllrb.com/docs/installation](https://jekyllrb.com/docs/installation)
[^2]: [https://jekyllrb.com/docs](https://jekyllrb.com/docs)
[^3]: [https://jekyllrb.com/docs/themes](https://jekyllrb.com/docs/themes)
[^4]: [https://mirrors.tuna.tsinghua.edu.cn/help/rubygems](https://mirrors.tuna.tsinghua.edu.cn/help/rubygems)
[^5]: [https://github.com/cotes2020/jekyll-theme-chirpy/wiki](https://github.com/cotes2020/jekyll-theme-chirpy/wiki)
