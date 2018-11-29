The PEDAC process is one approach to solving programming problems. Its primary goal is to help you identify and avoid pitfalls that you may encounter when you don't code with intent.

P - \[Understand the\] **P**roblem

E - **E**xamples / Test cases

D - **D**ata Structure

A - **A**lgorithm

C - **C**ode

This guide describes a "lighter" version of the PEDAC process that should help you prepare for the upcoming interview assessment. We'll discuss PEDAC in much more detail in a later course.

When given a programming problem, students often jump straight to the coding part. At first glance, this approach seems reasonable. In an interview setting with limited time, you want to solve the problem quickly. Writing an algorithm may seem like an unnecessary use of your limited time, especially when the problem seems simple. However, in this guide, we want to show you that following the PEDAC process saves time and lets you solve **complex** problems efficiently.

Note that we've bolded the word "complex." Some problems, like, writing a method that takes a string and returns its uppercased version are so simple that they don't need a detailed algorithm. However, writing a method that returns all the substrings from a given string that are palindromes is not simple, and following the PEDAC process is crucial to solving the problem in the time allotted.

In this guide, we will focus on the "understand the problem" and "data structure/algorithm" steps of the PEDAC process. We won't worry about the Examples/Test Cases step since we will provide test cases during the first interview assessment. We also won't worry about the Code: most students have sufficient knowledge of Ruby syntax and methods to solve even the hardest problems. Where they run into trouble is understanding the problem and determining an appropriate algorithm.

### P - \[Understand the\] **P**roblem

Understanding the problem has three steps.

1.  Read the problem description.
2.  Check the test cases, if any.
3.  If any part of the problem is unclear, ask the interviewer or problem requester to clarify the matter.

Let's walk through this process for the problem given below:

```ruby
# PROBLEM:

# Given a string, write a method change_me which returns the same
# string but with all the words in it that are palindromes uppercased.

# change_me("We will meet at noon") == "We will meet at NOON"
# change_me("No palindromes here") = "No palindromes here"
# change_me("") == ""
# change_me("I LOVE my mom and dad equally") == "I LOVE my MOM and DAD equally"
```

After reading this problem, some items may need clarification:

1.  **What is a palindrome?**
    You might ask the interviewer to tell you what a palindrome is, and he/she would tell you that it is a word that reads the same forwards and backward.

2.  **Should the words in the string remain the same if they already use uppercase?**
    Here, you can check the test cases. In the fourth test case, the word LOVE already uses uppercase, and it remains uppercase in the solution.

3.  **How should I deal with empty strings provided as input?**
    The test cases frequently answer this question. In this case, test case number 3 provides the answer.

4.  **Can I assume that all inputs are strings?**
    Test cases don't show any non-string inputs, so you should ask whether the inputs can contain non-string values, and what you should do with them. In this problem, we won't worry about non-string values.

5.  **Should I consider letter case when deciding whether a word is a palindrome?**
    Again, test cases don't show any appropriate examples. The interviewer might tell you that the palindrome words should be case sensitive: `'mom'` is a palindrome, `'Mom'` is not.

6.  **Do I need to return the same string object or an entirely new string?**
    This question is one of the most important and most overlooked that you can ask. Typically, while solving problems, students make certain assumptions. One assumption might be that they need to return the same string object. Students often start solving the problem without checking whether the assumption is correct. For this reason, the student might end up losing 10-15 minutes struggling with the wrong problem. In this problem, you should return an entirely new string. **Always verify your assumptions either by looking at the test cases or by asking the interviewer.**

To conclude this part of the PEDAC process, you need to write down what the inputs and outputs for the problem are. You should also describe the rules that you must follow. The rules should encapsulate all the explicit and implicit requirements in the problem. So, you should identify what the explicit requirements are, write them down, and then repeat the process for the implicit requirements:

```ruby
# input: string
# output: string (not the same object)
# rules: 
#      Explicit requirements: 
#        - every palindrome in the string must be converted to
#          uppercase. (Reminder: a palindrome is a word that reads
#          the same forwards and backward). 
#        - Palindromes are case sensitive ("Dad" is not a palindrome, but "dad" is.)

#      Implicit requirements:
#        - the returned string shouldn't be the same string object.
```

### **D**ata Structure / **A**lgorithm

