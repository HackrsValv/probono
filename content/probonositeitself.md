Title: Pro Bono Page hosting explained
Date: 2024-01-06 10:03
Category: (Almost) free website hosting

Hi! So let's start from the Pro Bono Page hosting itself. Its hosting is almost free and you can do it even for less amount of money then I spent.

## Services:

There are many services in the Internet, that are giving some starting packages that are either very cheap or free and here I am using two of them: 

- [Cloudflare](https://www.cloudflare.com/)
- [GitHub](https://github.com/)

## To generate the site:

- [Pelican](https://getpelican.com) - a static web site generator. Basically you create pages in MarkDown and it generates static HTML files - so any hosting, even the cheapest one shared hosting can host the site and it is very fast, small, easy to backup/restore/move. Static site generators are great! There are many of them - I am using Pelican for this page because I know a bit of Python and also it looked like it did not require lots of work to use. Also - it is very difficult to hack the sttically generated site that is deployed in this way, especially if it is hosted in Cloudflare or any other CDN that take cares (sombutnotol) security aspects. 

If you need more powerful one generator - check [Hugo](https://gohugo.io).

## The costs: 
    
- Domain name (in my case - this is a subdomain, probono that is part of hackrsvalv.com - so I don't pay extra for that). Usually I buy domain names via GKG.NET, but recently started to use Cloudflare for convenience. It is not the wisest solution though as I am putting all eggs in one basket (i.e. if Cloudflare would boot me out or would be having issues - managing of the domain might be problematic), but I accept the risks.

- I pay for GitHub subscription, but you do not have to. The setup does not require paid GitHub service. Also you can use any Git provider you want or do not use it at all and keep everything on your computer (make sure you have good backups).

How does it work? 

I will describe a flow I am using as for details on how to specifically use GitHub or Cloudflare - you can find it on the internet, but if you fail - come and we will see what can be done.

## Steps:

1. Buy a domain (around 10 bucks)
1. Get Cloudflare subscription (free)
1. Get GitHub subscription (free)
1. Go to Pelican site and follow QuickStart
1. Go to GitHub and create a new GitHub repo
1. Create requirements.txt - this will instruct Cloudflare build machine to install required packages. More information is [here](https://developers.cloudflare.com/pages/framework-guides/deploy-a-pelican-site/). I only had to use `pip3 list --format=freeze > requirements.txt` command as Cloudflare way produces some weird paths. I have found the workaround on [stackoverflow](https://stackoverflow.com/questions/62885911/pip-freeze-creates-some-weird-path-instead-of-the-package-version).
1. Use GitHub help to push directory from your computer to the GitHub repo (don't forget `git init`). Also I suggest to use [.gitignore for Python](https://raw.githubusercontent.com/github/gitignore/main/Python.gitignore) - save it as .gitignore in Pelican project directory).
1. Go over to Cloudflare and get to *Workers & Pages* screen. Create and and you will have to connect GitHub to Cloudflare. Select framework Pelican, add `PYTHON_VERSION 3.11` to the environment variables, everything else can be left as default. (This Python version worked for me, the version suggested in Cloudflare docs - did not).
1. There should be many log lines in the build, but we are only interested in `Success: Your site was deployed!`
1. Alright! Now we check if everything is OK: in the deployment details you can find a link to the website. If that works as expected - then let's connected the domain name to the page.
1. Just add custom domain and Cloudflare will do everything automatically. In my case I have added probono.hackrsvalv.com and in a couple of minutes it has started to work.

## Next:

Now go to explore more what can Pelican do for you. Any time you want to change anything/add new pages - you will have only edit/add, commit and push to the GitHub repo - Cloudflare will pickup changes automatically and will deploy the site!

In the next blog post I will show you on how to have comment functionality for free on the static site.






