% Software Architectures - Assignement 1: Design patterns
% Abdeslam Bakkali Taheri; Vincent Lindivat

# Exercise 1: Find instances of Design Patterns

In this exercise, we had to find instances of design patterns in Jedit's code, Jedit being an open source text editor written in Java.

<!-- TODO say and justify the category (creational, structural, behavioral) -->
<!-- TODO describe the participants (class & method names) -->
<!-- TODO class diagram (only include the necessary elements)-->
<!-- TODO motivation & application of the pattern in this context (don't give a general description of the pattern) -->
<!-- TODO in what way these implementations differ from the original pattern -->

## Singleton
The singleton pattern is categorized as a creational pattern because it ensures that a specific class is **instantiated** only once.

It is often criticized because an instance of a class using this pattern can be used like a global variable. A global variable causes problem for unit testing, because it can be modified by everyone and causes unpredictability in the state of the system. It also introduces coupling with classes using it, which renders them hardly reusable.

While using global variables may be seen as bad practice, and while there are alternatives (e.g. dependency injection), these alternatives may bring drawbacks such as having the code difficult to read, or the intent of the developpers may not be easy to grasp at first glance.

The gist of it is that design patterns should be used with parcimony, and should not be treated like some unquestionable magical spell. They are recipes, and can be adapted and modified to fit more specific problems that a developer encounters. Also, each decision has associated drawbacks, there is no such thing as perfect code.

Here's one example of a singleton implementation found in Jedit's code.

<!-- possible candidates :
    * pluginmgr/PluginManager and showPluginManager() method
    * ServicesManager with getService() method, Descriptor class (which is the singleton in itself) & serviceMap HashMap
    * ReflectManager
    * KillRing
    * ModeProvider works like a singleton
    * Registers.java uses datatransfer/TransferHandler (!not swing TransferHandler)
    * gui/DockableWindowFactory (TODO see why public static **synchronized**) (used by DockableWindowManager & PluginJAR)
-->

## Abstract Factory
* Creational
* ServiceManager
    * "Provide an interface for creating families of related or dependent objects without specifying their concrete classes." -> here we create related objects which are the services
* deviation from original pattern: no abstract class from which the ServiceManager inherits
<!-- TODO see in more details how ServiceManager works -->
<!-- TODO see all the factories in gui/statusbar -->

## Observer
* Behavioral
<!-- possible candidates :
    * BufferListener & BufferUndoListener
    *  PluginManagerProgress which implements ProgressObserver, MirrorList is a subject?
    * RegistersListener & JEditRegistersListener
    * AutoSave is a java.awt.event.ActionListener
    * BrowserListener is a java.util.EventListener
    * VFSDirectoryEntryTable::MainMouseHandler is a javax.swing.event.MouseInputAdapter
    * VFSBrowser uses javax.swing.event.EventListenerList and VFSBrowser::ActionHandler which implements ActionListener & ItemListener
    * HelpHistoryModelListener
    * BufferSetListener & BufferSetAdapter
    * and a shitload of other examples
-->

## Adapter
* Structural
<!-- possible candidates :
    * BufferAdapter
    * BufferSetAdapter
    * JEditVisitorAdapter
-->

<!--
It seems the word Adapter is used differently than waht is described by the pattern. It seems to describe an abstract class implementing an interface, and the methods' bodies are empty. It's a way to bypass the interface, and not enforce the implementation of all the methods... One of the reasons invoked is that the interface may change a lot later because it's still in development. It seems kinda bad, why bother describing an interface if it's not to use it correctly ? And why did this feature got released if it's still a work in progress? In should have stayed in a dev branch.

All that I described above need to be reviewed, because I did not look at the code in details. It's only what I could glimpse by skimming quickly through some classes.
-->

## Visitor
* Behavioral
<!-- possible candidates :
    * visitors folder
-->

# Exercise 2: Recognize Design Patterns
<!-- TODO -->

<!-- guesses
 * memento
 * command ?
 * composite ?
-->

# Exercise 3: Coupling & Cohesion
<!-- TODO -->
<!--
 * high cohesion and loose coopling are preferable + TODO explanations
-->

# References
<!-- TODO -->


# Miscellaneous
The following notes must not be included in the report, there are just some interesting things I noticed after searching information for this assignement.

 * A **nested class** is a member of its enclosing class. Non-static nested classes (inner classes) have access to other members of the enclosing class, even if they are declared private. Static nested classes do not have access to other members of the enclosing class. As a member of the OuterClass, a nested class can be declared private, public, protected, or package private. (Recall that outer classes can only be declared public or package private.) ([source](http://docs.oracle.com/javase/tutorial/java/javaOO/nested.html))

* Resources related to the Abstract Factory pattern :
    * <https://en.wikipedia.org/wiki/Abstract_factory_pattern>
    * <http://sourcemaking.com/design_patterns/abstract_factory>
    * <http://www.tutorialspoint.com/design_pattern/abstract_factory_pattern.htm>
    * <http://www.oodesign.com/abstract-factory-pattern.html> (!!!)
    * <http://www.dofactory.com/net/abstract-factory-design-pattern>
    * "An abstract factory has multiple factory methods, each creating a different product. The products produced by one factory are intended to be used together (your printer and cartridges better be from the same (abstract) factory). As mentioned in answers above the families of AWT GUI components, differing from platform to platform, are an example of this (although its implementation differs from the structure described in Gof)." ([source](https://stackoverflow.com/questions/1673841/examples-of-gof-design-patterns))
    * "Provide an interface for creating families of related or dependent objects without specifying their concrete classes."

* categories of design patterns
    * "Creational patterns are ones that create objects for you, rather than having you instantiate objects directly. This gives your program more flexibility in deciding which objects need to be created for a given case." (wikipedia)
    * "Structural: These concern class and object composition. They use inheritance to compose interfaces and define ways to compose objects to obtain new functionality." (wikipedia)
    * "Behavioral: Most of these design patterns are specifically concerned with communication between objects." (wikipedia)

* On dependency injection
    * http://www.theserverside.com/news/1321158/A-beginners-guide-to-Dependency-Injection
    * http://www.drdobbs.com/tools/dependency-injection-testable-objects/185300375
    * http://tutorials.jenkov.com/dependency-injection/index.html
    * http://www.tonymarston.net/php-mysql/dependency-injection-is-evil.html
