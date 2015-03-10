---
layout: post
title: Publishing Reusable Code on Nuget
excerpt: "Straight forward instructions for publishing packages on Nuget."
tags: [nuget, package manager, open source]
modified: 2015-01-24
comments: true
---

These days if your project is not using open source code you are either living under a rock or under very strict project requirements. This post highlights how easy it is to publish you open source package to Nuget with ASP.NET 5 and Visual Studio 2015.

The _Roslyn_ compiler by default will be compiling into memory to keep your builds as fast as possible, however we need output we can publish. Open up the properties of your application and go to the build tab. Make sure "Produce outputs on build" is checked.

![produce outputs property](./images/properties-build-outputs.png "Produce Outputs on Build")

This will make sure the successful build creates a NuGet package (.nupkg) in the Debug or Releases directories.

![nuget nupkg package](./images/nupkg.png "NuGet Nupkg Package")

The package can be opened and edited with the [NuGet Package Explorer](http://npe.codeplex.com/) to make sure the details are correct before publishing.

To publish the package login to your account at [https://www.nuget.org/](https://www.nuget.org/) and click on the _Upload Package_ link in the menu bar. Select and upload your .nupkg package, edit any details and submit.

![nuget upload](./images/nuget.png "NuGet Upload")

That's all there is to it. Creating and publishing reusable packages in .NET 5 with Visual Studio 2015 is very straightforward and painless for simple packages. For advanced packages check the documentation [here](http://docs.nuget.org/)
