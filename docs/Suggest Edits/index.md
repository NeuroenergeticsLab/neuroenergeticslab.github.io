---
layout: default
title: How to edit
nav_order: 10
---

# Option 1: edit single file online on Github

- Go to the repository ([here](https://github.com/Armos05/Armos05.github.io)).
- All the changes in the contents can be done by accessing the ``docs`` folder.
_Note: To perform any changes you need to have a github account and become a contributor to this repo before._

## Add a new section
- Click on ``Add file``, then go to ``Create new File``.
- Create a new folder and name it as the section you want to add. After putting in the name, press ``\``. 
- This will make you folder now. After this name your markdown file anything you want with extension ``.md``.
- Then add the following in the begining of your markdown file:
```
---
layout: default
title: <page title>
parent: <title of the parent page>
has_children: true
nav_order: 1
---
```

- Update the Title name, as to which you want to view on the website, and append the nav_order as well. 
- `has_children = True` lets you attach subpages to your markdown.
_Note: If you want to move this section up, you have to change the order of the section, you are replacing it with._
- Now, start writing into your markdown file. You can find some basic syntacts of markdown ([here](https://www.markdownguide.org/basic-syntax/)).
- Also, if you want to paste an image into your section, simply copy it to your local clipboard, and press ``Ctrl+V``, where you want to paste in your markdown file. Although this feature will not work if you will just copy it from google images (say), it should be copied from your local machine. Better idea would be to copy the image and just paste on something like powerpoint, Copy it again, and then you can just paste in the github markdown.


## Update a section
- Go to the folder which you want to edit.
- Open the markdown file associated with it. 
- Edit it using your preference.


# Option 2: edit multiple files locally and push to Github (for developers)

Option 1 above only lets you edit single page at a time. When you need to edit multiple pages, it is a lot easier to do that in one commit. The advantage is that you can see in real time what the website looks like before publishing it online.

## Before you begin

Install the requirements:

- make sure that git is installed
- [install Ruby, Jekyll and Bundler](https://jekyllrb.com/docs/installation/ubuntu/)

The easiest way is to set up this environment on Ubuntu/WSL and use VS Code to edit the markdown files.

## Set up the website repository

- Clone the repository from Github  
`git clone https://github.com/NeuroenergeticsLab/neuroenergeticslab.github.io.git`
- Install the Gems:  
'cd neuroenergeticslab.github.io && bundle install'
- add git remote:  
`git remote add origin https://github.com/NeuroenergeticsLab/neuroenergeticslab.github.io.git`

Now you're ready to start editing the pages.

## Preview the changes 

As you edit the pages, you can preview the changes in real time with jekyll. At this point, all changes are local and not visible to anyone online. You should be able to see the changes as soon as you save the .md file.

To start serving the website locally:
- `bundle exec jekyll serve`
- go to `localhost:4000` (or, the address  that the command tells you) in the browser


## Push the updates to Github

One you've finished editing, push the changes so they go online:

```
git add .
git commit -m "commit description"
git push origin master
```

After a few minutes, Github will build the website and it will be available online.

## Update a gem

Sometimes it is necessary to update a gem to keep the repostitory up-to-date.

- Check the available package version: https://pages.github.com/versions/
- `nano Gemfile` and change the package version, e.g.  
`gem "github-pages", "~> 206"` --change to--> `gem "github-pages", "~> 214"`
- `bundle update`
- `git add . && git commit -m "updated github-pages gem" && git push`

It is not necessary to include verions of other germ in the Gemfile because they will be installed as dependencies of github-pages

## Keep the local repository updated

When you start editing again, don't forget to run `git pull` to synchronize the repositories.
