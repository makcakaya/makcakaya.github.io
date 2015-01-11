---
layout: post
title: "Mutants in your code"
date: 2015-01-11 18:41:53 +0200
comments: false
categories: c#
keywords: immutable, object, mutabilty 
description: Ensuring some field or variable is assigned only once. 
---

Immutable objects are very popular in concurrency models because immutable objects are naturally thread safe because the state an object cannot be corrupted by multiple threads. As C# developers we can also benefit from immutability. C# has a keyword just for that, *readonly*. We can also utilize readonly property mechanism with private setters.

{% codeblock lang:csharp %}
// A field assigned in declaration statement
private readonly int _num = 20;

public MyClass(int num)
{
    _num = num; // Assign in constructor
}

// Use a readonly property
public int Num
{
    get{ return _num; }
    private set{ _num = value; } // Or you just don't introduce a private setter
}
{% endcodeblock %} 

<!-- more -->

These are all good approaches but they don't accompany you to the depths of API design hell! From now on, I will approach the notion of immutability from another perspective. Classical definition of *immutable object* says that the object's state is not changeable after it has been initialized. I find it valuable to be able to change the state of an object after it has been constructed but only once.

*readonly* keyword ensures that a field can only be assigned where it is declared or in the relevant constructor(static or instance). What if I want a field to be assigned even after it has been instantiated but ensured to be assigned only once? 

Readonly properties are phenomenal, I use them everywhere appropriate. But they too don't solve the problem. Take a look at the code:

{% codeblock lang:csharp %}
public MyClass()
{
    ...
    Initialize();
}

private void Initialize()
{
    _num = 11; // DON'T EVEN THINK ABOUT CHANGING THIS VALUE!!!
    ...
}

// What if someone else (Better Developer) comes and adds a method to your library like this
// He has enabled users to assign a new value while you assert that you only assign once
public void SomeMethod()
{
    ...
    _num = 12; // I like 12 better(Better Developer)
    ...
}
{% endcodeblock %} 

Readonly property mechanism fails you here, because both the private setter and the backing field is always there to change the state of the object. 

What do we do now? We can add an extra *boolean* field that keeps track of the assignment. But then if you have 5 fields that should be assigned only once, you have to add 5 extra fields to back them up and it would clutter the class definition. 

I've defined a very basic generic type called *WriteOnce<T>* for this purpose. Check it out:

{% codeblock lang:csharp %}
    /// <summary>
    /// Objects of this class limits their values to be assigned only once.
    /// After assigning the value the first time, any further assignments will throw exceptions. 
    /// </summary>
    /// <typeparam name="T"></typeparam>
    public sealed class WriteOnce<T>
    {
        #region Field

        private T _value;
        private bool _isLocked = false;

        #endregion

        #region Properties

        /// <summary>
        /// Gets/Sets the value
        /// Throws ReadonlyException if assigned for more than once
        /// </summary>
        public T Value
        {
            get { return _value; }
            set
            {
                if (this.IsLocked) { throw new WriteOnceException(); }

                _value = value;
                _isLocked = true;
            }
        }

        public bool IsLocked
        {
            get { return _isLocked; }
        }

        #endregion

        #region Ctor

        public WriteOnce() { }

        public WriteOnce(T value)
        {
            this.Value = value;
        }

        #endregion
    }
{% endcodeblock %}

*WriteOnce* ensures that as the developer of a class, you assign a field only once. If you plan to enable users assign values to fields but again only once, you can do that too. Now using this type I can define the previous class like this:

{% codeblock lang:csharp %}
public class MyClass
{
    // Will throw WriteOnceException if assigned more than once
    private readonly WriteOnce<int> _num = new WriteOnce<int>();

    public int Num
    {
        get { return _num.Value; }
        set { _num.Value = value; } // Or don't provide a setter if you like
    }

    private void Initialize()
    {
        ...
        this.Num = 11;
    }
}
{% endcodeblock %}
