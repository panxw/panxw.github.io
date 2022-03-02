---
layout: post
title: "关于APT，Gradle自定义插件总结"
date: 2022-02-28 20:05:01
category: android
tags: [APT, Gradle, 自定义插件]
---

APT ，全称Annotation Processor Tool，注解处理工具。是java包的工具。  
因此创建自定义Process时，要新建java-library模块，并在代码中继承AbstractProcessor，重新getSupportedAnnotationTypes和process方法。  
在process方法中，查找要处理的解析类，根据注解参数，生成相应的java代码。  

在生成java代码的时候，可以利用JavaPoet提高效率，它提供了很好的封装，使用方便，最重要的是，可以自行import依赖的类。  
先用APT，在gradle编译阶段，可以生成java代码。像Eventbus, Bindview等基本都是借用了apt达到相应的目的。  


Gradle自定义插件，则主要是在class文件转化成dex之前，可以利用自定义插件，对字节码进行修改。  
通常我们自定义插件，可以直接创建buildSrc或独立的plugin插件模块。在插件中，根据要求实现Plugin接口，在apply方法中，完成自定义Transform的注册。  
对字节码修改，则需要在自定义Transform的transfrom方法中进行，需要遍历所有jar包及目录。  
通常还要借助ASM库，用它提供的修改字节码的方法，完成字节码插桩会相对轻松点。  


无论是APT还是自定义插件，按一定的套路操作即可。  
APT关键是集中在解析注解，利用JavaPoet API编写符合需求目的的动态代码。  
自定义插件，更多的是考虑怎么插入需要的字节码，对字节码的熟悉，以及对ASM工具的使用。  

相对来说，APT更适合大多数人操作。  
