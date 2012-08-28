---
layout: post
title: "Assembly Build Error"
description: "How to solve the current assembly build error"
category: 
tags: []
---
{% include JB/setup %}

Currently, when attempting to build a project, some users may experience an error. This
error will come up after the command "sbt assembly" has been entered. It will look like
this:

    [error] C:\Users\User\.ivy2\cache\asm\asm-analysis\jars\asm-analysis-3.3.1.jar:META-INF/MANIFEST.MF
    [error] C:\Users\User\.ivy2\cache\asm\asm-tree\jars\asm-tree-3.3.1.jar:META-INF/MANIFEST.MF
    [error] C:\Users\User\.ivy2\cache\asm\asm-util\jars\asm-util-3.3.1.jar:META-INF/MANIFEST.MF
    [error] C:\Users\User\.ivy2\cache\asm\asm\jars\asm-3.3.1.jar:META-INF/MANIFEST.MF
    [error] C:\Users\User\.ivy2\cache\com.google.code.findbugs\jsr305\jars\jsr305-1.3.9.jar:META-INF/MANIFEST.MF
    [error] C:\Users\User\.ivy2\cache\com.google.guava\guava\jars\guava-11.0.1.jar:META-INF/MANIFEST.MF
    [error] C:\Users\User\.ivy2\cache\org.functionaljava\functionaljava\jars\functionaljava-3.1.jar:META-INF/MANIFEST.MF
    [error] C:\Users\User\.ivy2\cache\org.parboiled\parboiled-core\jars\parboiled-core-0.11.0.jar:META-INF/MANIFEST.MF
    [error] C:\Users\User\.ivy2\cache\org.parboiled\parboiled-java\jars\parboiled-java-0.11.0.jar:META-INF/MANIFEST.MF
    [error] C:\Users\User\.ivy2\cache\org.scalaz\scalaz-core_2.9.2\jars\scalaz-core_2.9.2-6.0.4.jar:META-INF/MANIFEST.MF
    [error] C:\Users\User\.sbt\boot\scala-2.9.2\lib\scala-compiler.jar:META-INF/MANIFEST.MF
    [error] C:\Users\User\.sbt\boot\scala-2.9.2\lib\scala-library.jar:META-INF/MANIFEST.MF

We are currently working on fixing this problem. Meanwhile you may use the temporary solution described below.

### Temporary Solution
Open the build.sbt file located in your simulator folder and add the following to the end of it:

    (mergeStrategy in assembly) <<= (mergeStrategy in assembly) { (old) => {
        case n if n.startsWith("META-INF") => MergeStrategy.rename
        case x => old(x)
    }}

Save this and try "sbt assembly"again.