Data structures influence your algorithm, and for that reason, these two steps are often paired. Deciding what data structure to use is generally easy for students: use cases for arrays and hashes, for instance, are generally easy to identify. However, designing the right algorithm is far more challenging. The biggest problem that students have when writing algorithms is providing sufficient detail.

Let's consider another problem. Try to work through the "understand the problem" part of this problem on your own, and write the input, output, and rules for it. We'll provide a solution below. Later, we'll tackle the data structure and algorithm.

```ruby
# PROBLEM:

# Given a string, write a method `palindrome_substrings` which returns
# all the substrings from a given string which are palindromes. Consider
# palindrome words case sensitive.

# Test cases:

# palindrome_substrings("supercalifragilisticexpialidocious") == ["ili"]
# palindrome_substrings("abcddcbA") == ["bcddcb", "cddc", "dd"]
# palindrome_substrings("palindrome") == []
# palindrome_substrings("") == []
```

```ruby
# Some questions you might have?
# 1. What is a substring?
# 2. What is a palindrome?
# 3. Will inputs always be strings?
# 4. What does it mean to treat palindrome words case-sensitively?

# input: string
# output: an array of substrings
# rules: 
#      Explicit requirements:
#        - return only substrings which are palindromes.
#        - palindrome words should be case sensitive, meaning "abBA"
#          is not a palindrome.
```

What data structure could we use to solve this problem? The obvious choice seems to be an array since that's the desired output.

Now, we come to the algorithm part. Look at the algorithm written below.

```ruby
# Algorithm:
#  - initialize a result variable to an empty array
#  - create an array named substring_arr that contains all of the
#    substrings of the input string that are at least 2 characters long.
#  - loop through the words in the substring_arr array.
#  - if the word is a palindrome, append it to the result
#    array
#  - return the result array
```

Does this algorithm look complete to you?

This algorithm resembles those that we often see students write during interviews. It looks complete, but let's think about it for a moment: what is the hardest part of this problem? Is it looping through an array and pushing substrings that are palindromes in the result array? Is it determining whether a substring is a palindrome? Is it something else entirely?

Determining whether a word is a palindrome isn't that difficult for most students. Looping through the array and selecting all the palindromes is relatively easy as well. However, finding all the substrings for a given string can be challenging. The above algorithm doesn't tackle that issue.

When a student starts writing code based on this algorithm, she soon realizes that returning all the substrings won't be easy. Ideally, she should return to the algorithm and try to come up with a way to find all the substrings from the input string. She might also create a new method named `substrings` that returns the array of substrings. In practice, though, the time limitations often lead a student to take a hack & slash approach instead. That almost always leads to spending more time than necessary on the problem or, worse yet, not solving it at all.

Let's now follow the correct approach. We'll return to the algorithm and expand it to include a sub-algorithm that focusses on the `substrings` method we will write.

To find the right algorithm, you can simplify the problem by taking a small concrete example and use it to determine how you will approach the problem. For instance, we can take a short word like `halo` and write all its substrings that are 2 characters in length or longer. The result is `["ha", "hal", "halo", "al", "alo", "lo"]`. Do you see a pattern here?

Beginning with the first letter of the string, `"h"`, we first find all of the substrings that begin with that letter: `["ha", "hal", "halo"]`. As you can see, we're showing a loop at work here: we first return the substring that begins with the first letter and ends with the second, then a substring that ends with the third, and, finally, a substring that ends with the last letter.

Continuing in this vein, we now find all of the substrings that begin with the second letter. That gives us `["al", "alo"]` in addition to the 3 substrings we found before. We repeat this process one last time to get all of the substrings that start with the 3rd letter, `"l"`, which contains one value: `["lo"]`. There's no point in going further - there can be no substrings of at least 2 characters that begin with the last letter.

One way to solve the problem above with code is to use two loops: an outer loop that tracks the index of the first letter of each substring, and an inner loop that tracks the index of the last letter of each substring. Let's try to write that:

```ruby
# - create an empty array called `result` that will contain all
#   the required substrings
# - initialize variable start_substring_idx and assign 0 to it.
# - initialize variable end_substring_idx and assign value of
#   first_letter_idx + 1 to it.
# - Enter loop which will break when start_substring_idx is equal
#     to str.size - 1
#   - Within that loop enter another loop that will break if
#     end_substring_idx is equal to str.size
#     - append to the result array part of the string from
#       start_substring_idx to end_substring_idx
#     - increment `end_substring_idx` by 1.
#   - end the inner loop
#   - increment `start_substring_idx` by 1.
#   - reassign `end_substring_idx` to `start_substring_idx += 1`
# - end outer loop
# - return `result` array
```

