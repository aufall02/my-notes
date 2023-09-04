# HEROKU

## Install heroku cli
- Download cli heroku [windows](https://cli-assets.heroku.com/heroku-x64.exe)

- Mac 
```
brew tap heroku/brew && brew install heroku
```
- tarball
```
curl https://cli-assets.heroku.com/install.sh | sh
```
- npm 
```
npm install -g heroku
```
Verifikasi login
```
heroku --version
```

heroku login
```
heroku login
heroku login -i
```

login with multi factor authentication
```
heroku authorizations:create
heroku auth:token
```

## Referensi
 * [Heroku cli install](https://devcenter.heroku.com/articles/heroku-cli)
* [multi factor aunthentication](https://help.heroku.com/PBGP6IDE/how-should-i-generate-an-api-key-that-allows-me-to-use-the-heroku-platform-api)