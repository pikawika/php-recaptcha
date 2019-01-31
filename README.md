# PHP driven form reCAPTCHA validation tutorial (With AJAX)

This is a small github repo with a step by step tutorial how to implement a Google invisible reCAPTCHA (v2) to an existing php form. 

We will also discuss how you can implement a callback function to trigger what otherwise would be an AJAX call on your contact.php to (eg) hide a contact form after succesfully sending an email and showing a succes message in it's place.

A working example can be found on my website:
> https://www.lennertbontinck.com/index.php#contact

## Inhoudsopgave

> - [Klant](#klant)


## Developer

| Name     | GitHub                        | Email                               |
| :---     | :---                          | :---                                |
| Bontinck Lennert | [GitHub Lennert](https://www.github.com/pikawika) | [info@lennertbontinck.com](mailto:info@lennertbontinck.com) |

## Current setup

We will be changing an existing contact form which uses AJAX to show a succes message after an email is succesfully send. Our environment before implementing reCAPTCHA looks like this:

- initial form
	- <kbd><img src="assets/before/empty-form.PNG" width="600"></kbd>
- succesfully send 
	- <kbd><img src="assets/before/success.PNG" width="600"></kbd>

## Wanted result:

- Keep the contact form easy to use due to an invisible captcha which requires no input most of the time.
- Use a simple image clicking captcha if user is suspected to be a bot.
- Stop a LOT (almost all) of bots from using our php driven (eg contact) form.
- Hide the ugly reCAPTCHA overlay yet will still be allowed by google by adding our own disclaimer.
- Still trigger the previous mentioned ajax function to hide the contact form and show a succes message.

## Getting the required free reCAPTCHA keys:

- Go to [the Recaptcha admin panel](https://google.com/recaptcha/admin).
- Sign in with a google account if not already logged in. You can have multiple free keys on one account
- You should see a form "register a new site"
	- <kbd><img src="assets/adminpanel/add-new-captcha.PNG" width="600"></kbd>
	- Choose invisible
	- Fill in all of the domains you want to use the current key for
		- eg: lennertbontinck.com 
	- Accept the reCAPTCHA Terms of Service.
- if everything is correct you should see a screen with your
	- Site key
	- Secret key
	- <kbd><img src="assets/adminpanel/keys.PNG" width="600"></kbd>

## Importing the required dependencies (js)

Include the following scripts tag to your html webpage which has the form on it

```html
<!-- ReCAPTCHA  -->
<script src='https://www.google.com/recaptcha/api.js'></script>
```

## Is it allowed to remove the ReCAPTCHA badge in the boddom right corner?

!!! CHECK FAQ IF REMOVING BADGE IS STILL ALLOWED !!!

You will probably have noticed an ugly Recaptcha badge after adding the script tag with the reCAPATCHA API. The badge i'm talking about is the following:

> <kbd><img src="assets/after/badge.PNG" width="300"></kbd>



If we look at google's FAQ we can see it is allowed to remove the captcha badge when and only when we mention the use of captcha with a specific format:

> <kbd><img src="assets/after/removing-badge-allowed.PNG" width="600"></kbd>

## Removing the ReCAPTCHA badge in the boddom right corner

Simply add the following css to your style.css or include it in style tags

```html
<!-- Hide reCAPTCHA badge -->
<style>
    .grecaptcha-badge {
        display: none;
    }
</style>
```



Now add the required usage of reCAPATCHA anywhere near your form where you use the reCAPATCHA, in this example we'll place it underneath the submit button.

```html
<p style="font-size: 9px !important;">This site is protected by reCAPTCHA and the Google
                                    <a href="https://policies.google.com/privacy">Privacy Policy</a> and
                                    <a href="https://policies.google.com/terms">Terms of Service</a> apply.
                                </p>
```



This will hide the badge and show the following subtext on your contact form.

> <kbd><img src="assets/after/empty-form.PNG" width="600"></kbd>

## Used sources

- [Clean html mail to send using php](https://github.com/pikawika/contact-form-mail-template)
- [Recaptcha FAQ](https://developers.google.com/recaptcha/docs/faq)