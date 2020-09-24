
<h1 align="center">
  Cyberguide
</h1>

![](/images/feature.png)

<h3 align="center">Welcome to Cyberguide, an open source, definitive collection of resources, writeups and guides for bootstraping your career in Cybersecurity.</h3>

<p align="center">Maintained by the Cyber Defense Club at Liberty University</p>

<br>

<p align="center">
  <a href="#key-features" style="color: red; padding-left: 10px; padding-right: 10px; padding-top: 5px; padding-bottom: 5px; border-radius: 3px; background-color: white; box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.75);">Key Features</a> •
  <a href="#install">Access</a> •
  <a href="#install">Rationale</a> •
  <a href="#Todo">Todo</a> •
  <a href="#credits">Credits</a> •
  <a href="#license">License</a>
</p>


## Key Features
* **All the best resources links in one place**
    * No more endlessly scrolling resource chats
* **Everyones plays a part**
    * Anyone can create a pull request to suggest a change
    * Organizational Members can make changes
* **Convenient**
    * Online
    * Responsive
    * Current

## Access

*Current Link*

[https://cyberguide.os9.run/](https://cyberguide.os9.run/)

*Future Link: Awaiting approval*

https://guide.lucyber.club/

## Rationale

This project was a created as an upgrade for a "resources" channel in our Discord Chat
that contained a lot of good resoures, but was an bottomless pit nonetheless. Accessing 
those resources later on wasn't practical unless you knew what to search for.

Why github, markdown, and [Hugo](gohugo.io)? By using this technologies, we create
and scalable, maintainable, and standard platform that is already used for documentation in
the industry. By writing in plain text with markdown and defining structure with a simple folder
structure, we can export that content to a Website (default), a PDF, and even an ebook.

## Development

For simple changes, those with write access to the repository can make changes to the files directly on github. 
When a change is commited to the master branch, the CI/CD pipeline with Github Actions kicks off, generates the site
with Hugo and deploys the result. If you're curious, that workflow file is located at `.github/workflows/main.yml`

For local development, you will need [NodeJS](nodejs.org), and [Hugo](gohugo.io) installed. Simple clone the repository
make your changes, and commit them. You will need to build the theme assets for the first time. After that you
can use hugo's local dev server with live reloading to see changes as you make them.

**Example:**

```
git clone git@github.com:lucyber/cyberguide.git
cd cyberguide/themes/geekdoc
npm install
gulp default
cd ../..
hugo server -D
```

*Commit changes*

```
git add -A
git commit -m "Added privesc links"
git push
```

## Todo

* [] Define Skill based outline
* [] Define topic-based outline
* [] Begin adding resources links
* [] Write guides


## Credits

- Philip - Original Idea
- [Hugo](http://carbon.now.sh) (Static Site Generation from Markdown)

## License

MIT



