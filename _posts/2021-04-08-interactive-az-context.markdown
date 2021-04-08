---
layout: post
title:  "Choosing Your Azure PowerShell Context With a Simple Wizard"
date:   2021-04-08 13:37:00 +0200
categories: azure powershell 
---
#### Azure Contexts in Powershell

If you are working with Azure, the probability of you having multiple accounts and subscriptions to work with are very high. If I look at myself, I have a personal account, a business account and my workaccount that I often use everyday. Deploying scripts through Powershell requires you to make sure you are in the right context. Especially with the rise of Azure Lighthouse, where you maybe have access to a lot of subscriptions through one account, a simple mistake is easily made.

#### Switching between accounts

The workflow I previously used for executing Powershell scripts was to Disconnect all accounts, logging in with the right one and setting the right subscription with Set-AzContext. It works, but takes a lot of time. To reduce the time I need for switching between contexts, I wrote a simple script which works as follows:

- Lists all your connected Contexts through Get-AzContext -List
- You choose an account (No input defaults to 0)
- If multiple subscriptions: Lists all the Enabled Subscriptions accessible through the selected account
- If multiple subscriptions: You choose a subscription (No input defaults to 0)
- The context will be set

![image](/assets/img/InteractiveAzContext.gif)

#### How to use it

To access the function everywhere, you can add it to you Powershell profile. By running $profile within powershell you can determine the location of your PowerShell Profile. Prefixing the variable with your favorite editor will open the profile directly. For example:

```powershell
code $profile
```

#### The code
The code can be found at: [stefanpetter/PS-InteractiveAzContext][github-stefan-azcontext]{:target="_blank"}.

This is a quick sketch, but it works very well! If you think the code could more elegant, or you have ideas for functionality, I highly encourage you to improve it!

Thank you for reading!

[github-stefan-azcontext]: https://github.com/stefanpetter/InteractiveAzContext