# Multi-Factor Authentication (TOTP)

# Configuration

[Log into the Warpgate admin UI](https://github.com/warp-tech/warpgate/wiki/Accessing-the-admin-UI) and navigate to `Config` > `Users` > `admin` and click `Add OTP`:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189997866-69094a56-6e2e-469c-bdaf-17adf3fc5149.png">

The QR code shown can now be used to set up a mobile TOTP authenticator app.

Once done, click `Update configuration` to save.

## Credentials policy configuration for SSH & HTTP

To specify 2FA policies for SSH or HTTP sessions, uncheck `Any credential` in the corresponding `Auth policy section` and select all required credentials:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189998135-e623ab08-27a5-4002-b77d-9855ceb1b610.png">
