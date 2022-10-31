# Hiding things

To facilitate unit testing is it helpful to hide things external to your code.  Things like
* Everything on the network
* Everything on the computer besides the running code
* Security, privileges, permissions
* The current user
* The operating system.
* The current time

## Network
The network is notoriously unreliable.  You do not want unit tests failing because a network resource is not available.  This is well understand and most network resources have well-defined APIs described by interfaces.  Almost anything with an interface is easy mock.  Design your own services around interfaces and you should be able to test things easily.

I think the most important thing to define in network resources is who performs retry.  If your service performs retry I think it is always a good idea to provide a way to turn off retry.  In a system, there should be clear understanding of which layer(s) perform(s) retry.

In .net I recommend using cancellation tokens end to end so the caller can perform timeout when it needs to and signal any outstanding calls that they are no longer needed.

Unit tests should be able to test the business code without leaving the machine.

## Machine
The file system is likely the most common external resource used.  While some classes implement interfaces most classes deal with real objects.  Wrapping the file system behind an interface can simplify testing.  Unit tests should be able to mock both the success and failure paths without requiring any external files.

Having a nice FileSystem interface also standardizes things like path separators, case sensitivity, path lengths, valid characters for file and directory names.  It is also a chance to simplify the names spaces to a single interface.  THere is a rich set of interfaces but sometimes it is nice to just use a standard CRUD interface that follows best practices.




[Back](./coding_style.md)  [Next](./primitive_obession.md)