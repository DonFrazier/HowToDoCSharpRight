# Projects and Solutions

**Circular references are not allowed so plan carefully.**
**Respect your choices.**
**Separate for presentation, business logic and data layers in most cases.**
**A base project for domain-specific objects can be useful at all levels.**

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

The primitives project should have no dependencies, including nuget or other package dependencies.

An easy example is something like Person that has a first name, middle name and last name.  There are rules about how long your data layer allows names to be, maybe these differ between first, middle and last.  Rather than just use strings for First, Middle and Last define a type for these name parts and use them instead of making them strings.  I'll discuss this more in 


[Back](./build_and_deploy.md)  [Next](./coding_style.md)