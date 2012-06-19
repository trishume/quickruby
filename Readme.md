# QuickRuby

QuickRuby is a ruby DSL designed for programming contests such as the Google Code Jam, CCC and ECOO.

In my experience, there are three things that are very important when it comes to writing programming
contests:

1. Knowing how to solve the problem
2. Coding it, *fast*
3. Getting the damn thing to work after you have coded it. (AKA debugging)

It is hard for a programming language to help with the first one but I feel that the other two
problems could be made much easier with the help of a special programming language and tools.

I am working on a series of projects that I think will help with the last two problems.
The first one is the QuickRuby framework. Not only do I think it will help me code solutions
faster but the structure will allow debugging tools to more easily understand the code.

## Example program

Here is an example of what a program written with QuickRuby would look like:

```ruby
# sample test case for debugging
testcase <<DATA
5.35 3 3 stuff 7 8 9
xox
oxo
xox
DATA
# debugging data file
testinput "test1.txt"
# data file for real run
realinput "DATA1.txt"
# helper functions accessible from other bits
helpers do
  def dist(p1,p2)
    Math.hypot(p1[0]-p2[0],p1[1]-p2[1])
  end
end
# solves a single test case, handy parsing functions are pre-defined
# input and out are IO objects. num is the test case number
solvecase do |input,out,num|
  # gets a line and creates variables and converts types based on the names
  # f=float i=integer w=word  type(+|:)name  ':' gets one '+' consumes many
  getparams "f:maxdist i:width i:height w:wordparam i+nums"
  mat = getcharmat(height) # == mat=[];height.times {mat<<input.gets.chars.to_a}

  # do calculations and stuff...
  dp wordparam # debug print
  sum = nums.inject(:+)
  outp "Sum: #{sum}" # prints to output

  diagonal = dist([0,0],[width,height])
  dline [0,0],[width,height] # used for visual debugging of a line
  lessmore = diagonal < maxdist ? "less" : "more"
  outp "Diagonal: #{diagonal} - #{lessmore} than the max distance of #{maxdist}"

  # find average exes per row of matrix
  dmat mat # visual debugs a matrix
  exsum = 0
  mat.each do |row|
    exes = row.count('x')
    exsum += exes
  end
  exavg = exsum / mat.size.to_f
  outp "Average exes: #{exavg}"
end
```


