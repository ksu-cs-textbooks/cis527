---
title: "Windows Web Application"
weight: 50
pre: "10. "
---

{{< youtube  >}}

#### Resources

* [.NET Forum](https://www.jitbit.com/asp-net-forum/) from JitBit
* [SQL Server 2017 Express Edition](https://www.microsoft.com/en-us/sql-server/sql-server-editions-express) from Microsoft

#### Video Transcript

In this video, I'll go through some of the basic steps to install a .NET web application on your server. For this example, I'll be using a trial version of the JitBit .NET Forum software, as it is a good representative example of what it takes to deploy an existing .NET application to your server.

First, I'll need to install Microsoft SQL Server Express Edition to use as the database server for this application. This is a compact version of the full Microsoft SQL Server that is designed for smaller applications and development. You can find a link to download that software in the resources section below this video. Once it has finished installing, you can click **Close** to exit the installer.

Next, I'll need to download the JitBit .NET Forum software from their website. I've provided a link to that software in the resources section below this video as well. Feel free to download that software and follow along if you'd like. However, you won't be able to use JitBit's .NET Forum as your web application for the lab assignment, as I'd like you to demonstrate you can install a web application independently.  

Once I've downloaded the software, I can extract the ZIP file into my downloads directory. When you open that directory, you'll see a file that is very obviously the "README" for this application. In general, many applications will provide installation instructions either via their website or as part of the downloaded software. After all, if customers aren't able to install your software, they are not very likely to use it either. However, that doesn't mean that the installation instructions are always good, nor will they always exactly fit your needs either. So, you'll need to learn how to read the instructions and adapt them to fit your situation.

In this case, I'm going to install this software on top of the existing website `example.local` that I created in the last video. So, I'll adapt these instructions just a bit to fit that setup.

First, I'll need to copy all of these files to the folder I created for this website, which is stored at `C:\inetpub\example`. You'll notice when you do so that it will overwrite the file named `web.config`, so we'll have to deal with that a bit later. Finally, I'll also need to delete the file named `index.html` that I created earlier.

Next, I'll need to convert the existing website to an application in IIS Manager. To do that, right-click the Example website in IIS Manager and choose **Add Application**. There, you'll give the application an alias, as well as the physical path to the files for this application. In addition, you'll need to choose the application pool. Since this application is using .NET 4.0, I can just use the "DefaultAppPool" here. When you click **OK** you should see your application appear in the menu to the left.

Once you've created your application, you'll need to change some file permissions. The official guide from JitBit recommends that you change the user identity used by your application pool, and then assign that account the permissions needed. So, to do that, I'll click on the **Application Pools** option on the left side of IIS Manager, and then right-click the **DefaultAppPool** and select **Advanced Settings**. In that window, find the **Identity** option, and change it to use the **NetworkService** built-in account. Click **OK** to save that setting.

Now, navigate to where you stored the files for .NET Forum, and give the **NetworkService** account full control of the files in the `App_Data` folder. This allows your web application to store files in that folder.

Lastly, you'll need to configure the database connection. That information can be found in the `web.config` file in your application's directory. The instructions give a variety of options for configuring the database, but in general we can just use the default option to use SQL Server Express.

To test your application, clear the cache in your web browser once again, then navigate to `http://example.local`. You should see the application load with the title "Acme Forum" on the page. To test the application, you can log in with the default credentials listed in the instructions, and then create a new forum. If everything is working correctly, it should allow you to do this without any problems.

However, you should hopefully have noticed that it no longer redirected you to HTTPS when you loaded the website. Did you? When we created that URL redirect, it stored the settings in the `web.config` file that was previously located in this folder. So, we'll have to set that up again.

Once you do so, you should test it once again. Hopefully this time it should redirect properly. If you'd like, you can also review the contents of the `web.config` file in the web application's directory to see the additional information added to that file by the URL Rewrite module.

That should do it! You've now configured and deployed your first .NET web application in IIS. This example shows some of the details you may have to deal with when deploying a web application in IIS, but each application is different. In short, you'll always have to read the documentation carefully, but use your own knowledge and experience to adapt the instructions to match your own server's configuration. In addition, don't be afraid to search for additional information on the internet. All of those resources will help you to complete your task. 
