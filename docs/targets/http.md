This page explains the process of adding a new HTTP target host to Warpgate and allowing users to connect to it.

# Connection setup

[Log into the Warpgate admin UI](https://github.com/warp-tech/warpgate/wiki/Accessing-the-admin-UI) and navigate to `Config` > `Targets` > `Add target` and give the new HTTP target a name:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189968286-5ceef643-25c5-49e2-9895-360cfce61a9f.png">

Fill out the configuration:

* Target URL: the destination web service, including the protocol (`http://` or `https://`).
* TLS mode: whether to ignore, prefer or require TLS (overrides the URL's protocol).
* Verify certificate: whether to reject untrusted certificates.
* Bind to a domain: link this target to a specific sub-domain of the domain Warpgate is on - see [[HTTP targets on separate domains]]

Example:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189969585-623bbe28-deb6-4884-bcb6-df38d46d372a.png">

The target should show up on the Warpgate's homepage:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189970415-01f48fcb-b0cf-4323-9346-1cdf9000ceb7.png">

# Accessing the target

Users can either access the target by selecting it on the Warpgate's homepage, with a direct URL:

```
https://<warpgate host>:<port>/?warpgate-target=<name>
```

You can also find a copyable URL in the _Targets_ section of the admin UI:

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/189970476-768135f6-80de-451f-86f8-c836e78071de.png">

While the target is active, Warpgate will pass-through all HTTP traffic in this session straight to it. You can return back to the homepage by manually navigating to `/@warpgate`, or by using the injected session menu (shown below). The menu button can be dragged around to stay out of the way and will remember its location.

<img width="500" alt="image" src="https://user-images.githubusercontent.com/161476/177399700-45131120-abe8-4868-b797-1636c9006b7c.png">


# Up next

* [[User authentication and roles]]