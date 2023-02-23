# shortner
![linkshortener_vueJSfinalcompressed](https://user-images.githubusercontent.com/59767843/221048760-1dc420aa-288e-48ad-a1d0-744505852cba.gif)
<p align="center">
 here's a gif image of the website 😊
</p>
shortner is a link shortner created with vueJS version 3 using the Bitly API.

It was created at the end of january 2023 and finished by end of february 2023.

## prerequisites
You will need an bitly API key and an Account to get a key. 
``` 
accessToken: "<your API Key here>",
```

Refer to the bitly website for more informations:

- [Bitly Home page](https://bitly.com/ "Bitly Home Page")
- [Sign up Page](https://bitly.com/a/sign_up/ "Sign up page Bitly")
- [API Doc](https://dev.bitly.com/ "Bitly API Documentation 4.0.0")


## Features
In case everything turns out great it will return a shortnered Link

If something went wrong, it will return some error in one of those conditions: 
- input error, if empty
- input error, if wrong link format
- API error if wrong API key or API related error in the bitly account

In case of an API Error, please refer to the [Bitly API Doc](https://dev.bitly.com/ "API Documentation 4.0.0")

## Improvement tracks
change the ReGeX so that it only validates the links in the following form:
```
 https://www.youtube.com/
 https://bitly.com/
 https://www.indeed.com/
```
And NOT in this form:
```
 http://localhost:8080/
 http://local.host/
 http://example.Kappa/
```

## Project setup

```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```
