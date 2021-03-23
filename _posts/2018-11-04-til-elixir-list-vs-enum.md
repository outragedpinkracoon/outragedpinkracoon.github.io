---
title: Traversing and Accessing Lists in Elixir
description: A little not about List vs Enum and how traversal of lists in Elixir is different to Ruby.
layout: post
categories: [elixir, programming]
---
I was a little puzzled today that the List module in Elixir has first and last methods, but no way to access any elements in between. Though there are many similarities between Ruby and Elixir, it’s not possible to use the my_list[2] syntax to access elements of a list in Elixir like you do in Ruby.

I wanted to investigate this further I used my recently learned h List command to give me some interesting help about the List module in iex which showed me this:

“This module aims to provide operations that are specific to lists, like conversion between data types, updates, deletions and key lookups (for lists of tuples). For traversing lists in general, developers
should use the functions in the Enum module that work across a variety of data types.”

Ah ha! So it would seem that the Enum module is what I actually want to use for accessing and traversing my list, and actually is a more general use module for various data types.

By typing ​​h List. (notice the ‘.’ there) then tab I can see all of the functions available, such as:

- delete
- replace_at
- starts_with?
- flatten
- insert_at
And so forth, there are around 36 functions in total in my version of Elixir (1.6.4) which are List specific.

Enum however has around 90 functions including:

- empty?
- map
- join
- max
- min
- sort
- slice
- take

And so on, which are applicable to different data types and not just lists. Most importantly I found the at function which allows me to access an element by index! Which lives on Enum and not List because it’s not List specific.

Key learning point: refer to the Enum module for most traversal and transformation activities on a data_type and only use List for very specific functions that only apply to lists.
