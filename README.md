PF4J - JPMS integration
=====================
This project is a proof of concept related to how you can integrate [PF4J](https://github.com/pf4j/pf4j) with Java Platform Modules System that comes with Java 9.

Features/Benefits
-------------------
What I think/feel that are possible:
- a `Module` from JPMS is equivalent with a `Plugin` from PF4J
- read plugin metadata from `module-info.java` (module-info.class), that means to write a custom [PluginDescriptorFinder](https://github.com/pf4j/pf4j/blob/master/pf4j/src/main/java/org/pf4j/PluginDescriptorFinder.java)
- read extensions-points and extensions from `module-info.java`, that means to write a custom [ExtensionFinder](https://github.com/pf4j/pf4j/blob/master/pf4j/src/main/java/org/pf4j/ExtensionFinder.java)

When required, PF4J can be forced to use a single class loader for all plugins (the default is to use a class loader for each plugin) via [DefaultPluginLoader.createPluginClassLoader(Path pluginPath, PluginDescriptor pluginDescriptor)](https://github.com/pf4j/pf4j/blob/master/pf4j/src/main/java/org/pf4j/DefaultPluginLoader.java#L51) (returns the same instance).

**TODO**: add other ideas

PF4J vs JPMS (conceptual)
-------------------
- In JPMS, the syntax for indicating dependency in a module is asymmetric - you export a package, but require
a module. 
- In JPMS you export only some packages from a module.

Possible issues
-------------------
- ~~PF4J uses [SemVer](http://semver.org/) but JPMS not.
A possible solution is to abstract the work with versions in a `VersionManager` (interface) and to have the possibility to inject a custom version manager in `PluginManager`.~~ Resolved by https://github.com/pf4j/pf4j/pull/155.
- find a resource

Resources
-------------------
- [PF4J project](https://github.com/pf4j/pf4j)
- [JPMS very simple demo](https://github.com/decebals/jpms-demo) based on PF4J demo
- [JEP 261: Module System](http://openjdk.java.net/jeps/261)
