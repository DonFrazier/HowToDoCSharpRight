# Projects and Solutions

**Circular references are not allowed so plan carefully.**

**Respect your choices.**

**Separate project by presentation, business logic and data layers in most cases.**

**A base project for domain-specific objects can be useful at all levels.**

**Enable Nullable**

**Use project using declarations.**

**Treat Warnings as Errors**

Every coding assignment I've worked on has been made up of multiple projects.  These projects tend to self-distribute into the familiar presentation, business logic and data layer pieces.

This distribution helps enforce the rules about the flow between presentation, business logic and data.  The presentation layer usually has a reference to the business.  The business logic holds a reference to the data layer.  So the presentation layer is force to get data only for some business motion from the user.

At each layer the objects that flow between the layers may mutate.  Properties that are only relevant to the UI rarely need to flow all the way to the data layer.  Similarly data properties that are of no  interest end users may be 100% maintained by the data layer.  For example creation date, last updated by user, last update date are often automagically maintained by the data store.  If they leave the data layer at all, it is usually only for information purposes and no allowance is made for the user to edit.

Each layer knows about its own objects that it uses exclusively and about the object in the layer immediately below.  For example the presentation layer keeps its state and the business layer has no need to know how the UI works.  But when presentation needs call business logic it needs to know how to ask correctly.  Presentation takes its version of the data, turns it into something the business layer understands and makes a request.  The business responds and the presentation knows how to turn the response into something meaningful to the user.  It should be obvious that objects that sit on this boundary live in the business project.

Similarly, business needs to know to talk with data.  Data defines its language at its layer.

It may seem inefficient to translate the objects as they enter and exit each layer but this separation enables each layer to change internally while keeping its external interface unchanged.  Resist the urge to share objects across all layers.

You will probably wind up with models at each layer.  It can be helpful to separate the models themselves into one (or more) projects.  Immutable objects are nice in many ways and should be tried as the first choice in most cases.

When you need to change something, there should be a mutator that can create a new object with the updated properties.  Use the C# [record](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/tutorials/records) structure to facilitate this.

Separating object lifetime and state change into factory, accessor and mutator classes can help keep even very large projects organized.  A project for each of these at the presentation, business logic and data layers still winds up with a lot of projects.  Even so if you adhere to these boundaries it should be obvious which projects are available to the layer above them.

There is one category of projects that may be useful and may be referenced by any other project.  This is your project for your domain models.  Just as C# defines data types like int, string and bool that are used every where, your application has objects that need to behave the same everywhere.  See [Primitive Obession](./primitive_obession.md) for more details.

Nulls are not evil but they are problematic.  In your .csproj files enable the [Nullable](https://docs.microsoft.com/en-us/dotnet/csharp/tutorials/nullable-reference-types) option so the compiler will automagically warn you about possible null references.  This is one of the best new language features in some time.  Use it every where.  There is also an option to enable it file by file.  If you are creating new classes, consider including it with the directive.

Be careful with the `latest` version of C# by setting `<LangVersion>` since it may use features not installed on your platform.  My recommendation is to set this to `default` unless you have a reason for something else.  If you choose a specific version chances are no one will ever change it and your project will be locked into that level forever.

[Implicit Usings](https://learn.microsoft.com/en-us/dotnet/core/tutorials/top-level-templates) can also reduce the boilerplate at the top of a file.  I think this option will give way to the project declaration in larger projects but it is useful for your one-off experiments.

Keep a clean build by treating warnings as errors.  1,000 warnings in a build hide issues that the compiler thinks you should know about but that are not necessarily errors.  If you introduce a new one the existing horde will obscure it.  Clean builds should be a priority and this option helps keep questionable code out of the deployed code.

```
<PropertyGroup>
    <Nullable>enable</Nullable>
    <LangVersion>default</LangVersion>
    <ImplicitUsings>enable</ImplicitUsings>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
    <WarningsAsErrors />
</PropertyGroup>
```

Move the namespace `using` declarations to your project file.  You can include static usings globally.  I like to include `System.String` just so I can use `IsNullOrWhitespace(somestring)` and write just a bit less code. Be aware that you may still have conflicts and have to fully qualify a static method name.  For example System.Guid also has an Empty() property that conflicts with System.String when used like this.

Note you can also include global aliases for types.  This is another very nice feature that has been elevated from per-file to per-project.  If you have long type names consider adding shorter global aliases for them in the .csproj file.

This is also helpful if you have objects in different .net namespaces that share the same name.  Define project-wide aliases to help clarify which ***Part*** is the ***Part*** that is the ***Part*** in the current scope.
```
  <ItemGroup>
    <Using Include="System.Linq" />
    <Using Include="System.Text" />

    <Using Include="System.String" Static="true" />

    <Using Alias="u32 Include="System.UInt32" />
    <!-- Parts is Parts except when it is not always Parts -->
    <Using Alias="FooPart Include="My.Company.Feature.Data.Foo.Part" />
    <Using Alias="BizPart Include="My.Company.BusinesssLogic.Part" />
    <Using Alias="UIPart Include="My.Company.UserInterface.Model.Part" />
  </ItemGroup>
```

move to primitive obsession section.
The primitives project should have no dependencies, including nuget or other package dependencies.

An easy example is something like Person that has a first name, middle name and last name.  There are rules about how long your data layer allows names to be, maybe these differ between first, middle and last.  Rather than just use strings for First, Middle and Last define a type for these name parts and use them instead of making them strings.  I'll discuss this more in 


[Back](./build_and_deploy.md)  [Next](./coding_style.md)