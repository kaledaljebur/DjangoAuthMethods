Django REST Framework (DRF) supports several types of authentication out of the box, and you can also implement custom authentication methods. Here are the main types of authentication supported:

1. Token Authentication
* Description: Each user is associated with a unique token, which is used to authenticate API requests. The client includes the token in the `Authorization` header with the prefix `Token`.
* Use Case: Suitable for mobile apps or any scenario where the client can securely store the token.
Setup:
    * Add `rest_framework.authtoken` to `INSTALLED_APPS`. 
    * Run `python manage.py migrate`. 
    * Use `TokenAuthentication` in your DRF settings or views.
2. Session Authentication
* Description: Uses Django's built-in session framework. Typically used for browser-based clients where the session ID is stored in a cookie.
* Use Case: Suitable for web applications that already use Django's session management.
* Setup: Ensure the Django session middleware is enabled.
3. Basic Authentication
* Description: Encodes the username and password in the `Authorization` header of each request.
* Use Case: Useful for testing or when security is not a concern. Avoid using it in production without HTTPS.
* Setup: Use `BasicAuthentication` in your DRF settings or views.
4. OAuth2 Authentication
* Description: Uses OAuth2 protocol to handle authentication via a third-party provider or your own OAuth2 server.
* Use Case: Useful for scenarios requiring delegated access or third-party login systems.
* Setup:
    * Use libraries like [django-oauth-toolkit](https://django-oauth-toolkit.readthedocs.io/) or integrate with external providers.
5. JWT (JSON Web Token) Authentication
* Description: Issues a signed JWT to the client, which is included in the `Authorization` header with the prefix `Bearer`.
* Use Case: Common for stateless authentication in modern APIs.
* Setup:
    * Use third-party libraries like [djangorestframework-simplejwt](https://django-rest-framework-simplejwt.readthedocs.io/) or [django-rest-framework-jwt](https://github.com/jpadilla/django-rest-framework-jwt).
6. Custom Authentication
* Description: Define your own logic for authenticating users by extending `BaseAuthentication`.
* Use Case: Suitable for specialised requirements not covered by existing authentication methods.
* Setup: Implement a custom authentication class and include it in the `DEFAULT_AUTHENTICATION_CLASSES`.
7. Remote User Authentication
* Description: Uses Django’s `RemoteUserBackend` to authenticate users based on external authentication systems like Apache's mod_auth.
* Use Case: When integrating with enterprise-level authentication systems.
* Setup: Enable the `RemoteUserMiddleware` and configure the authentication backend.
8. API Key Authentication
* Description: Issues an API key for each client, which is sent with requests for authentication.
* Use Case: Suitable for server-to-server communication or when you need to identify different applications consuming the API.
* Setup:
Use libraries like [django-rest-framework-api-key](https://florimondmanca.github.io/djangorestframework-api-key/).
9. Combining Authentication Methods
You can combine multiple authentication classes in your settings:

In settings.py:
```
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.BasicAuthentication',
        'rest_framework.authentication.TokenAuthentication',
    ],
}
```
DRF will attempt to authenticate the user using each method in order.