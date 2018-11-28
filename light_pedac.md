PEDAC process is one approach to solving programming problems. The main goal of this process is to help you identify and avoid pitfalls which you may encounter when you do not code with intent.

P - [Understand the] **P**roblem

E - **E**xamples / Test cases

D - **D**ata Structure

A - **A**lgorithm

C - **C**ode

This guide will give you a "lighter" version of PEDAC process that should help you prepare for the upcoming interview assessment.

When given a problem, most students usually jump straight into the coding part. This approach seems logical at first glance. When you are in the interview setting time is limited and you want to solve the problem as fast as possible. Writing algorithm seems like an unnecessary use of time. However, in this guide, we want to show you that following PEDAC process will, in the long run, actually save you time and enable you to solve **complex** problems in a much efficient way.

Note that the word "complex" is bolded. The reason for this is that simple problems, like, write a method that takes a string and returns its uppercased version are so simple for most students that they usually do not require writing of the algorithm, but, writing a method that returns all the substrings from a given string that are palindromes is not that simple, and following PEDAC process here will help you immensely.

In this guide, we will mostly be focused on "understand the problem" and "data structure/algorithm" parts of the PEDAC process. The reason for this is that on the first interview assessment you will be given test cases and as far as coding part is concerned, we have noticed that most students have sufficient knowledge of Ruby syntax and methods to solve even the hardest problems, and what they lack is problem understanding and/or figuring out the right algorithm for the problem.

### P - [Understand the] **P**roblem

Understanding the problem consists usually of three steps.

1. Read the problem the description
2. Check the test cases if they are given
3. If something is still unclear ask the interviewer (if in the interview setting) to clarify things for you


We will walk you through this process for the problem given below: 

```ruby
=begin
PROBLEM:

Given a string, write a method change_me which returns the same string but with all the words in it that are palindromes uppercased.

change_me("We will meet at noon") == "We will meet at NOON"
change_me("No palindromes here") = "No palindromes here"
change_me("") == ""
change_me("I LOVE my mom and dad equally") == "I LOVE my MOM and DAD equally"
=end
```

After reading the problem some things might still be unclear.

**1. What is a palindrome?**
   You might ask the interviewer to tell you what a palindrome is, and he/she would tell you that it is a word that reads the same forwards and backward.

**2. Should other words in the string remain the same if they are uppercased currently?**
   Here, you might check the test cases and see that in the fourth test case word LOVE is written uppercased and it remained uppercased in the solution as well.

**3. How to treat empty strings as inputs?**
   This question can also be clarified by checking the test cases (test case number 3).

**4. Are we going to have only strings as inputs ?**
   Test cases do not show inputs that are not strings so you might check with the interviewer whether the input can be something other than a string.

**5. Should we consider letter cases when deciding whether the word is a palindrome or not?**
   Again, test cases do not show examples of that, but interviewer might tell you in this case that the palindrome words should be case sensitive.

**6. Do I need to return the same string object or just the same sequence of characters?**
   This question is one of the most important ones. Usually, while solving problems, students make certain assumptions. One of the assumptions might be that they need to return the same string object, to which the answer is no, but, most of the time, a student starts solving the problem without checking whether the assumption was correct or not. For this reason, the student might end up losing 10-15 minutes struggling and trying to solve the wrong problem, until finally, he/she asks the interviewer whether the same string object needs to be returned or not. **The right approach is to check every assumption that you make either by looking at the test cases or by asking the interviewer.**

Finally, you would conclude this part of the PEDAC process by writing what the input and output for the problem are and what are some specific rules.

```ruby
=begin
input: string
output: string (not the same object)
rules: every palindrome in the string needs to be uppercased. (Reminder: a palindrome is a word that reads the same forwards and backward). Treat palindrome words case sensitive ("Dad" is not a palindrome, but "dad" is.)
=end
```

### **D**ata Structure / **A**lgorithm

Data Structure influences your algorithm and for that reason, these two steps are often paired together.

Deciding what data structure to use is usually easy for students, but figuring out the right algorithm has proven to be the most difficult part and usually, the reason for this is that student just doesn't write detailed enough algorithm.

Let's consider another problem. Try to go through the "understand the problem" part of this problem yourself and write input, output, and rules for it. We will provide you with the solution below. Later, we will tackle the data structure and algorithm part.

```ruby
=begin
PROBLEM:

Given a string, write a method `palindrome_substrings` which returns all the substrings from a given string which are palindromes. Consider palindrome words case sensitive.

Test cases:

palindrome_substrings("supercalifragilisticexpialidocious") == ["ili"]
palindrome_substrings("abcddcbA") == ["bcddcb", "cddc", "dd"]
palindrome_substrings("palindrome") == []
palindrome_substrings("") == []
=end
```

```ruby
=begin
Some questions you might have?
1. What is a substring?
2. What is a palindrome?
3. Will inputs be only strings?
4. What does it mean to treat palindrome words case insensitive?

input: string
output: an array of substrings
rules: palindrome words should be case sensitive, meaning "abBA" is not a palindrome.
=end
```

What data structure we could use to solve this problem? The obvious choice seems to be an array.

Now, we come to the algorithm part. Look at the algorithm written below.

```ruby
=begin
Algorithm:
     - initialize new result variable and assign an empty array to it
     - find all the substrings, at least 2 characters long, for a given string and assign it to substring_arr variable
     - loop through the substring_arr array and if the word is a palindrome append it to the result array
     - return the result array
=end
```

Does this algorithm look complete to you?

