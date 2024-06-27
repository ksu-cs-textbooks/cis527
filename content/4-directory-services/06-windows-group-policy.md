---
title: "Windows Group Policy"
weight: 30
pre: "6. "
---

{{< youtube p6f41Qq6FBM >}}

#### Resources

* **[Slides]({{% relref "/4-directory-services/06-windows-group-policy-slides.md"  %}})**
* [Group Policy](https://en.wikipedia.org/wiki/Group_Policy) on Wikipedia
* [Group Policy Processing and Precedence](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc785665(v=ws.10)) from Microsoft Docs
* [Group Policy Fundamentals in Active Directory](https://redmondmag.com/articles/2016/01/12/group-policy-fundamentals.aspx) by Troy Thompson in Redmond Magazine
* [Tutorial: The Joys of Windows Server's Group Policies](https://www.infoworld.com/article/3117286/windows-server/tutorial-the-joys-of-windows-servers-group-policies.html) by J. Peter Bruzzese on InfoWorld
* [What is Group Policy in Windows](https://www.howtogeek.com/125171/htg-explains-what-group-policy-is-and-how-you-can-use-it/) from How-To Geek
* [The 10 Windows Group Policy Settings you Need to Get Right](https://www.csoonline.com/article/562485/the-10-windows-group-policy-settings-you-need-to-get-right-2.html) from CSO Online
* [In the Trenches: Eight Tips-n-Tricks for Microsoft Windows Group Policy](https://www.globalknowledge.com/us-en/content/articles/in-the-trenches-eight-tips-n-tricks-for-microsoft-windows-group-policy/) by Mark Mizrahi on Global Knowledge
* [Top 10 Most Important Group Policy Settings for Preventing Security Breaches](https://www.lepide.com/blog/top-10-most-important-group-policy-settings-for-preventing-security-breaches/) by Abhishek Rai on Lepide Blog
* [Group Policy Best Practices](https://activedirectorypro.com/group-policy-best-practices/) by Robert Allen on Active Directory Pro
* [Optimizing Group Policy Performance](https://technet.microsoft.com/en-us/library/2008.01.gpperf.aspx) by Darren Mar-Elia on Microsoft TechNet
* [Group Policy Design Best Practices](https://www.itprotoday.com/management-mobility/group-policy-design-best-practices) by Darren Mar-Elia on ITPro Today
* [10 Windows Group Policy Settings you Need to Tweak](http://techgenix.com/windows-group-policy-settings/) by Benjamin Roussey on TechGenix

#### Video Transcript

One of the major features of Microsoft's Active Directory is the ability to use Group Policy Objects, or GPOs, to enforce specific security settings on any Windows client added to the domain. For large enterprises, this is a major tool in their arsenal to ensure that Windows PCs are properly configured and secured in their organization.

Group Policy can be set at both the local computer level, as well as via Active Directory. The settings themselves are hierarchical in nature, so you can easily browse through related settings when using the Group Policy Editor tool. In addition, GPOs are inheritable, and multiple GPOs can be applied to a group or OU in a domain.

When group policies are applied, they follow this order. First, any policies set locally on the machine are applied, then policies from the Active Directory site, then the global domain itself, and finally any policies applied to the OU containing this computer or user are applied. At each level, any previous settings can be overridden, so in essence, the policies applied at the OU level take precedence over others.

Some examples of things you can control via Group Policy are shown here. You can create mapped drives, which we will see in a later module. You can also set power options, which could be used in an organization to save money by reducing energy usage. In addition, you can use group policy to enforce password restrictions, and even install printers and printer drivers as well.

Let's take a look at one quick demonstration, setting a password policy for the domain. This tutorial is from Infoworld, and is linked in the resources section below the video.

Here I have opened my Windows 2016 Server VM as configured for Lab 4. First, I'll open the Group Policy Management Console, which is available on the Tools menu in Windows Server Manager. Next, I'll find my domain, and right-click it to create a GPO in this domain. I'll also give the GPO a helpful name, and click OK to create it.

Next, I can right-click the policy and choose Edit. In the policy editor, I'll need to dig down the following path:

```
<name>\Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Password Policy
```

In that window, we'll right-click the "Password Must Meet Complexity Requirements" option, and choose **Properties**. Then, we'll enable the setting by checkmarking the box and clicking Enable. You can find more information about the policy by clicking the **Explain** tab at the top.

Finally, once the policy is configured, you'll need to right-click on it once again, and select the **Enforced** option to enforce it on the domain itself.

That's all there is to it! Now, any new password created on this domain must meet those complexity requirements. While you won't have to work with Group Policy for this lab assignment, we'll come back to it in a later module as we work with application and file servers.