The code for this might look like this :

```ruby
def substrings(str)
  result = []
  start_substring_idx = 0
  end_substring_idx = start_substring_idx + 1
  loop do
    break if start_substring_idx == (str.size - 1)
    loop do
      break if end_substring_idx == str.size
      result << str[start_substring_idx..end_substring_idx]
      end_substring_idx += 1
    end
    start_substring_idx += 1
    end_substring_idx = start_substring_idx + 1
  end
  result
end
```

Checking whether the string is a palindrome is easy enough, but we could also write the method for it as well and include it in the algorithm.

```ruby
# - Inside the `is_palindrome?` method, check whether the string
#   value is equal to its reversed value. You can use the
#   `String#reverse` method.
```

```ruby
def is_palindrome?(str)
  str == str.reverse
end
```

Here's the complete **pseudocode** for this problem:

```ruby
# input: a string
# output: an array of substrings
# rules: palindrome words should be case sensitive, meaning "abBA"
#        is not a palindrome

# Algorithm:
#  substrings method
#  =================
#  - create an empty array called `result` which will contain all
#    the required substrings
#  - initialize variable start_substring_idx and assign 0 to it.
#  - initialize variable end_substring_idx and assign value of
#    first_letter_idx + 1 to it.
#  - Enter loop which will break when start_substring_idx is equal
#      to str.size - 1
#    - Within that loop enter another loop which will break if
#      end_substring_idx is equal to str.size
#      - append to the result array part of the string from
#        start_substring_idx to end_substring_idx
#      - increment `end_substring_idx` by 1.
#    - end the inner loop
#    - increment `start_substring_idx` by 1.
#    - reassign `end_substring_idx` to `start_substring_idx += 1`
#  - end outer loop
#  - return `result` array

#  is_palindrome? method
#  =====================
#  - check whether the string value is equal to its reversed
#    value. You can use the `String#reverse` method.

#  palindrome_substrings method
#  ============================
#  - initialize a result variable to an empty array
#  - create an array named substring_arr that contains all of the
#    substrings of the input string that are at least 2 characters long.
#  - loop through the words in the substring_arr array.
#    - if the word is a palindrome, append it to the result
#      array
#  - return the result array
```

The code for this with all the helper methods :

```ruby
def substrings(str)
  result = []
  start_substring_idx = 0
  end_substring_idx = start_substring_idx + 1
  loop do
    break if start_substring_idx == (str.size - 1)
    loop do
      break if end_substring_idx == str.size
      result << str[start_substring_idx..end_substring_idx]
      end_substring_idx += 1
    end
    start_substring_idx += 1
    end_substring_idx = start_substring_idx + 1
  end
  result
end

def is_palindrome?(str)
  str == str.reverse
end

def palindrome_substrings(str)
  result = []
  substrings_arr = substrings(str)
  substrings_arr.each do |substring|
    result << substring if is_palindrome?(substring.downcase)
  end
  result
end
```

Note that you don't need to write all your pseudocode before you start coding. You might write a high-level version of the `palindrome_substrings` pseudocode that omits the details of `substrings` and `is_palindrome?`, write the corresponding code, and then return to the two lower-level methods when you're ready to write them.

There is more than one way to write the `substrings` method. For instance, this denser solution also works:

```ruby
def substrings(str)
  result = []
  0.upto(str.size - 2).each do |start_idx|
    (start_idx + 1).upto (str.size - 1) do |end_idx|
      result << str[start_idx..end_idx]
    end
  end
  result
end
```

The main takeaway is that you need to write a complete algorithm for a problem, including all the hard parts (like our `substrings` method). If you can't write a plain English solution to the problem, you won't be able to code it either. You also don't need any "fancy" methods to solve these problems. Yes, the `Integer#upto` method makes this problem easier to code, but even if you don't know it, you can solve it with simple looping.

In conclusion, practice working through the PEDAC process while solving problems. It may be hard, at first. For simple problems, it might even seem unnecessary, but, stick with it. In time, your process will improve; you'll soon be able to solve difficult problems much more readily.