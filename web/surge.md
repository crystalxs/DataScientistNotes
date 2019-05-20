# Surge

> <https://surge.sh/>
>
> Static web publishing

## Initial

```shell
# install
npm install --global surge

# sign up or log in
surge
# input email and password
```

## Deploy a Jekyll project

```shell
jekyll build
surge _site/
# _site is the default destination, if customed, use the customed one
```

## Deploy a Webpack project

Configure `scripts` section in `package.json`:

```json
"scripts": {
  "start": "hjs-dev-server",
  "build": "webpack",
  "deploy": "npm run build && surge -p public -d somedomain.com"
}
```

