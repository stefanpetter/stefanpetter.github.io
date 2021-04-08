---
layout: post
title:  "Creating a Button to Trigger a DevOps Release From Anywhere!"
date:   2021-03-28 18:55:05 +0200
categories: devops pipelines 
---
18 march, Troy Witthoeft [tweeted][tweet-troy-witthoeft]{:target="_blank"} if someone could make a wifi-connected button that could trigger a Release Pipeline. As a tinkerer with lots of IoT boards laying around, this was a fun little project, so I accepted the challenge!

I started off with a NodeMCU, some wires and a button. The NodeMCU has an ESP8266 WiFi chip on board. 
![image](/assets/img/pushtorelease.png)

After connecting the hardware together, the idea was as follows:
- The NodeMCU has to connect with a WiFi hotspot on my phone. 
- After connecting, the NodeMCU waits for a button push
- When the button is pushed, a release gets triggered through the DevOps API

After a short search, I found the following Docs: [Azure DevOps - Releases - Create][ms-devops-release-api]{:target="_blank"}. This was exactly what I needed! The following challenge was how to deal with the authentication. I was almost certain that a Personal Access Token (PAT) would be the answer here. The solution is to add the following header: 
~~~
Authorization: Basic base64(username:personalaccesstoken)
~~~

After verifying in Postman that the API call worked, it was time to implement the solution on the NodeMCU. For the code I used a lot of available examples in the Arduino Studio combined with a hint of Stack Overflow. Everything went really smooth. The only challenge was calling an HTTPS endpoint using the existing libraries. To make sure that worked I added the SHA1 fingerprint of the dev.azure.com certificate in the code. 
~~~
const char fingerprint[] PROGMEM = "61 66 D0 97 53 63 80 53 D0 FF E5 22 6A 89 9E 7E 3A 92 63 CA";

// Use WiFiClientSecure class to create TLS connection
WiFiClientSecure client;
Serial.printf("Using fingerprint '%s'\n", fingerprint);
client.setFingerprint(fingerprint);
~~~

After some more tweaking, the button worked! It triggered a release with a predefines description which get past in the body of the POST API request.
![image](/assets/img/devopsrelease.png)

I made a video of the result! You can [check it out][tweet-stefan-petter]{:target="_blank"} on Twitter :)

The code for the project is available in Github. It isn't the prettiest code and can really use some extra variables for stuff, but it was just a quick and fun proof of concept: [stefanpetter/C-DevOpsReleaseOnButtonPush][github-stefan]{:target="_blank"}. 

If you have any questions, feel free to contact me on Twitter!

[tweet-troy-witthoeft]: https://twitter.com/Twitt_hoeft/status/1372582974324084739
[tweet-stefan-petter]: https://twitter.com/Stefan_Petter/status/1372836952026853381
[github-stefan]: https://github.com/stefanpetter/C-DevOpsReleaseOnButtonPush
[ms-devops-release-api]: https://docs.microsoft.com/en-us/rest/api/azure/devops/release/releases/create?view=azure-devops-rest-6.0
[ms-devops-release-api]: https://docs.microsoft.com/en-us/rest/api/azure/devops/?view=azure-devops-rest-6.1