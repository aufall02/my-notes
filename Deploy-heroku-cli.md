# Deploying with Git ~ heroku

## Prerequisites
- [Install Git](https://git-scm.com/downloads)
- [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli#install-the-heroku-cli)

## Initializing a Git repository
```
cd example-app
git init
git add .
git commit -m "My first commit"
```

## Create a Heroku Remote
```
heroku create -a example-app
git remote -v
```
note : For an Existing App
```
heroku git:remote -a example-app
```
## Rename a Remote

By default, the Heroku CLI names all of the Heroku remotes it creates for your app heroku. You can rename your remotes with the git remote rename command. For example, rename heroku to heroku-staging:
```
git remote rename heroku heroku-staging
```
## Deploy From a Branch Besides main
To deploy code to Heroku from a non-main branch of your local repository (for example, testbranch), use the following syntax push it to the remote’s main branch:
```
git push heroku testbranch:main
```

## Reset a Git Repository
```
heroku plugins:install heroku-repo
heroku repo:reset --app appname
```


## Referensi
- [Deploy heroku](https://devcenter.heroku.com/articles/git#prerequisites-install-git-and-the-heroku-cli)