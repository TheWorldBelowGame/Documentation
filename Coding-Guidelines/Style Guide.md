# The World Below C# Coding Style

### Table of Contents

1. [Abstract](#abstract)
2. [File Conventions](#file-conventions)
3. [Naming](#naming)
	1. [Classes](#classes)
	2. [Variables](#variables)
	3. [Constants](#constants)
4. [Formatting](#formatting)
	1. [Braces](#braces)
	2. [Parenthesis](#parenthesis)
5. [Documentation](#documentation)

### Abstract

This document describes style guidelines for writing C# scripts in Unity. All code that is committed to the repository should follow these guidelines. This allows us to have a language that is common across all scripts, which ensures that all developers can read the scripts in the codebase. A common style makes it easy to add new people to the team, and reduces ambiguity between different files.

Some of the guidelines listed here are taken from the [Microsoft C# Coding Conventions](https://msdn.microsoft.com/en-us/library/ff926074.aspx), as well as [this weird wiki I found](http://c2.com/cgi/wiki?SelfDocumentingCode).

*NB: This document so far has solely been written by Cooper Riehl, and may be biased towards his preferred style. We can easily modify the document to match style guidelines that work for everyone.*

### File Conventions

If the file contains a script class (i.e the class extends `MonoBehavior`), the class and the file should be named exactly the same. Unity gets really upset if the names do not match. Furthermore, the script class should be the ONLY thing in that file. If another class is needed in a script file, prefer to use a `private class` within the MonoBehavior subclass i.e

```C#
class ScriptThing : MonoBehavior
{
	private class MyPrivateStuff
	{
		int foo;
		
		MyPrivateStuff(int foo)
		{
			this.foo = foo;
		}
	}
	
	MyPrivateStuff bar;
}
```

If the file does NOT contain a script (i.e not a MonoBehavior) then the file SHOULD be named after one of the classes in the file. Ideally, one file will only ever contain one class anyways, but there are exceptions.

### Naming

Names should always be descriptive enough for someone to infer what the object does just by looking at it. Variables don’t need to be 80 characters long and take up an entire line, but if you have the choice between a four-word name and a two-word name that is less descriptive, prefer the longer one. This will save time and headaches in the long run. Example:

```C#
public class PSB {} // What does PSB stand for? This is a bad name.
public class PlayerStateBase {} // Much better! Now we know this class is the base class for all player states.

int count;	// What is this counting? Who knows!
int numCycles;	// Now we know this is counting the number of cycles
int numWashCycles	// Even better, we know what KIND of cycle is being counted.
```

##### Classes

Classes should be named using camel case with a capitalized first letter (ex. `MyClass`, `BaseClass`, `LongClassName`).

##### Variables

Variables should be named using camel case with a lowercase first letter (ex. `myVariableName`, `fooBarBaz`).

**A note on Hungarian notation:** don't use it. It's outdated and archaic, and Visual Studio lets us see the type of a variable just by hovering over it, so it's also pointless. Variable names like `m_piSisterObjectID` are just confusing and make the code muddy. `sisterObjectID` tells us exactly what we need to know, and the rest should be inferred from the editor.

##### Constants

Generally, constants are written either in `ALL_UPPERCASE_WITH_UNDERSCORES` or with a leading 'k' as in `kConstantWithoutCapsLock`. We will prefer the latter, since the former looks gross.

*NB: this is also a bit of a carry-over from C++, since C macros are traditionally written in CAPS_LOCK. This makes it hard to differentiate between a CAPS_LOCK_CONSTANT and a CAPS_LOCK_MACRO, so the leading 'k' is preferred.*

### Formatting

##### Braces

For namespaces, classes, enums and methods, prefer K&R style braces (i.e braces on their own line). For everything else, prefer opening braces on the same line as the statement. Closing braces should always be on their own line.

##### Parenthesis

Parenthesis should generally be on the same line as a statement. In the case of very long statements, parenthesis can follow the same rules as braces above. Example:

```C#
void ShortMethod(int singleParameter);

void ReallyLongMethodWithLotsOfParameters(
	int reallyLongParameterName,
	ReallyLongTypeName anotherLongParameterName
) {
	// ...
}
```

### Documentation

A developer should be able to tell what the code is doing just by looking at it. This is made possible through the principles of *self-documenting code* and *commenting*.

##### Self-Documenting Code

Ideally, code should be written in such a way that anyone who looks at it will understand how it works with minimal effort. Self-documenting code helps us achieve that effect by removing unnecessary comments, and keeping comments that help us actually understand the code. There are a few basic guidelines we can follow to help reduce comments and actually make the code more readable:

* **Use descriptive variable names.** Anyone looking at a variable should be able to tell what that variable's purpose is, solely by the name.
* **Follow guidelines for code spacing.** Code that is smushed together with few spaces becomes unreadable very quickly. Equations that are separated to a readable degree go a long way towards maintaining readable code, which in turn allows us to more easily see what is happening in the code.
* 
