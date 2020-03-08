---
title: "Awesome Things I Learned Creating My Own Website"
description: "A walk through of the awesome hings I Learned while making my own personal website."
toc: true
comments: true
layout: post
categories: [website, awesome]
image: images/logo.png
author: Nathan Cooper
---

Hello, Solar System! (As a space faring civilization, I feel it only customary we update our greetings to reflect such awesome accomplishments 🤓) I am a nerd and hopefully you are as well.

This post goes over many of the awesome technologies, resources, and overall tips and tricks I learned while creating my own personal website! This post is **NOT** a tutorial, mostly because there are tons of already existing ones on how to create a website and you don’t want to create *a website* or even *my website* (though mine is pretty awesome), you want you create *your own website*. For me this came from a lot of trial and error and tons of random google searches to fit some niche feature I wanted to add. So, this post is to centralize all of the niche features that went into my website in case any of you out there want to personalize some for your own website. This post is not really made to be gone through end to end, but rather for you to pick out the pieces that resonate best with you and give you inspiration for your own website.

Let’s get some of the boring stuff out of the way first, namely these are the main components that my website is made out of:

* [ReactJS](https://reactjs.org/) - using [create-react-app](https://github.com/facebook/create-react-app) and 

* [Material-UI](https://material-ui.com/) - for the style points 😎 (Sadly not as delicious as brownie points)

* [GitHub Pages](https://pages.github.com/) - for hosting the static site (ty GitHub <3), requires you use gh-pages and setup your create-react-app up correctly. Here is some [documentation](https://create-react-app.dev/docs/deployment/#github-pages) on how that is done

* [GitHub](https://github.com/) and GitHub Pages - for storing my projects and for storing the web demos of my projects (Sounds epic, right?!?!? More on this later)

* [Redux](https://redux.js.org/) - for storing and updating state of ReactJS thingies like lists of current projects and blog posts (More on this later)

* [ReactMarkdown](https://github.com/rexxars/react-markdown) - for rendering my blog posts, which, you guessed it, are markdown files!

* Paperclips - I couldn’t afford duct tape :(

# Niche Features and Tips

## Resume of Coding Projects:

The core motivation behind my website was that I wanted a cool way to show off some of my projects that I’ve created over the years. I’ve seen how others create theirs and actually got inspired in part by [https://nmarch213.github.io/Portfolio/#/projects](https://nmarch213.github.io/Portfolio/#/projects). However, the issue is that these displays of projects need to be manually created and that was a problem for me because like most developers I am lazy and I don’t want to do that. I wanted a way where I could just create new projects and they would be automatically added in the correct format, including images, titles, descriptions, etc. I could just redirect users to my GitHub page, where I place all of my coding projects, but that seemed like a cop out and did not allow for any customization. So, like any good programmer, I made a scrapper that took the output from GitHub and converted into a format for my own usage 😊. This gave my website the ability to update the list of projects automatically as I added new repositories, which the title of each project is just determined by the repository’s name. To add an image to be displayed as the project’s logo, I just add an `icon.png` file to the root of the project and grab the icon from there when displaying the list.

To scrape all this information, I use the amazing [GitHub API v3](https://developer.github.com/v3/) that GitHub provides. This API offers a ton of useful features, but for scrapping my projects I specifically used the [Repositories API](https://developer.github.com/v3/repos/#list-user-repositories). This also has information like the repository’s description, so you could include that information in your list of projects automatically if you so choose. The GitHub API v3 has a bunch of awesome functionality, another API I use is the [Contents API](https://developer.github.com/v3/repos/contents/#get-contents) for listing out the different posts I have created (more on this later)! For integrating these APIs using ReactJS, I suggest using [Redux](https://redux.js.org/) for storing the state, i.e., the projects and blog posts once they have returned from the GitHub API, and [Axios](https://github.com/axios/axios) for actually making the HTTPS requests.

Besides just hosting one website using GitHub Pages, you can have one per repository. Incorporating this with the dynamic list of my coding projects, I am able to now create their own page that can serve as documentation or can even be a web demo! Currently I am not using this feature to the best of its ability, but I plan on overhauling my more put together projects so that they have at the very least some documentation using this awesome feature.

Overall, using very simple components offered by GitHub I am able to have my custom resume of projects that dynamically updates when I create a new one and links to documentation or a web demo of the project. Any updates to the actual project are reflected on the website without additional changes to some configuration file that contains all of the projects I have.

## Blog:
I know do all of my blogging using the new awesome [fastpages](https://github.com/fastai/fastpages) library built by Hamel Husain and Jeremy Howard!

### [Deprecated]
Aside from being able to high-light my accomplishments, I wanted to be able to express myself on a multitude of topics. I never thought I would be a blogger, but a blog post by the awesome Rachel Thomas, [Why you (yes, you) should blog](https://medium.com/@racheltho/why-you-yes-you-should-blog-7d2544ac1045), inspired me to take it seriously. I tried with Medium, but I wanted something of my own and when I saw the equally awesome Jeremy Howard discussing his work on [Fast Template](https://github.com/fastai/fast_template) that allows you to easily create your own personal blog using GitHub Pages and simple Markdown files I knew the time was now to commit. Now while I do not directly use Fast Template, because it is a bit too rigid for the amount of customizability I like to perform, I drew a lot of inspiration, namely writing blog posts as markdown files and having them stored statically on my website instead of on some weird MongoDB. To integrate this concept of using Markdown files I needed a way to render them easily using React, which is where I found this awesomely customizable library for doing just that called [React Markdown](https://github.com/rexxars/react-markdown). What’s nice about React Markdown is that each of the formatting components such as code snippets and headings are separated into their own rendering engine allowing you to swap out or customize them very easily. So since I quite enjoy dark theme, I found this awesome post by [Bexultan A. Myrzatayev](https://medium.com/young-developer/react-markdown-code-and-syntax-highlighting-632d2f9b4ada) showing how you can use a custom react highlighting engine, I use [React Syntax Highlighter](https://github.com/conorhastings/react-syntax-highlighter), and swap out the default theme for code syntax highlighting for something like "atomOneDark"! (obviously I chose a dark theme, because dark theme is the only theme)

To write my posts, I don’t just write directly using Markdown as that would be extremely painful. I took the advice of Jeremy Howard again from his post on [Syncing your blog with your PC, and using your word processor](https://www.fast.ai/2020/01/18/gitblog/) and used a word processor, in my case it is [Google Docs](https://www.google.com/docs/about/). Sadly, Google Docs does not allow you to directly export your document as a Markdown file, but thankfully an awesome person named Mangini created [gdocs2md](https://github.com/mangini/gdocs2md) that does the conversion and handles grabbing the images and emails them to you!

## Material Design:

As a nerd and mostly a computer nerd, my artistic skills are not the best. However, I wanted my website to look stylish, clean, modern, cool, hip.... (words I searched google for when trying to create a pretty website). This brought me to Google, they always create such chic looking websites and mobile apps, in my opinion obviously, so it wasn’t too surprising to learn that Google wrote the bo… well, website for designing GUI components, which they called [Material Design](https://material.io/). This is where Material-UI comes in. It is a complete React component implementation of the Material Design language and it looks smooootthhhhh. Using it is quite simple as laid out in there website, but I’m including a code snippet because I want to flex how my website is able to render code snippets courtesy of [React Markdown](https://github.com/rexxars/react-markdown) and [Bexultan A. Myrzatayev](https://medium.com/young-developer/react-markdown-code-and-syntax-highlighting-632d2f9b4ada)’s awesome post on how to change the theme used in code snippets :

Code snippet from what a project entry looks like:

```javascript

import {

  Button,

  Card,

  CardActions,

  CardContent,

  CardMedia,

  Typography

} from "@material-ui/core";

….

const site = has_pages ? (

    <Button variant="contained" color="secondary" href={pages_url}>

      View Site

    </Button>

  ) : null;

return (

    <Card className={classes.card} fullWidth>

      <CardMedia

        className={classes.media}

        image={icon_src}

        onError={e => {

          console.log("cannot find icon");

        }}

      />

      <CardContent>

        <Typography gutterBottom variant="headline" component="h4">

          {_.startCase(_.camelCase(name))}

        </Typography>

      </CardContent>

      <CardActions>

        {site}

        <Button variant="contained" color="primary" href={html_url}>

          View Repo

        </Button>

      </CardActions>

    </Card>

  );

….

```

## Development:

I think programming is an invaluable skill that I am constantly learning to improve. So, I highly recommend those creating their own website to at least try to program it themselves. It is an adventure of pain and misery that I wish to inflict onto others, hahaha, haha, ha… But extremely rewarding when you finally see that beautiful glowing (please don’t make your website glow, it’s annoying) website plastered on your web browser (please let it be Chromium based or just basically not Explorer). All programmers need some system in which to develop whatever it is they care about creating. This is where things like Integrated Development Environments (IDEs), debuggers, and testing frameworks come in handy.

To keep myself sane, I spent a long, arduous, and tedious time trying and experimenting with different workflows for developing systems. And I have found the holy grail that has answered all of *my* questions and that allows for 10X greater productivity for *me *(your results will most certainly differ if you decide to use the same developmental setup). For me, I found the combination of [Visual Studio Code](https://code.visualstudio.com/) and [Docker](https://www.docker.com/) to be the textbook definition of perfection. In particular, the [Remote Container](https://code.visualstudio.com/docs/remote/containers) extension that some genius made. This extension allows you to connect your vscode editor to a docker container’s file system. So, why is this so important to me? Well Docker allows you to spin up pretty much any environment you want such as a node server for hosting a ReactJS website :D, but most importantly it allows you to version and share these environments through Dockerfiles. This allows me to specify an environment per project, so I don’t have to maintain installing all of the dependencies that may conflict with each other on my local machine. This is why I use Docker for pretty much everything I do and I also quite enjoy using vscode, so being able to marry the two is absolute perfection!

# Conclusion

So, that concludes my first blog post! I hope you are able to use some of these awesome things I learned while creating my own website for your own. Keep a lookout for my future posts, I am planning on creating posts circulating around the following topics:

* Machine Language Processing (MLP) - like Natural Language Processing (NLP), but for computer nerds like us 🤓.

* Automatic Code Comment Generation using Deep Learning.

Also, feel free to contact me using my custom "Contact" system, which uses this awesome [Google Script](https://github.com/dwyl/learn-to-send-email-via-google-script-html-no-server) for sending emails without the need of manually setting up a backend server, integrated into my website or on twitter [@ncooper57](https://twitter.com/ncooper57) :).
