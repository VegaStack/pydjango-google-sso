# Troubleshooting Guide

### Common errors:

??? question "Admin Message: _**State Mismatched. Time expired?**_"
    This error occurs when the user is redirected to the Google login page and then returns to the Django login page but
    original state are not found. Please check if the browser has the anonymous session created by Django. This error
    can occur if you use `127.0.0.1` instead of `localhost` for your local tests.

??? question "Google show the message: _**The Solicitation from App XXX is Invalid.**_"
    Make sure you have added the correct Callback URI on Google Console. Please remember the trailing slash for this URI.

??? question "My custom css is not working"
    Make sure you have added the correct static files path on your `settings.py` file. Please check the
    [Django documentation](https://docs.djangoproject.com/en/4.2/howto/static-files/) for more details. Make sure your
    path is `static/django_google_sso/google_button.css`. You can also need to setup the `STATICFILES_DIRS` setting in
    your project. Check the Example app below for more details.

??? question "How can I log out Django user if I log out from Google first?"
    If you log out from Google, the Django user will not be logged out automatically - his user session is valid up to
    1 hour, or the time defined, in seconds, in `GOOGLE_SSO_SESSION_COOKIE_AGE`. You can use the `GOOGLE_SSO_SAVE_ACCESS_TOKEN`
    to save the access token generated during user login, and use it to check if the user status in Google (inside a
    Middleware, for example). Please check the [Example App](https://github.com/megalus/django-google-sso/tree/main/example_google_app)
    for more details.

??? question "My callback URL is http://example.com/google_sso/callback/ but my project is running at http://localhost:8000"
    This error occurs because your Project is using the Django Sites Framework and the current site is not configured correctly.
    Please make sure that the current site is configured for your needs or, alternatively, use the `GOOGLE_SSO_CALLBACK_DOMAIN` setting.

??? question "There's too much information on logs and messages from this app."
    You can disable the logs using the `GOOGLE_SSO_ENABLE_LOGS` setting and the messages using the `GOOGLE_SSO_ENABLE_MESSAGES` setting.

??? question "System goes looping to admin after login."
    This is because the user data was received from Google, but the user was not created in the database or is not active.
    To see these errors please check the logs or enable the option `GOOGLE_SSO_SHOW_FAILED_LOGIN_MESSAGE` to see failed
    login messages on browser. Please, make note these messages can be used on exploit attacks.

### Example App

To test this library please check the `Example App` provided [here](https://github.com/megalus/django-google-sso/tree/main/example_google_app).

### Not working?

Don't panic. Get a towel and, please, open an [issue](https://github.com/megalus/django-google-sso/issues).
