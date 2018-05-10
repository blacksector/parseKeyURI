
<h1 align="center">
  <br />
  <br>
  jsKeyURI
  <br>
</h1>

<h4 align="center">A quick vanilla JS solution to parse the URI and parameters for one time passcode (OTP) key URI.</h4>


<p align="center">
  <a href="https://paypal.me/omarq" target="_blank">
    <img src="https://img.shields.io/badge/$-donate-ff69b4.svg?maxAge=2592000&amp;style=flat">
  </a>
</p>

<p align="center">
  <a href="#key-features">Key Features</a> •
  <a href="#setup">Setup</a> •
  <a href="#usage">Usage</a> •
  <a href="#license">License</a>
</p>


I needed a simple way to parse the otpauth:// uri in vanila JavaScript so that I could use it for a project. The problem was I did not want to install another node module, or grab another huge library and the current OTP library I was using didn't have the a feature to decode the URI. Anyway, so I decided to just create a simple function that returns to me an object with all of the parameters I need and in certain cases tells me if something is wrong.


## Key Features
This "library" (more like a function to be honest), uses the [Google Authenticator Key Uri Format](https://github.com/google/google-authenticator/wiki/Key-Uri-Format) and so these are some sample parameters:
- type (required - something like 'totp' or 'hotp')
- label (required)
- secret (required)
- issuer (optional - but recommended)
- algorithm (optional)
- digits (optional)
- counter (required iff type = 'hotp')
- period (optional)



## Setup

Setup is simple, just import the `parseKeyURI.js` file into your project or just copy the function into your javascript project!


## Usage

Usage is super simple, and you only need one parameter.


```javascript
var obj = parseKeyURI('otpauth://totp/Google:omar@quazi.co?secret=ATQQBI2LLNYDVXADF3V4NSJMRN5I62VF&algorithm=SHA1&digits=6&period=30');
```

The variable `obj` will now contain all of the parameters you need, in the event that the function failed to verify the URI (for example if it was invalid), `obj` will be `undefined`. If parseKeyURI succeded, the `obj` variable should look like this:

```json
{
  type: "totp",
  secret: "ATQQBI2LLNYDVXADF3V4NSJMRN5I62VF",
  period: "30",
  label: "omar@quazi.co",
  issuer: "Google",
  digits: "6",
  algorithm: "SHA1"
}
```
A simple way to verify that parsing the URI worked is like this:
```javascript
if (obj === undefined) {
  alert("Failed to parse Key URI");
} else {
  alert("Success!")
}
```

Note: I know this isn't very "nice", but it worked out well for me and I needed to keep it very very simple. If I missed something or there is a parsing issue, just open up an issue and I will look into it.

## License
The code is MIT Licensed:

```
Copyright 2018 Omar Quazi

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

---

> [Project 52](https://project52.tech) &nbsp;&middot;&nbsp;
> [Omar Quazi ](https://quazi.co) &nbsp;&middot;&nbsp;
> [@quaziomar ](https://instagram.com/quaziomar)
