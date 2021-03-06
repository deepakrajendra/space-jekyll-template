---
layout: post
title:  "Csharp Generics Part 1"
image: ''
date:   2017-01-08 00:06:31
tags:
- C#
description: ''
categories:
- Learn C# 
---

## Generics! A true super hero.

Before we dive into the concept of Generic lets have a look at what it means as per the dictionary.

**Generic:** characteristic of or relating to a class or group of things; not specific.

**synonyms:**	general, common 

The synonyms up there tells it all.

> A generic is something that is common or something thats generalized.



___


### OK now where does this principle apply to in programming?

Say we have a Library that has a collection of books and another Library of CDs.

	    public class BookLibrary
    	{
        	public void AddBook(Book book)
        	{
             	Console.WriteLine("Book added");
        	}
            
        	public Book this[int i]
        	{
            	get { throw new NotImplementedException();}
        	}
    	}
        
          public class CDLibrary
    	{
        	public void AddBook(CD cd)
        	{
             	Console.WriteLine("CD added");
        	}
            
        	public Book this[int i]
        	{
            	get { throw new NotImplementedException();}
        	}
    	}
        
Here, there is class BookLibrary with
1.Method Add to add a Book.
2.An indexer for returning a book at an index.

The same is implemented for the class CDLibrary.

This code works but this is definitely not a great approach as there is code duplication. The same functionality is being implemented by both the libraries here.

### Have a better approach?

	 public class LibraryObject
    {
        public void Add(Object obj)
        {
            if(obj is Book)						//Check if the object is of type Book
            {
            Console.WriteLine("Book added");
            }
            if(obj is CD)
            {
            Console.WriteLine("CD added");	//Check if the object is of type CD
            }
        }
        public Object this[int i]
        {
            get { throw new NotImplementedException(); }
        }
    }
    
     class Program
    {
        static void Main(string[] args)
        {
            LibraryObject library = new LibraryObject();
            library.Add(new Book());
            library.Add(new CD());
        }
    }

Here we have used the power of the Object class.

**Object class**: Object class is the parent of all the class available in .Net Framework. (Its the root of type heirarchy)

The code has been refined and cut down to single Class with Add method that accepts an Object. Further in the method
a check is made to figure out what was added using **"is"** operator.

The code here looks clean and optimized by wait!
In a realtime scenario if this approach is followed a lot of type casting(Converting obj to Book or CD or viseversa) will be needed that will eventually effect the performance.

Even in another case if a value type(int, float,etc) is passed instead of an object boxing and unboxing comes into play affecting the performance again.

This is the core reason that resulted in the birth our superhero **GENERICS**
____

	public class GenericLibrary<T>
    {
        public void Add(T value)
        {
            Console.WriteLine(value+ "added");
        }

        public T this[int i]
        {
            get { throw new NotImplementedException(); }
        }
    }
    
     class Program
    {
        static void Main(string[] args)
        {
            GenericLibrary<Book> library = new GenericLibrary<Book>();
            GenericLibrary<CD> lib = new GenericLibrary<CD>();
            library.Add(new Book());
            lib.Add(new CD());
        }
    }

**Decoding the code**

1. public class GenericLibrary<T>  //here T represents the Type of input that the class would accept. This is 		    								 assigned at runtime.
2. public void Add(T value)     // T is replaced by the type of value passed to the class.
3. GenericLibrary<Book> library = new GenericLibrary<Book>();  // this object takes the type book.

![cmd1.png]({{site.baseurl}}/_posts/cmd1.png)


So, here we have a single Generic class that can be used to encapsulate all the common functionalities irrespective of the types( value or reference).

### Summary

1. We have learned the reason why the concept of Generics came into existence.
2. How a generic class is implemented.

### Whats coming Up?

In the next article we will be playing around with different features of generics and different Generic collections available in C#.
