+++
date = "2023-03-20"
title = "Nullable Reference Types in C#"
tags = ["C#", ".Net"]
categories = ["Development"]
+++

C# is a popular programming language that is widely used in the development of various applications. Microsoft has been working hard to make C# more robust and feature-rich, and one of the additions to the language (added in C# 8) are the nullable reference types. The C# nullable references feature allows developers to better control `null` values and handle null reference exceptions.

In this blog post, we'll explore C# nullable references in detail, including what they are, why they're important, and how to use them in your code.

# What are C# Nullable References?

Before we dive into the details of nullable references, let's first clarify what we mean by "nullable". A nullable type is one that can have a `null` value. In C#, most types are not nullable by default, meaning that they cannot be assigned a `null` value. However, nullable types can be declared using the `?` modifier, which indicates that the type can be assigned a `null` value.

Nullable references in C# take this concept a step further. With nullable references, the language allows developers to annotate reference types as nullable or non-nullable. When a reference type is annotated as non-nullable, the compiler enforces the rule that the variable must always be assigned a non-null value. If you try to use the variable without assigning it a value first, the compiler will generate a warning.

# Why are Nullable References Important?

The main advantage of using nullable references is that they can help prevent `null` reference exceptions (NREs). In C#, an NRE occurs when you try to dereference a `null` reference. This can cause your application to crash, and tracking down the cause of the exception can be time-consuming and frustrating. By using nullable references, you can catch these errors at compile time, before your code ever gets executed.

Another benefit of nullable references is that they can help make your code more self-documenting. By annotating your reference types as nullable or non-nullable, you make it clear to other developers what the expectations are for that variable. This can help reduce confusion and make your code easier to understand and maintain.

# Using Nullable References in C#

Now that we understand what nullable references are and why they're important, let's take a look at how to use them in your code.

## Enabling Nullable References

Before you can start using nullable references in your code, you need to enable the feature. To do this, you need to add the following line to your project file:

```xml
<Nullable>enable</Nullable>
```

This tells the compiler to enable nullable references for your project.

## Annotating Reference Types

Once you've enabled nullable references, you can start annotating your reference types as nullable or non-nullable. To annotate a reference type as non-nullable, you simply omit the `?` modifier when declaring the type:

```csharp
string myString = "Hello, world!"; // non-nullable string
```

To annotate a reference type as nullable, you add the `?` modifier:

```csharp
string? myNullableString = null; // nullable string
```

In the above example, we've declared a nullable string variable and assigned it a `null` value. Note that if you try to use this variable without first assigning it a value, the compiler will generate a warning.

## Handling Nullable Values

When you're working with nullable reference types, you need to be careful when accessing their values. If you try to access the value of a nullable reference type that is currently `null`, you'll get a null reference exception.

To avoid this, you can use the null-coalescing operator (`??`) to provide a default value if the nullable reference is `null`:

```csharp
string? myNullableString = null;
string myNonNullableString = mynullableString ?? "default value"; // myNonNullableString is "default value"
```

In the above example, we're using the null-coalescing operator to assign a default value to `myNonNullableString` if `myNullableString` is `null`.

You can also use the null-conditional operator (`?.`) to safely access members of a nullable reference type. This operator allows you to access a member of an object only if the object is not `null`:

```csharp
string? myNullableString = null;
int? length = myNullableString?.Length;
```

In the above example, we're using the null-conditional operator to get the length of `myNullableString` only if it is not `null`. If `myNullableString` is `null`, `length` will also be `null`.

# Conclusion

We've explored C# nullable references, including what they are, why they're important, and how to use them in your code. By using nullable references, you can catch `null` reference exceptions at compile time, make your code more self-documenting, and improve the overall robustness of your applications.

While nullable references may take some getting used to, they're a powerful tool that can help you write better, more reliable code. So if you haven't already, be sure to give nullable references a try in your next C# project!

