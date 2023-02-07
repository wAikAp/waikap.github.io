---
title: Chirpy Jekyll Blog Setup MacOS
author: Waikap
date: 2023-01-05 00:00:01 +0800
categories: [Blogging]
tags: [Setup]
---
# Chirpy Jekyll Themes

Github有[official document](https://docs.github.com/en/pages/quickstart)教點將Jekyll setup系自己account下.
呢個方法非常之快&方便加上唔洗系local setup environment, 但係d theme唔係我心目中想要, 機緣巧合下穩到Chirpy, feels good

[Chirpy getting-started](https://chirpy.cotes.page/posts/getting-started/) 正路黎講都係跟住份doc step by step
呢度有2種Installation方法.

* [**Using the Chirpy Starter**](https://chirpy.cotes.page/posts/getting-started/#option-1-using-the-chirpy-starter) - Easy to upgrade, isolates irrelevant project files so you can focus on writing.
* [**Forking on GitHub**](https://chirpy.cotes.page/posts/getting-started/#option-2-forking-on-github) - Convenient for custom development, but difficult to upgrade. Unless you are familiar with Jekyll and are determined to tweak or contribute to this project, this approach is not recommende

如果想非常客製化當然選Forking, 但就我個case唔想理咁多, Chirpy Starter系最好選擇.
high level黎講, 無論你揀fork or starter其實原理上都係炒曬呢堆files去自己github repo下, 跟住再clone&pull反落自己local部機, setup environment/install related lib
跟住寫下d markdown(就係d posts)然後放係_post/呢個folder下面, 改下d樣式/config/etc

#### Using the Chirpy Starter

按[Chirpy Starter](https://github.com/cotes2020/chirpy-starter/generate)會自動跳到Github create a new repo
輸入翻自己噶username系 `<GH_USERNAME>.github.io` 入面如下圖

![1672972287656](/posts/2023-01-05/1672972287656.png)

#### Setup environment

Create完就可以clone反落自己部機可以用Github desktop/git cmd 隨你喜歡, 跟住就可以開始係local setup environment. [jekyll Instllation MacOS](https://jekyllrb.com/docs/installation/macos/)

1. 如果未裝[Homebrew](https://brew.sh/)就要裝左先 (已安裝Skip this step to 2.)

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
2. 裝左就將homebrew update去最新version & upgrade all individual packages

   ```bash
   brew update
   brew upgrade
   ```
3. Install & update homebrew 無問題就可以install `chruby` and `ruby-install` (有問題pls google) (homebrew常見問題不外乎錯path/有也裝漏/etc, google can help)

   ```bash
   brew install chruby ruby-install xz
   ```
4. Install Ruby (supported by Jekyll)

   ```bash
   ruby-install ruby 3.1.3
   ```
5. 完成後, 要行d cmd, 其目的係將新裝噶chruby ruby替換左系統自帶的

   ```bash
   echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.zshrc
   echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.zshrc
   echo "chruby ruby-3.1.3" >> ~/.zshrc # run 'chruby' to see actual version
   ```

   但係如果你跟住份doc打完下面三句, restart terminal, 有機會出現 `chruby: unknow Ruby: ruby-3.1.3` 經過google大神發現好多人都有類似情況, 而係jekyll噶[issues](https://github.com/jekyll/jekyll/issues/9194)都穩到解決辦法

   ![1672974883840](/posts/2023-01-05/1672974883840.png)
6. Finally !! After installing Ruby with chruby, install the latest Jekyll gem

   ```bash
   gem install jekyll
   ```

#### **Running Local Server**

1. cd to your project's path
   ```bash
   cd /Users/who/Desktop/Mine/waikap.github.io
   ```
2. run cmd, to install dependence
   ```
   bundle
   ```
3. run cmd to start the application
   ```bash
   bundle exec jekyll s
   ```
4. After a while, the local service will be published at  *[http://127.0.0.1:4000](http://127.0.0.1:4000/)* .

#### **Depolyment**

git push, 會自動行github action, 會幫你自動build & deploy 到github噶static server (Linux) 另外注意: Before the deployment begins, check out the file `_config.yml` and make sure the `url` is configured correctly. Furthermore, if you prefer the [**project site**](https://help.github.com/en/github/working-with-github-pages/about-github-pages#types-of-github-pages-sites) and don’t use a custom domain, or you want to visit your website with a base URL on a web server other than  **GitHub Pages** , remember to change the `baseurl` to your project name that starts with a slash, e.g, `/project-name`.
