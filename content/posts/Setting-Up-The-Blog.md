---
title: "Setting Up My Blog"
date: 2024-12-19T17:30:10+10:00
draft: false
scrolltotop : true
---

Welcome to my first 'official' blog post! Here, I’ll walk you through how I set up my blog with Hugo, the Hermit V2 theme, and GitHub Pages. Along the way, I'll share the hiccups I encountered and how I solved them so you can skip the headaches, allowing you to focus on learning and building your own blog!

Why Hugo and GitHub Pages?
I chose Hugo because it's a fast, flexible, and open-source static site generator that allows for full customization with minimal effort. Combined with GitHub Pages, I get free hosting and easy version control, which makes maintaining my site much simpler. This setup is perfect for anyone looking for a lightweight, scalable solution without the overhead of traditional blogging platforms like WordPress or Wix.

{{< admonition warning "Caution">}}
Feel free to follow along, that is why I've written this after all. However, please note that depending on the theme you choose, your journey will likely take you down a slightly different path. Remember to always consult the documentation for your specific theme for any configuration changes!
{{< /admonition>}}


# Stage 1: Preparation

I initially followed a guide my friend created, which you can find at "[**dzonta.com**](https://dzonta.com)", Zonta's guide helped me get an overview of the process and drove me to create the very blog you are reading.

### Here's everything I needed to get started: 