The algorithm written above is what we usually see students write for similar problems. It looks complete, but let's think for a second what is the hardest part of the given problem? Is it looping through an array and pushing substrings that are palindromes in the result array? Is it maybe determining whether a substring is a palindrome? Or is it something else?

Finding whether the word is a palindrome or not is not that difficult for most students. Looping through the array and pushing all the palindrome substrings is easy as well. But, finding all the substrings for a given string can be quite challenging. What the algorithm above doesn't tackle is how we are going to return all the substrings from a given string.

So, what usually happens is that the student starts writing a code following the algorithm above, and then realizes that returning all the substrings won't be such an easy task. The right approach now would be to return to the algorithm and try to come up with a way to find all the substrings from a given string. The student could also create a new method called `substrings` which would return what is needed. But, in practice, since the time is limited, the student usually tries to hack&slash his way to the solution, which inevitably leads to either spending much more time solving the problem or not solving the problem at all.

Let's now follow, the right approach, return to the algorithm and try to find one for the `substrings` method.

To find the right algorithm for the `substrings` method, you should try to simplify the problem. Take a short word like `halo` and write all its substrings which are greater than 1 character in length(we are not considering 1 letter substrings as for the word to be a palindrome it needs to be at least 2 characters long). Those would be `["ha", "hal", "halo", "al", "alo", "lo"]`. Do you see any pattern here?

The starting letter of each substring is the same, while we loop through the ending letter, which always starts 1 character after the starting letter and goes all the way to the end of the string.

When we arrive at the end of the string with the ending letter, we move starting letter by 1 space to the right, and again loop through the ending letter, which again starts from 1 character after the starting letter, until the end of the string.

This process repeats until the first letter reaches the last character of the string.

One way to solve the problem above with code would be to have two loops. One outer loop which would track the index of the starting letter and inner loop which would track the index of the ending letter.

Let's try to write that.

```ruby
=begin
- create an empty array called `result` which will contain all the required substrings
- initialize variable start_substring_idx and assign 0 to it.
- initialize variable end_substring_idx and assign value of first_letter_idx + 1 to it.
- Enter loop which will break when start_substring_idx is equal to str.size - 1
- Within that loop enter another loop which will break if end_substring_idx is equal to str.size
- append to result array part of the string from start_substring_idx to end_substring_idx
- increment `end_substring_idx` by 1.
- end the inner loop
- increment `start_substring_idx` by 1.
- reassign `end_substring_idx` to `start_substring_idx += 1`
- end outer loop
- return `result` array
=end
```

And the code for this might look like this :

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

Also, checking whether the string is a palindrome or not is easy enough, but we could also write the method for it as well and write that in the algorithm.

```ruby
=begin
- inside of the is_palindrome? method check whether string value is equal to its reversed value. (reverse method can be used)
=end
```

```ruby
def is_palindrome?(str)
  str == str.reverse
end
```

Finally, the complete PSEUDO code for this problem would look like this :

```ruby
=begin
input: a string
output: an array of substrings
rules: palindrome words should be case sensitive, meaning "abBA" is not a palindrome
Algorithm:
     - initialize new result variable and assign an empty array to it
     - find all the substrings, at least 2 characters long, for a given string and assign it to the substring_arr variable (for that we would need another method, called substrings which would return all the substrings from a given array)
     - loop through the substring_arr array and if the word is a palindrome(we could also create a method `is_palindrome?` to check whether the string is a palindrome or not) shovel it into the result variable
     - return result variable

     **substrings** method
      - create an empty array called `result` which will contain all the required substrings
      - initialize variable start_substring_idx and assign 0 to it.
      - initialize variable end_substring_idx and assign value of first_letter_idx + 1 to it.
      - Enter loop which will break when start_substring_idx is equal to str.size - 1
      - Within that loop enter another loop which will break if end_substring_idx is equal to str.size
      - append to result array part of the string from start_substring_idx to end_substring_idx
      - increment `end_substring_idx` by 1.
      - end the inner loop
      - increment `start_substring_idx` by 1.
      - reassign `end_substring_idx` to `start_substring_idx += 1`
      - end outer loop
      - return `result` array

     **is_palindrome?** method
     - check whether the string value is equal to its reversed value. (reverse method can be used)
=end
```

And the code for this with all the helper methods :

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

Note that you do not need to write whole pseudocode before you start coding the solution. You might write the bigger picture algorithm and then write the `palindrome_subsrings` method. But, since you still need two helper methods, you would return to the algorithm and write it for one helper method, `is_palindrome?` for example, and then code that method and test it and finally, you would repeat the process for the other helper method called `substrings`.

The `substrings` method can be solved in many different ways and we will provide another more dense solution below.

```ruby
def substrings(str)
  result = []
  0.upto(str.size - 2).each do |start_idx|
    (start_idx + 1).upto (str.size - 1) do |end_idx|
      result << str[start_idx..end_idx]
    end
  end
  result
```

The main takeaway here is that you need to write a complete algorithm for a problem, including all the hard parts of it (like our `substrings` method from above) because if you can't write in plain English solution to the problem, you will not be able to code it as well. You also do not need to know any "fancy" methods to solve these problems. Yes, knowing `Integer#upto` method would make this problem easier, but even if you do not know it, the problem can be solved with simple looping as we have shown you.

Finally, practice working through the PEDAC process while solving all the problems. At first, it will be hard, and for some simple problems, it might even look unnecessary, but, stick with it. In time, you will become better at it, and you will start solving difficult problems much more efficiently than before.