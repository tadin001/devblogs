---
ID: 2823
post_title: >
  Framework Multi-Targeting for VC++
  Projects
author: Visual Studio Blog
post_excerpt: ""
layout: post
permalink: >
  http://devdevblogs.wpengine.com/blog/framework-multi-targeting-for-vc-projects
published: true
post_date: 2009-11-22 08:11:00
---
**[<img title="Pavan (2)" border="0" alt="Pavan (2)" align="left" src="https://msdnshared.blob.core.windows.net/media/TNBlogsFS/BlogFileStorage/blogs_msdn/visualstudio/WindowsLiveWriter/FrameworkMultiTargetingforVCProjects_E3BC/Pavan%20(2)_thumb_1.png" width="81" height="83" />][1]Short Bio:** Pavan Adharapurapu is a developer on the Visual Studio Project and Build team. As part of VS 2010, he has worked on numerous features of the VC++ project system such as property sheets, filters, property pages, platform and tool extensibility, etc. His long term focus is on developing a "common project system" infrastructure which could be used to quickly build richly featured project systems. Prior to joining the Visual Studio team in 2008, he was working on Workflow technologies in Microsoft Dynamics Axapta. Pavan holds a Masters degree in Computer Science (CS) from the University of California, Los Angeles (UCLA) and a Bachelors degree in CS from the Indian Institute of Technology (IIT), Madras. He lives in Redmond, WA with his wife and loves to play soccer and watch movies in his spare time.

Have you ever wanted to target .NET Framework 3.5 with your C++ application in Visual Studio 2010? If you’ve upgrade your C++ CLR application or created a new one, you will notice that it automatically will target .NET Framework 4.0. However, with a little bit of work it is possible to have your C++ CLR application developed in VS 2010 and targeting 3.5. This blog post will explain just that. Please note that this post is about <u>managed</u> re-targeting for <u>VC++</u> projects as opposed to 

· Managed re-targeting for <u>C#/VB</u> projects (see ScottGu's blog [post][2] for this), or

· <u>Native</u> re-targeting for VC++ projects (Li’s blog [post on the VC++ blog][3] and Soma's blog [post][4]).

I assume that you have a VS 2010 VC++ CLR project (.vcxproj) generated, perhaps, by the Visual Studio Conversion Wizard that you want to re-target to v3.5 framework version. Note that you can see the current framework version targeted by this project by going to the project properties UI and looking under Common Properties > Framework and References for the Targeted framework property (see snapshot below).

[<img title="clip_image002" border="0" alt="clip_image002" src="https://msdnshared.blob.core.windows.net/media/TNBlogsFS/BlogFileStorage/blogs_msdn/visualstudio/WindowsLiveWriter/FrameworkMultiTargetingforVCProjects_E3BC/clip_image002_thumb.jpg" width="467" height="324" />][5]

This field was a drop-down in VS 2008 and was the primary way one could re-target to a different framework version. In VS 2010, it is a read-only field. To re-target in VS 2010, we need to do some work.

First of all VS 2008 SP1 must be installed on your system (you cannot do without SP1). This is a mandatory requirement for targeting framework version 3.5. Installing only the .NET Framework 3.5 redist won't do. C++ tools like cl.exe in VS 2010 are only capable of targeting v4.0. So to target an earlier framework version, we need the tools from that earlier version. And these tools are shipped with VS and not with .NET Framework.

Next, you need to manually edit the project file (.vcxproj) with a text editor (like notepad) and add the TargetFrameworkVersion property (if it is not already there) as shown below. It is recommended that this property be added to the property group labeled "Globals". 

[<img title="image" border="0" alt="image" src="https://msdnshared.blob.core.windows.net/media/TNBlogsFS/BlogFileStorage/blogs_msdn/visualstudio/WindowsLiveWriter/FrameworkMultiTargetingforVCProjects_E3BC/image_thumb.png" width="501" height="267" />][6] 

<p class="MsoNormal">
  <span></span>
</p>

If you use VS IDE itself to edit the project file (you have to first Unload Project and then choose Edit MyProject.vcxproj from the context menu of the project in the solution explorer), you will get the very helpful intellisense (see picture below) that will aid you in the definition of this property.

[<img title="clip_image005" border="0" alt="clip_image005" src="https://msdnshared.blob.core.windows.net/media/TNBlogsFS/BlogFileStorage/blogs_msdn/visualstudio/WindowsLiveWriter/FrameworkMultiTargetingforVCProjects_E3BC/clip_image005_thumb.jpg" width="461" height="145" />][7]

Once this property is defined with the right value, reload the project and verify that the Targeted framework property mentioned at the beginning of this post shows v3.5.

 [1]: https://msdnshared.blob.core.windows.net/media/TNBlogsFS/BlogFileStorage/blogs_msdn/visualstudio/WindowsLiveWriter/FrameworkMultiTargetingforVCProjects_E3BC/Pavan%20(2)_1.png
 [2]: http://weblogs.asp.net/scottgu/archive/2009/08/27/multi-targeting-support-vs-2010-and-net-4-series.aspx
 [3]: http://blogs.msdn.com/vcblog/archive/2009/12/08/c-native-multi-targeting.aspx
 [4]: http://blogs.msdn.com/somasegar/archive/2008/11/21/c-enhancements-in-vs-2010.aspx
 [5]: https://msdnshared.blob.core.windows.net/media/TNBlogsFS/BlogFileStorage/blogs_msdn/visualstudio/WindowsLiveWriter/FrameworkMultiTargetingforVCProjects_E3BC/clip_image002_2.jpg
 [6]: https://msdnshared.blob.core.windows.net/media/TNBlogsFS/BlogFileStorage/blogs_msdn/visualstudio/WindowsLiveWriter/FrameworkMultiTargetingforVCProjects_E3BC/image_2.png
 [7]: https://msdnshared.blob.core.windows.net/media/TNBlogsFS/BlogFileStorage/blogs_msdn/visualstudio/WindowsLiveWriter/FrameworkMultiTargetingforVCProjects_E3BC/clip_image005_2.jpg