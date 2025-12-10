---
publish: "true"
---
Goal: I want to publish some of my Obsidian notes to the web. The idea is to create a blog like repository that I can use as idea dumping but also to create a cohesive storytelling on some topics. I want to integrate a summary of the notes to LinkedIn and reference the linkedin link in the notes and a link to the published note on LinkedIn

Technology: after a brief discussion with Perplexity I am opting for Obsedian > Quartz > GitHub > GitHub Pages
Let's see how it goes

Info:
- I am working on a Mac
- My Obsedian Vault is on iCloud

## Step 1. HOW/WHERE TO PUBLISH 
what do I use to publish. Perplexity suggests GitHub Pages. I have Github account and I started working on it again, so... why not.

### GitHub Pages
Start with https://docs.github.com/en/pages/quickstart
Ok I created a new project following the instructions
issue 1. the page url is not immediately available... should I wait 10minutes? **yes**

GitHub pages can read md files
I created a new page, Technically I do not need to transform the md files because github pages does that on its own.

## Step 2. HOW TO GET OBSIDIAN md files TO GITHUB
Let's use QUARTZ an SSG (static site generator) to pull the obsidian files and create a structured website

Start with Quartz 4 https://quartz.jzhao.xyz/?ref=ssp.sh
it is pretty straight forward. 

- check node version, check npm version
- follow instructions to clone and install quartz
	- create a project folder where to install and run quartz (mine is under /Projects/nina_website and it contains the cloned github repository where I will finally publish the content)
	- follow the instructions in the terminal to connect quartz to your obsedian vault with a **Symlink an existing folder**. 
	  I have my Obsedian vault in **iCloud** so I had to find the true link. I opened the folder in a new terminal and then used the `pwd` command to retrieve the correct path.
- run `quartz create`
- for the first run without changing configurations quartz requires and index.md file, so I added an index page in Obsedian. (*I plan to figure out how to change this default*)

available on localhost:8080 and live updating (unless it finds and error and you need to re-run it)

## Step 3: recap
1. Ok now I have the github repository publishing the readme on a github page
2. I have all my Obsedian vault published locally through quartz. 

### What I want
1. #priorityHigh I want to separate what to publish and just random notes that I take when I feel like
2. #priorityLow I may want to change the overall look of the pages.
3. I want to publish the quartz public folder to git hub repo
4. I want to ensure that by committing, I will have that same website on github pages

## Step 4: tell quartz to only look at a specific folder
Ok, I am trying a few options
### Explicit Publish
configure quartz filters to accept only files with property publish set to true with the plugin Explicit Publish https://quartz.jzhao.xyz/plugins/ExplicitPublish
To add a property to a file, go to obsidian, open a file, at the top right menu, "Add property" publish:true
then edit quartz.config.ts filters, remove the existing filter and use Explicit Publish (or maybe you can use both)
### Remove Drafts
DEFAULT 
configure quartz filters to accept only files with property publish set to true with the plugin Remove Drafts https://quartz.jzhao.xyz/plugins/RemoveDrafts
To add a property to a file, go to obsidian, open a file, at the top right menu, "Add property" draft: true

### Option 3. Connect to a specific folder in your Vault
you can also only add a specific folder of your vault for quartz to process. This will give you more control. You can still control more with the above filters
As I already started with quartz, I had to remove the existing content folder, create it again and then re-run the command `npx quartx create`

## Step 5: Synchronise Quartz to GitHub Pages

Final step, I want to take the public folder of quartz and commit it to github. 
Not sure I should keep the configuration of quartz on the same repository... why would I not?

### Generate and Commit the public folder into your GitHub repo
1. Build quartz with the output option set to a path in the github repository condigured for GitHub pages. I published it in a /docs folder 
   `npx quartz build --output [pathtoyourlocalinstanceofyourgithubrepository]/docs`

I think I would version also the quartz project as I am adding more and more customisations and it is better to store them more safely than in an old Mac.

## Step 6. Recap
I have a selection of my Obsidian notes live at https://nina4github.github.io 🎉
I have the very basic design from the default theme of Quartz - changed a couple of basic details in `quartz.config.ts` like _PageTitle_ and added a _description_ 


And then I actually changed the approach, created a new repo, synchronised all quartz in it and then created a github action to publish the content to GitHub pages as described here https://notes.nicolevanderhoeven.com/How+to+publish+Obsidian+notes+with+Quartz+on+GitHub+Pages
https://quartz.jzhao.xyz/hosting#github-pages