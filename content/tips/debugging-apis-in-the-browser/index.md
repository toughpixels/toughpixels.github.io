---
title: "Debugging APIs in the Browser"
date: 2021-03-23T19:09:06-05:00
tags: api, HTTP, browser
description: "You can easily mock API and other network requests for development and debugging using Firefox, the Network Inspector, and the 'Edit and Resend' tool."
---

## Mocking API Network Requests with The Inspector

One difficult part of building an API is mocking and modifying the requests your application will receive. There are lots of tools out there, like [Postman](https://www.postman.com/), but those are heavy tools to use early in the development process or for simple testing. Instead, there is a simple way of copying, editing, and re-running HTTP requests directly in the inspector.

## Firefox!

The Firefox browser [inspector](https://developer.mozilla.org/en-US/docs/Tools) comes bundles with some great developments tools. Two of my favorites are the [CSS grid inspector](https://developer.mozilla.org/en-US/docs/Tools/Page_Inspector/How_to/Examine_grid_layouts) and this API debugging miracle: "Edit and Resend".

##  Network Inspector

If you're a seasoned developer, you might know and love the [Network Monitor](https://developer.mozilla.org/en-US/docs/Tools/Network_Monitor). If you're newer or haven't ever checked it out, I really encourage you to watch a few dozen web requests pass by while looking at the tab. It gives you a lot of insight into how the web works.

##  Edit and Resend

To use this tool, open the Network Monitor tab of your Inspector in Firefox. Make your first HTTP request by visting a URL. In the image, I'm visiting `localhost:8000/api/users/create`, which creates a GET request for that resource.

{{< figure src="API-request-returning-a-405-error-code.png" caption="Making a GET request to my API" >}}

In my application, the endpoint only accepts POST requests, so the application throws an error. Time to break out some `cURL` or `fetch()`, right?  There's an easier solution! I can right click the request, then select `Edit and Resend` to modify the request right in the browser.

{{< figure src="editandresend.png" caption="Locating the Edit and Resend tool" >}}

I changed the HTTP request method to POST, and added some data to the request body.

{{< figure src="edit-request.png" caption="Making any changes to my API request" >}}

Now when I click the send button, I can see that my API is reponding as expected. It's `201` season, friends!

{{< figure src="success!.png" caption="After tweaking, the API handles my request!" >}}

##  Pack It Up and Take It Away!

Once your API request is properly formed in the browser, and your API or application is returning the results you expect, how do you export that request to another application?  Again, the brwowser makes it easy. Right click your working request, then copy it into the format you want. Now you can use your working request anywhere in your code!

{{< figure src="copytoyourfavoritetool.png" caption="Copying my API request for use in my application." >}}