# OpenRewrite example to migrate Vaadin Bookstore example from Vaadin 23 to Vaadin 24.

## Migrations are pain

Newer version of library or framework that you are using is introducing a breaking change that you now must deal with
modifying your code. Sometimes having to do these modifications is just a risk and additional work for you if you were
happy with the functionality that the current in production version offers and the only reason to update is not to fall
too much behind which will eventually lead into not having support at all.

## Sometimes you get lucky and sometimes you don't

If it's just few compilation errors that are due to renamed method or changed package name, then it is easy to just
rename your calls, and you are good to go again, but when your codebase is large and there are more than just few
changes that you cannot reasonably search and replace, then something like migration automation comes in very handy.

## How to deal situations when you are unlucky

Migration automation could be characterized as being search and replace on steroids. You have more control over how to
modify your code because migration automation tools are understanding your programming language level constructs instead
of just being dumb text replacement.

The tool that we are going to use in this tutorial is [OpenRewrite by Moderne](https://docs.openrewrite.org/).
OpenRewrite is based
on [lossless semantic trees](https://docs.openrewrite.org/concepts-explanations/lossless-semantic-trees) or LSTs, that
holds type information in addition to textual formatting. It is free and open source and there are plenty of 3rd party
migration recipes available.

## In practical terms

This tutorial gives your pointers how to approach migrating your project in automated fashion by using OpenRewrite. This
is not to provide full and comprehensive library of OpenRewrite recipes but more of an idea provocation. We are going to
take older version of Vaadin example application [Bookstore](https://github.com/vaadin/bookstore-example) that is still
using Vaadin 23 and creating OpenRewrite recipe to migrate it to using latest Vaadin 24 version.

In fact the sample application that you see here is the Vaadin 23 version of the Bookstore example and to get the Vaadin
24 version of it you would run OpenRewrite locally.

In a nutshell you need two things or in this case they are added on top of the original Bookstore example already.

- [rewrite.yml](rewrite.yml) file at your project root.
- rewrite-maven-plugin plugin in your [pom.xml](pom.xml#L145) or invoke maven plugin directly from the command line.

This is all you need in terms of how configuration goes. Then you simply run maven mvn rewrite:run and your codebase is
being automatically migrated based on recipe(s) found in [rewrite.yml](rewrite.yml). Console output will list changes
and if you cloned
this as a git repository, you can also see the changes in git uncommited changes where you can compare what kind of
changes were made.

## Takeaways

[rewrite.yml](rewrite.yml) that is included here is no means an exhaustive list of changes between Vaadin 23 and Vaadin
24 but instead
a demonstrative list of what kinds of tasks would a typical migration would include. In usual use cases you would write
[rewrite.yml](rewrite.yml) based on what kind of changes your specific codebase requires. In the example of Bookstore
there is no
migration recipes related to Spring Boot 3.0, so breaking changes of Spring Boot 3 are not addressed. This is because
Bookstore is not using Spring at all.

If you found migration automation appealing in your use case then give it a shot! You may start by taking the example
[rewrite.yml](rewrite.yml) and extend it based on your codebase needs. When your migration effort grows, and you cannot
reasonably to
have just one single atomic migration recipe, you could add more than one and run them individually and do manual
changes in between runs.