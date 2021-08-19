# intellij-reproducer

Reproduces an issue with Java 11 compilation in IntelliJ IDEA.

A maven project that inherits from `org.jboss:jboss-parent` pom.xml uses the `var` keyword introduced in Java 10.
Despite the fact that maven invoked via a terminal successfully compiles the project, IntelliJ IDEA (Project context menu -> Rebuild...) 
fails to compile the project due to the unknown keyword `var`.

The `jboss-parent` pom.xml defines a property `<maven.compiler.target>1.8</maven.compiler.target>`, 
while this project defines `<maven.compiler.release>11</maven.compiler.release>`, which should effectively override the `<maven.compiler.target>` defined
in the parent pom.xml.

It does not; while defining the `<maven.compiler.release>11</maven.compiler.release>` is sufficient to make code highlighting work, compilation in IntelliJ IDEA
requires also the `<maven.compiler.target>11</maven.compiler.target>` to be directly overriden in this project.

Thus, the code highlighting and compilation are inconsistent in terms of how the `<maven.compiler.release>` influences them. Moreover, the current compilation behavior is inconsitent with maven.



