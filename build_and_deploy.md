# Build and Deploy

**Use a `.yaml` file to describe your build.**

**Use Azure Dev Ops aka ADO**

**Use ARM (or Bicep [it makes your arm stronger]) to deploy your infrastructure.**

Whatever you think of yaml as a generic syntax it is a text file that is easily added to source control right next to your raw source code.  That alone gives it an advantage over anything that is not in source control next to your raw source code.

Azure Dev Ops is a nice infrastructure for cloud build, and if you are also using Azure, cloud deployments.  I haven't used it but I understand there is tooling to target AWS as well.  If I was using multiple cloud providers I'd give it a look and root for it to win so I have one technology.

When using Azure it is tempting to sit at the portal web site and define your infrastructure, push some code from Visual Studio and suddenly see your work of art live from your <a title="Chrome">favorite browser</a>.  But when it's time to scale out so you have an instance of your app closer to some of your users, and then another site closer to another subset of your users ...  You get the picture.  📹

Take the time to learn ARM, or Bicep, or Terraform or any tool that defines your infrastucture in a set of text files.  Because you can copy a set of files or copy/paste sections if a file to suddenly have another whole instance of your resource in a different physical location.  I will go out on a limb 🌳 and say it's impossible to do that manually.  And even if you do, it's impossible for someone else to repeat.

Besides, when you leave your team, who is going to remember that there is one certificate that has to be copied to an Enterprise Application's certificate store?

Or worse, Azure audit your resources and because the owner is no longer around, unceremoniously just deletes said resources.  Yeah ... Shhhh. It happens.

With ARM you can define all of your infrastructure, certificates, managed identities, configuration, scale percentage, AKS clusters, etc.  Better, if you get whacked by a bad actor or a disgruntled employee you have your git history and ADO pipelines to recover everything quickly.  I would say ARM lets you sleep soundly at night.

Pick a tool and put 100% of your infrastructure into it.  Make sure everyone knows how to and is comfortable with making changes.

[Back](./tooling.md)  [Next](./projects_and_solutions.md)