* [Hugo](https://gohugo.io/) *(the static site generator)*
* [a Theme](https://themes.gohugo.io/) *(defines your blog's design and layout, make sure to fork this to your GitHub repo!)*
* [Git](https://git-scm.com/download/win) *(version control)*
* [a GitHub account](https://github.com/) *(online platform for hosting and sharing code)*
* [Chocolatey](https://docs.chocolatey.org/en-us/choco/setup/) *(Windows package manager)*
* [Visual Studio Code](https://code.visualstudio.com/download) *(text editor)*
* [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.4) *(make sure it’s not Windows PowerShell)*

{{< admonition tip>}}
To speed up the installation process, you can leverage Chocolatey by running the following command to install Hugo, Git and VS Code for you:

```powershell
choco install hugo-extended git.install vscode -y
# Installs Hugo, Git, and VS Code using Chocolatey package manager.
```
Chocolatey simplifies software installation on Windows by automating the process with a single command. If you’re unfamiliar with it, consider checking out the [Chocolatey documentation](https://docs.chocolatey.org/en-us/why/) for more details on its benefits.

{{< /admonition>}}

# Stage 2: Setting Up

After setting up a GitHub account, I followed the [Hugo Quick start guide](https://gohugo.io/getting-started/quick-start/) to complete the below steps from a new powershell window (or the terminal within VS Code):
1. ```powershell
    hugo new site quickstart
    # Creates a new Hugo site in a folder named "quickstart."
    ```

* *You can change "quickstart" to whichever folder directory you would like your blog to be stored in.*

2. ```powershell
    cd quickstart 
    # Changes the working directory to the "quickstart" folder.
    ```
*  *If you changed the directory in step 1, change it here too.*

3. ```powershell
    git init
    # Initializes a new Git repository in the current directory.
    ```
* Starts the Git Module within your Powershell session

4. ```bash # Set to bash rather than powershell to avoid the ':' being highlighted 
    git submodule add https://github.com/xBrendan66/Blog-Theme.git themes/HermitV2
    # Adds the HermitV2 theme repository as a Git submodule.

* *Be sure to change the URL to the fork of your theme!*

5. Within File Explorer on your device, you should now be able to find the new folder directory that you have just created, it should have some pre made subfolders. Locate the file "hugo.toml", this is going to be where all global changes and config settings are handled. More on this in Stage 3, though for now, either use the command below to set your theme within the 'hugo.toml' file, or open hugo.toml within VS Code and add `theme = 'HermitV2'` here.

```powershell
echo "theme = 'HermitV2'" >> hugo.toml
    # Appends the theme configuration to the Hugo settings file.
```

{{< admonition warning>}}
Note: I'm using HermitV2 as my theme. Make sure to replace this with the name of your chosen theme where applicable.
{{< /admonition>}}

6. Whilst you are browsing the folder structure, locate the "content" folder and create a subfolder within named "posts". Leave the posts folder empty for now, we will come back to it in Stages 3 & 4.

7.  To test that your blog is working locally, enter the command `hugo server` this will give you a URL that you can use to view the current state of your blog in real time, via a local server. This command is useful for testing and checking changes as you go!


# Stage 3: Customisation and Configuration

Now that my blog was up and running locally, it was time to start customising it. This involved diving into the `hugo.toml` configuration file, tweaking some settings, and figuring out how to make things work with the Hermit V2 Theme. It wasn’t without challenges, but that’s part of the fun, right?

First things first, let's give the site a name and subtitle!
```toml
title = "Text Goes Here"
    # Sets the title of the site.

[params]
homeSubtitle = "Text Goes Here"
    # Sets the subtitle of the site.
 ```

Within the Hermit V2 Theme, there are x3 fields at the top of each post:
* Author
* Read Time
* Publication Date

To set these, add the following code under your `[params]` heading:
```go
author = "Text Goes Here"       #Change this to your name
readTime = true 
dateform = "Jan 2, 2006"        # Customise these date formats to your liking
dateformShort = "2006-01-02"     
dateformNumTime = "2006-01-02 15:04"
```

{{< admonition tip>}}
For further configurations to test, please view the [HermitV2 documentation "Explaining Configs"](https://1bl4z3r.github.io/hermit-V2/en/posts/explaining-configs/), or the corresponding documentation for your theme.
{{< /admonition>}}

If you've been checking your progess with `hugo server` you may notice that your homepage is looking nicer, though you are lacking any navigation to your posts from the homepage - let's fix that with some code!
```go
[menu]

  [[menu.main]]
  name = "All Posts"
  url = "posts/"
  # Adds a navigation menu link to the "posts" folder of your blog.
  ```

  Your site is now 100% functional (locally)! To start writing your first post, open the 'posts' folder and create a new file and save it with the '.md' (markdown) extension as this is the format required by Hugo. If you are unfamiliar with using Markdown to format and write text, I'd reccomend checking out [this guide to basic syntax for markdown](https://www.markdownguide.org/basic-syntax/). I'll also be making a guide on useful features within Hermit V2 as I learn more about it; Keep an eye out for this!

  # Stage 4: It's Alive!

  With the blog customized and running locally, it was time to make it live on the web! Hosting it on GitHub Pages was a straightforward process, but like everything else, there were a few bumps along the way. Here’s how I got it all set up.

  To host your blog on GitHub Pages, you’ll need a public repository named in the format `username.github.io`. For me, this was `xBrendan66.github.io`. Once the repository was created, it was time to push my local blog files to GitHub.

  I started by signing into GitHub via Git in the terminal using this command:

```bash
git credential-manager github login
    # Logs into GitHub using the Git Credential Manager.
```

Next, I set up the remote repository and attempted to push my local files:

1. 
```bash
git remote add origin https://github.com/your-username/your-repo.git
    # Replace 'your-username' and 'your-repo' with your GitHub username and repository name.
```
2. 
```bash
git branch -M main
    # Renames the current branch to "main."
```

3. 
```bash
git push -u origin main
    # Pushes the local repository's changes to the remote "main" branch.
```

Unfortunately, this didn’t work at first. The fix involved creating a new branch and ensuring Git recognized me as the user:

1. 
```bash
git checkout -b main
    # Creates and switches to a new branch named "main." 
```

2. 
```bash
git add .
    # Stages all changes in the working directory for the next commit.
```

3. 
```bash
git commit -m "Initial commit"
    # Creates a commit with the message "Initial commit."
```

4. 
```bash
git config --global user.email "your-email@example.com"
    # Sets your global Git email
```

5. 
```bash
git config --global user.name "Your Username"
    # Sets your global Git username
```

6. 
```bash
git commit -m "Initial commit" 
    # Creates a commit with the message "Initial commit."
```

7. 
```bash
git push -u origin main
    # Pushes the committed changes to the remote "main" branch and sets tracking.
```

After refreshing the repository on GitHub, all the files were there, and the site was ready to be configured for GitHub Pages.

To enable GitHub Pages, I navigated to Settings > Pages in the repository. Under Build and Deployment, I selected GitHub Actions as the source.

At this point, I needed to set up a workflow to automatically build and deploy my site whenever I pushed changes. This required creating some new files in the repository.

1. In the root of my repository, I created a new folder called '.github'.
2. Inside '.github', I created another folder called 'workflows'.
3. Within 'workflows', I added a new file named 'hugo.yaml'.

For the workflow configuration, I used a template from [this gist](https://gist.github.com/thisismikekelly/1a24ad2c8c923127dc3cb29edca13746) or [the Hugo documentation](https://gohugo.io/hosting-and-deployment/hosting-on-github/). After pasting the contents into a new 'hugo.yaml' file, I saved the changes and pushed them to GitHub:

1. 
```bash
git add .
    # Stages all files for commit (used again for later changes).
```

2. 
```bash
git commit -m "Add Hugo workflow"
    # Creates a commit with the message "Add Hugo workflow."
```

3. 
```bash
git push
    # Pushes the changes in the repository to the remote server.
```

{{< admonition tip>}}
With the new workflow, each time you push a new commit, it will automatically display the new content to your static site!
{{< /admonition>}}

# Stage 5: Finishing Touches

With the blog hosted successfully on GitHub Pages, the next step was to set up a custom domain and make some enhancements like adding a favicon and social links.

I decided to use my custom domain, `bmatho.com`, for the blog. Here’s how I got it working:

1. **Adding the Domain in GitHub Pages:**  
   - Went to **Settings > Pages** in the repository.  
   - Under **Custom Domain**, added `bmatho.com`.  
   - GitHub prompted me to add a TXT record to my DNS server to verify ownership of the domain.

2. **Dealing with Verification Issues:**  
   - Initially, the custom domain setup failed. To resolve this, I added four A records in my DNS settings pointing to GitHub’s servers as per [GitHub's documentation](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site):  
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - After this, `bmatho.com` started showing my blog, though it was formatted weirdly...

   3. **Fixing the Formatting Issue:**  
   
   ![Formatting Issue](/Setting%20Up%20The%20Blog/Formatting%20Issue.jpg)

   - My base URL in the `hugo.toml` file was set to `https://bmatho.com`, but since I hadn’t set up HTTPS yet, this was causing the formatting issue.  
   - I changed it to `bmatho.com`, and the site loaded correctly.
   - I then proceeded to enable HTTPS for my domain, changed the URL back to https:// within hugo.toml, pushed the change and verified that is is now working!

   ### Adding a Favicon  
To replace the default “globe” favicon, I used [favicon.io](https://favicon.io/favicon-generator/) to create a custom favicon.  

1. Downloaded the favicon files and added them directly to the `static/` folder of my Hugo project.  
2. After pushing the changes, the new favicon appeared on the site.

### Adding a GitHub Link  
To make the blog more interactive, I added a link to my GitHub repository in the footer. This required updating the `hugo.toml` file:  

```toml
[[params.socialLinks]]
    name = "github"
    url = "link goes here"
    # Adds a social link to your GitHub profile in the site's footer.
```

With these updates, the blog now feels more polished and professional. The custom domain, HTTPS, and favicon give it a personal touch, and the social links make it easier for visitors to connect with me!

# Closing Notes

And that’s it, your blog is live! I hope this guide not only helped you learn something new but also inspired you to create a blog of your own. Whether you're sharing personal learnings, homebrew projects, or something else entirely, the web is now your canvas. Stay tuned as I continue improving this site and sharing more tips along the way.

Until next time, happy blogging!

-Brendan

