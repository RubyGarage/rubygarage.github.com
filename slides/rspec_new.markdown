---
layout: slide
title:  RSpec
---

# RSpec

---

# The value of tests

One of the most valuable benefits of tests is that they give you confidence that your code works as
you expect it to work. Tests give you the confidence to do long-term development because with tests
in place, you know that your foundation code is dependable. Tests give you the confidence to
refactor your code to make it cleaner and more efficient.

Tests also save you time because tests help prevent regressions from being introduced and released.
Once a bug is found, you can write a test for it, you can fix the bug, and the bug can never make it
to production again because the tests will catch it in the future.

Another advantage is that tests provide excellent implicit documentation because they show exactly
how the code is designed to be used.

---

# Writing tests

> Let’s take a look at how tests are best structured. All tests should follow the same basic structure.

--

## 1. Set up environment for testing

Typically, methods perform some sort of operation upon data. So in order to test your methods,
you’ll need to set up the data required by the method. This might be as simple as declaring a few
variables, or as complex as creating a number of records in database.

Your tests should always create their own test data to execute against. That way, you can be
confident that your tests aren’t dependent upon the state of a particular environment and will be
repeatable even if they are executed in a different environment from which they were written.

If you find that many of your tests require very similar setup code, be sure to properly decompose
the setup code so that you don’t repeat yourself.

--

## 2. Call the method being tested

Once you have set up the appropriate input data, you still need to execute your code. If you are
testing a method, then you will call the method directly.

--

## 3. Verify that the results are correct

Verifying that your code works as you expect it to work is the most important part of testing. Tests
that do not verify the results of the code aren’t true tests. They are commonly referred to as smoke
tests, which aren’t nearly as effective or informative as true tests.

--

## 4. Clean up environment

Environment always should be cleaned after a test running. That way, you can be confident that your
next tests are not dependent upon the state of previous tests executing.

---

# TDD

> `Test Driven Development` (TDD) is not about writing tests. TDD is more than that, it’s a
methodology. The main idea of TDD is to write tests before code.

--

# "Red" – write failing test

This means that you have to have a failing test first. You can’t write any production code before
`red`. Why? Because you have to know this test could fail in some circumstances and you have to know
which change makes it pass.

--

# "Green" – make the test pass

Write code that is only needed to make the test pass. Now, try to run the test again. WOW, passed!
Do you think this is a bad solution? Doesn’t work fine? Sure it works fine, because the test passed.
There is `YAGNI` principal (`YAGNI stands for You Ain’t Gonna Need It`) which says `don’t write more
than you need at this moment`. If you are sure you need more, write test for it and then implement
this functionality.

--

# "Refactor" – clean up your code

Look at your code. Do you like it? Do you want to eat it? Do you want to f... it? If your answer to
any of these questions was `no`, you should do something about that. Refactoring is changing code
without changing its functionality.

--

# The colorful iteration

Whole `red, green, refactor` thing is about iteration, little programming cycles and fast feedback.
When we write failing test we say `hey, my app should do that!` Then we make it come true as fast as
we can. It’s like in this game where you have to pass the ball to the next player before it `burns`
you. When you make a test pass, then you can relax and do refactoring. Change implementation,
introduce design pattern and extract class or whatever you want. You have confidence that your code
works all the time and that you didn’t break anything. This is the smallest programing cycle; this
is exactly what TDD is about.

---

# Installation

--

## Setup envirepment

Install ruby

```bash
$ rvm install ruby-2.4.2
```

Create isolated gemset

```bash
$ rvm use 2.4.2@hello-rspec --create
ruby-2.4.2 - #gemset created /Users/ty/.rvm/gems/ruby-2.4.2@hello-rspec
ruby-2.4.2 - #generating hello-rspec wrappers - please wait
Using /Users/ty/.rvm/gems/ruby-2.4.2 with gemset hello-rspec
```

Prepare project directory

```bash
$ mkdir -p hello-rspec/lib && cd hello-rspec
```

Install bundler

```bash
$ gem install bundler
```

--

Initialize Gemfile with rspec

```bash
$ bundle init
Writing new Gemfile to /home/User/ty/hello-rspec/Gemfile

$ bundle inject rspec 3.8
Fetching gem metadata from https://rubygems.org/..........
Resolving dependencies...
Added to Gemfile:
gem 'rspec', '~> 3.8.0'
```

Run bundle Install

```bash
$ bundle install
```

Generate conventional files for a RSpec project

```bash
$ rspec --init
create   .rspec
create   spec/spec_helper.rb
```

---

### Let's write first test

lib/library.rb <!-- .element class="filename" -->

```ruby
class Library
  attr_reader :books

  def initialize(books = [])
    @books = books
  end
end

```

spec/library_spec.rb <!-- .element class="filename" -->

```ruby
require 'library'

RSpec.describe Library do
  describe '.new' do
    it 'initializes empty Library' do
      library = Library.new
      expect(library.books.size).to eq 0
    end
  end
end

```

--

# Describe

We use the `describe()` method to define an example group.

```ruby
describe 'A Library' do
end
# => A Library

describe Library do
end
# => Library

describe Library, 'with good books' do
end
# => Library with good books
```

The `describe()` method takes an arbitrary number of arguments and an optional block, and returns a
subclass of `RSpec::Core::ExampleGroup`.

--

# Nested groups

```ruby
RSpec.describe Library do
  describe '.new' do
    it 'initializes empty Library' do
    end
  end
end

# Library
#   .new
#     initializes empty Library
```

---

# What’s `it()` All About?

The `it()` method takes a single String, an optional Hash and an optional block.
String with `'it'` represents the detail that will be expressed in code within the block.

--

## Specify

Alias for `it`. Can be used when decsription can be leaved

```ruby
specify { expect(Library.new.books).to be_a Array }
```

---

# Running specs and formating output

--

# Running

All specs

```bash
$ rspec
```

Specs in specific folder

```bash
$ rspec spec/
```

Specific spec

```bash
$ rspec spec/library_spec.rb
```

Specific line in spec

```bash
$ rspec spec/library_spec.rb:4
```

--

# Formating

Colorization

```bash
$ rspec spec/library_spec.rb --color
```

Progress format (default)

```bash
$ rspec spec/library_spec.rb
```

or

```bash
$ rspec spec/library_spec.rb  --format progress

..
```

--

# Documentation format

```bash
$ rspec spec/library_spec.rb --format documentation

Library
  .create
    sets library name
    should be a kind of Library

Finished in 0.00142 seconds (files took 0.0783 seconds to load)
2 examples, 0 failures
```

--

# Additional tools for formatting

```bash
$ gem install fuubar
```

```bash
$ rspec spec/library_spec.rb  --format Fuubar
```

Output to file
```bash
$ rspec spec --format documentation --out rspec.txt
```

---

# How Expectations work

--

```ruby
expect(obj).to(matcher = nil)
expect(obj).not_to(matcher = nil)
```

Both methods take an optional Expression Matcher.

<br>

When `to` receives an Expression Matcher, it calls `matches?(self)`. If it returns true, the spec passes and execution
continues. If it returns false, then the spec fails with the message returned by matcher.failure_message.

<br>

Similarly, when `not_to` receives a matcher, it calls `matches?(self)`. If it returns false, the spec passes and
execution continues. If it returns true, then the spec fails with the message returned by
matcher.negative_failure_message.

--

### Eq matcher

```ruby
expect(obj).to eq(expected)
expect(obj).not_to eq(expected)
```

Passes if given and expected are of equal value, but not necessarily the same object.
```ruby
RSpec.describe 'a string' do
  context '#eq' do
    it 'is equal to another string of the same value' do
      expect('this string').to eq('this string')
    end
  end
end
```

--

### Equal matcher

```ruby
expect(obj).to equal(expected)
expect(obj).not_to equal(expected)
```

Passes if given and expected are the same object (object identity).
```ruby
RSpec.describe 'a string' do
  context '#equal' do
    it 'is equal to itself' do
      string = 'this string'
      expect(string).to equal(string)
    end
  end
end
```

---

### Let's try TDD in action.
Assume Library class functionality should be extended with:
- Add a single book to library
- Show list of books, columns `id, name` (id is a book index in array)
- Remove book by id

--

### What exactly should be tested?

To answer this question, we must get acquainted with [Use case](https://en.wikipedia.org/wiki/Use_case) definition.
Shortly, `Use case` describes how a user uses a system to accomplish a particular goal. Each use case may have positive and negative tests cases.

---

### Use case: Add a single book to library

### What to check?
1. Check if books count was changed by 1.
2. Check if added book has similar name.
3. Check if name of book is not empty.

--

### Add tests for use cases

```ruby
require 'library'

RSpec.describe Library do
  describe '.new' do
    it 'initializes empty Library' do
      library = Library.new
      expect(library.books.size).to eq 0
    end

    specify { expect(Library.new.books).to be_a Array }
  end

  describe '#add_book' do
    it 'adds book with name to library' do
      library = Library.new
      book_name = 'First book'
      library.add_book(name: book_name)
      expect(library.books.first[:name]).to eq book_name
    end

    it 'increases books count by 1' do
      library = Library.new
      book_name = 'First book'
      expect(library.books.size).to eq 0
      library.add_book(name: book_name)
      expect(library.books.size).to eq 1
    end
  end
end

```

--

### Tests are red

```bash
Library
  .new
    initializes empty Library
    should be a kind of Array
  #add_book
    adds book with name to library (FAILED - 1)
    increases books count by 1 (FAILED - 2)

Failures:

  1) Library#add_book adds book with name to library
     Failure/Error: library.add_book(name: book_name)

     NoMethodError:
       undefined method `add_book' for #<Library:0x000056158d355a18 @books=[]>
     # ./spec/library_spec.rb:17:in `block (3 levels) in <top (required)>'

  2) Library#add_book increases books count by 1
     Failure/Error: expect { library.add_book(name: book_name) }.to change(library.books, :size).from(0).to(1)

     NoMethodError:
       undefined method `add_book' for #<Library:0x000056158d354848 @books=[]>
     # ./spec/library_spec.rb:24:in `block (4 levels) in <top (required)>'
     # ./spec/library_spec.rb:24:in `block (3 levels) in <top (required)>'

Finished in 0.00337 seconds (files took 0.08869 seconds to load)
4 examples, 2 failures

Failed examples:

rspec ./spec/library_spec.rb:14 # Library#add_book adds book with name to library
rspec ./spec/library_spec.rb:21 # Library#add_book increases books count by 1
```

--

### Implementation

```ruby
class Library
  attr_reader :books

  def initialize
    @books = []
  end

  def add_book(name:)
    books << { name: name }
  end
end
```

### Tests are green

```bash
Library
  .new
    initializes empty Library
    should be a kind of Array
  #add_book
    adds book with name to library
    increases books count by 1

Finished in 0.00232 seconds (files took 0.06807 seconds to load)
4 examples, 0 failures
```

--

### Include

Passes if given includes expected. This works for collections and Strings. You can also pass in multiple args and it
will only pass if all args are found in collection.

```ruby
expect([1,2,3]).to include(3)
expect([1,2,3]).to include(2,3)
expect('spread').to include('read')
expect('spread').to_not include('red')
```

--

## Membership

```ruby
expect(obj).to include(expected)
expect(obj).to match_array(expected_array)
expect(obj).to contain_exactly(one_element, another_element)
```

### Examples

```ruby
expect([1, 3, 5]).to contain_exactly(3, 1, 5)
expect([1, 3, 5]).to match_array([5, 3, 1])
```
--
### Changes

Sometimens you expect some code (wrapped in a proc) to change the state of some object. There is a convenient way to
check it with rspec:

```ruby
it 'should remove the last element' do
  expect { @array.pop }.to change{ @array.size }
end
```

`by()`, `to()`, `from()`, `by_at_least()`, `by_at_most()`

```ruby
it 'removes the last element' do
  expect { @array.pop }.to change{ @array.size }.by(1)
end

it 'removes the last element' do
  expect { @array.pop }.to change{ @array.size }.to(2)
end

it 'removes the last element' do
  expect { @array.pop }.to change{ @array.size }.from(3).to(2)
end

it 'changes size by at least 1' do
  expect { 2.times { @array.pop } }.to change{ @array.size }.by_at_least(1)
end

it 'changes size by at most 2' do
  expect { 2.times { @array.pop } }.to change{ @array.size }.by_at_most(2)
end
```

--

```ruby
require 'library'

RSpec.describe Library do
  # ...

  describe '#add_book' do
    it 'adds book with name to library' do
      library = Library.new
      book_name = 'First book'
      library.add_book(name: book_name)
      expect(library.books).to match([{name: book_name}])
    end

    it 'increases books count by 1' do
      library = Library.new
      book_name = 'First book'
      expect { library.add_book(name: book_name) }.to(
        change{ library.books.size }.from(0).to(1)
      )
    end
  end
end
```

---

# Hooks

`before` / `after` / `around`

> Use before, after, around hooks to execute arbitrary code before and/or after the body of an
example is run

- `:each` / `:example` - runs before/after/around each example
- `:all` / `:context` - runs before/after/around top level group
- `:suite` - run once before the first example or/and after the last example

--

# Using

```ruby
# Inside spec
describe MyClass do
  before {}
  before(:each) {}
  before(:all) {}

  after {}
  after(:each) {}
  after(:all) {}

  around {}
  around(:each) {}
end

```

--

## before(:all)

spec/array_spec.rb <!-- .element class="filename" -->

```ruby
require 'library'

RSpec.describe Library do
  describe '.new' do
    it 'initializes empty Library' do
      library = Library.new
      expect(library.books.size).to eq 0
    end

    specify { expect(Library.new.books).to be_a Array }
  end

  describe '#add_book' do
    before(:all) do
      @book_name = 'First book'
    end

    it 'adds book with name to library' do
      library = Library.new
      library.add_book(name: @book_name)
      expect(library.books).to match([{name: @book_name}])
    end

    it 'increases books count by 1' do
      library = Library.new
      expect { library.add_book(name: @book_name) }.to(
        change{ library.books.size }.from(0).to(1)
      )
    end
  end
end
```
--

## before(:each)

spec/array_spec.rb <!-- .element class="filename" -->

```ruby
require 'library'

RSpec.describe Library do
  before(:each) do
    @library = Library.new
  end

  describe '.new' do
    it 'initializes empty Library' do
      expect(@library.books.size).to eq 0
    end

    specify { expect(@library.books).to be_a Array }
  end

  describe '#add_book' do
    before(:all) do
      @book_name = 'First book'
    end

    it 'adds book with name to library' do
      @library.add_book(name: @book_name)
      expect(@library.books).to match([{name: @book_name}])
    end

    it 'increases books count by 1' do
      expect { @library.add_book(name: @book_name) }.to(
        change{ @library.books.size }.from(0).to(1)
      )
    end
  end
end
```

--

## Hooks run in order

spec/callbacks_spec.rb <!-- .element class="filename" -->

```ruby
RSpec.describe 'before and after callbacks' do
  before(:all) do
    puts 'global before all'
  end

  before(:each) do
    puts 'global before each'
  end

  after(:each) do
    puts 'global after each'
  end

  after(:all) do
    puts 'global after all'
  end

  it 'gets run in order' do
    puts 'global test 1'
  end

  it 'gets run in order' do
    puts 'global test 2'
  end

  describe 'in group' do
    before(:all) do
      puts 'group before all'
    end

    before(:each) do
      puts 'group before each'
    end

    after(:each) do
      puts 'group after each'
    end

    after(:all) do
      puts 'group after all'
    end

    it 'gets run in order' do
      puts 'group test 1'
    end

    it 'gets run in order' do
      puts 'group test 2'
    end
  end
end
```

--

```bash
$ rspec spec/callbacks_spec.rb

global before all
global before each
global test 1
global after each
global before each
global test 2
global after each
group before all
global before each
group before each
group test 1
group after each
global after each
global before each
group before each
group test 2
group after each
global after each
group after all
global after all
```

---

## Moreover, tests can be refactored even better with
# Let

--

Use `let` to define a memoized helper method. The value will be cached across multiple calls in the same example but
not across examples.

--

## Use before

```ruby
  before(:each) do
    @library = Library.new
  end

  describe '.new' do
    it 'initializes empty Library' do
      expect(@library.books.size).to eq 0
    end

    specify { expect(@library.books).to be_a Array }
  end
```

--

## Use let

```ruby
require 'library'

RSpec.describe Library do
  let(:library) { Library.new }

  describe '.new' do
    it 'initializes empty Library' do
      expect(library.books.size).to eq 0
    end

    specify { expect(library.books).to be_a Array }
  end

  describe '#add_book' do
    let(:book_name) { 'First book' }

    it 'adds book with name to library' do
      library.add_book(name: book_name)
      expect(library.books).to match([{name: book_name}])
    end

    it 'increases books count by 1' do
      expect { library.add_book(name: book_name) }.to(
        change{ library.books.size }.from(0).to(1)
      )
    end
  end
end
```

Note that `let` is lazy-evaluated: it is not evaluated until the first time the method it defines is invoked.
You can use `let!` to force the method's invocation before each example(note, that it's a bad practice accordingly to [rubocop-rspec](https://www.rubydoc.info/gems/rubocop-rspec/1.7.0/RuboCop/Cop/RSpec/LetSetup))

---

# Subject

--

Use `subject` in the group scope to explicitly define the value that is returned by the subject method in the example
scope.

<br>

If you don't define `subject` it is set as an object of described class (for example Array.new)

<br>

Use `subject!` can be used for calling method before each example

--

spec/array_spec.rb <!-- .element class="filename" -->

```ruby
RSpec.describe Array, 'with some elements' do
  subject { [1,2,3] }

  it { expect(subject).not_to be_empty }
  it { is_expected.not_to be_empty }

  it 'has the prescribed elements' do
    expect(subject).to eq([1,2,3])
  end
end
```

```bash
$ rspec spec/array_spec.rb --format documentation

Array with some elements
  should not be empty
  should not be empty
  should have the prescribed elements

Finished in 0.00495 seconds
3 examples, 0 failures
```

--

```ruby
RSpec.describe Array, 'with some elements' do
  subject(:array) { [1,2,3] }

  it { expect(array).not_to be_empty }
  it { is_expected.not_to be_empty }

  it 'has the prescribed elements' do
    expect(array).to eq([1,2,3])
  end
end
```

--

```ruby
require 'library'

RSpec.describe Library do
  subject(:library) { Library.new }

  describe '.new' do
    it 'initializes empty Library' do
      expect(library.books.size).to eq 0
    end

    specify { expect(library.books).to be_a Array }
  end

  describe '#add_book' do
    let(:book_name) { 'First book' }

    it 'adds book with name to library' do
      library.add_book(name: book_name)
      expect(library.books).to match([{name: book_name}])
    end

    it 'increases books count by 1' do
      expect { library.add_book(name: book_name) }.to(
        change{ library.books.size }.from(0).to(1)
      )
    end
  end
end
```
---

# Described class

--

If the first argument to the outermost example group is a class, the class is exposed to each example via the
`described_class()` method.

```ruby
require 'library'

RSpec.describe Library do
  subject(:library) { described_class.new }

  describe '.new' do
    it 'initializes empty Library' do
      expect(library.books.size).to eq 0
    end

    specify { expect(library.books).to be_a Array }
  end

  describe '#add_book' do
    let(:book_name) { 'First book' }

    it 'adds book with name to library' do
      library.add_book(name: book_name)
      expect(library.books).to match([{name: book_name}])
    end

    it 'increases books count by 1' do
      expect { library.add_book(name: book_name) }.to(
        change{ library.books.size }.from(0).to(1)
      )
    end
  end
end
```

---

### True/False Matchers

```ruby
expect(obj).to be_truthy    # passes if obj is truthy (not nil or false)
expect(obj).to be true      # passes if obj == true
expect(obj).to be_falsey    # passes if obj is falsy (nil or false)
expect(obj).to be false     # passes if obj == false
```


```ruby
require 'library'

RSpec.describe Library do
  subject(:library) { described_class.new }

  describe '.new' do
    it 'initializes empty Library' do
      expect(library.books.empty?).to be true
    end

    specify { expect(library.books).to be_a Array }
  end

  # ...
end
```
--

### Predicate Matchers

A Ruby predicate method is a method that ends with a `?` and returns a boolean value, like `string.empty?` or
`regexp.match?` methods. For these cases Rspec allows us to describe expectations with `be_something` matcher.
When using a `be_something` matcher, RSpec removes the `be_`, appends a `?` and calls the resulting method in the
receiver.

```ruby
# instead of writing
expect(''.empty?).to eq(true)

# RSpec allows to use predicate expectation
expect('').to be_empty
```

--

### How it works

- `be_`      -> '?'
- `be_zero`  -> 'zero?'
- `be_nil`   -> 'nil?'
- `be_empty` -> 'empty?'

<br>

Alternately, for a predicate method that begins with `has` like `Hash#has_key?`, RSpec allows you to use an alternate
form since `be_has_key` makes no sense.

<br>

- expect(hash).to have_key(:foo) -> calls hash.has_key?(:foo)
- expect(array).to_not have_odd_values -> calls array.has_odd_values?

--
<img src="https://res.cloudinary.com/dciwrzg9w/image/upload/v1573082013/sverh_rspec_tjshdd.jpg"
     alt="Markdown Monster icon"
     height="800" />

--
```ruby
require 'library'

RSpec.describe Library do
  subject(:library) { described_class.new }

  describe '.new' do
    it 'initializes empty Library' do
      expect(library.books).to be_empty
    end

    # ...
  end

  # ...
end
```
---

### Use case: Show list of books, columns `id, name` (id = index + 1 of element in array)

### What to check?
1. Check result for empty Library
2. Check result for Library with books
--
### Add tests for use cases
```ruby
RSpec.describe Library do
  subject(:library) { described_class.new(books) }
  let(:books) { [] }

  # ...

  describe '#show_books' do
    context 'empty Library' do
      let(:expected_message) { 'Library is empty' }

      it 'returns empty message' do
        expect(subject.show_books).to eq expected_message
      end
    end

    context 'Library with books' do
      let(:expected_message) do
        "1. #{book_name_1}"\
        "\n"\
        "2. #{book_name_2}"
      end
      let(:book_name_1) { 'Book 1' }
      let(:book_name_2) { 'Book 2' }
      let(:books) { [{ name: book_name_1 }, { name: book_name_2 }] }

      it 'returns a list of books' do
        expect(subject.show_books).to eq expected_message
      end
    end
  end
end
```
--
# Context

The `context()` method is an alias for `describe()`.

```ruby
RSpec.describe Library do
  subject(:library) { described_class.new(books) }
  let(:books) { [] }

  describe '#show_books' do
    context 'Library with books' do
      let(:books) { [{ name: book_name_1 }, { name: book_name_2 }] }

      it 'returns a list of books' do
      end
    end
  end
end

# Library
#   #show_books
#     Library with books
#       returns a list of books
```

--

## Tests are Red

```bash
Library
  .new
    initializes empty Library
    should be a kind of Array
  #add_book
    adds book with name to library
    increases books count by 1
  #show_books
    empty Library
      returns empty message (FAILED - 1)
    Library with books
      returns a list of books (FAILED - 2)

Failures:

  1) Library#show_books empty Library returns empty message
     Failure/Error: expect(subject.show_books).to eq expected_message

     NoMethodError:
       undefined method `show_books' for #<Library:0x000055cb3bb92380 @books=[]>
     # ./spec/library_spec.rb:36:in `block (4 levels) in <top (required)>'

  2) Library#show_books Library with books returns a list of books
     Failure/Error: expect(subject.show_books).to eq expected_message

     NoMethodError:
       undefined method `show_books' for #<Library:0x000055cb3bb908f0>
     # ./spec/library_spec.rb:51:in `block (4 levels) in <top (required)>'

Finished in 0.00505 seconds (files took 0.08538 seconds to load)
6 examples, 2 failures

```
--

### Implementation

```ruby
class Library
  EMPTY_LIBRARY_MESSAGE = 'Library is empty'.freeze

  attr_reader :books

  def initialize
    @books = []
  end

  # ...

  def show_books
    return EMPTY_LIBRARY_MESSAGE if books.empty?

    books.each_with_index.map do |book, index|
      "#{index + 1}. #{book[:name]}"
    end.join("\n")
  end
end
```
--
### Tests are green

```bash
Library
  .new
    initializes empty Library
    should be a kind of Array
  #add_book
    adds book with name to library
    increases books count by 1
  #show_books
    empty Library
      returns empty message
    Library with books
      returns a list of books

Finished in 0.00419 seconds (files took 0.0975 seconds to load)
6 examples, 0 failures

```
--
## Refactoring

```ruby
class Library
  EMPTY_LIBRARY_MESSAGE = 'Library is empty'.freeze

  attr_reader :books

  def initialize(books = [])
    @books = books
  end

 # ...

  def show_books
    return EMPTY_LIBRARY_MESSAGE if books.empty?

    compose_books_message
  end

  private

  def compose_books_message
    books.each_with_index.map do |book, index|
      "#{index + 1}. #{book[:name]}"
    end.join("\n")
  end
end
```
--
### Tests are green

```bash
Library
  .new
    initializes empty Library
    should be a kind of Array
  #add_book
    adds book with name to library
    increases books count by 1
  #show_books
    empty Library
      returns empty message
    Library with books
      returns a list of books

Finished in 0.00419 seconds (files took 0.0975 seconds to load)
6 examples, 0 failures

```

---
### Use case: Remove book by id

### What to check?
1. Check books count was reduced by 1
2. Check error was raised if book with id does not exist
3. Check error was raised if id value is nil
4. Check error was raised if id value is empty string
5. Check error was raised if id value is not a digit
6. Check error was raised if id value is zero

--


### Raise Error Matcher

```ruby
expect { raise "oops" }.to raise_error
expect { raise "oops" }.to raise_error(RuntimeError)
expect { raise "oops" }.to raise_error("oops")
expect { raise "oops" }.to raise_error(/op/)
expect { raise "oops" }.to raise_error(RuntimeError, "oops")
expect { raise "oops" }.to raise_error(RuntimeError, /op/)
expect { raise "oops" }.to raise_error(an_instance_of(RuntimeError).and having_attributes(message: "oops"))
```
--
Add tests for use cases
```ruby
RSpec.describe Library do
  subject(:library) { described_class.new(books) }
  let(:books) { [] }

  # ...

  describe '#remove_book' do
    let(:books) { [{ name: 'Book 1' }] }

    it 'removes book from library' do
      expect { subject.remove_book(1) }.to(
        change { subject.books.size }.from(1).to(0)
      )
    end

    context 'book with such id does not exist' do
      it 'raises BookNotFound error' do
        expect { subject.remove_book(999) }.to raise_error(BookNotFoundError, /with id 999 not found/)
      end
    end

    context 'id is nil' do
      it 'raises DigitValidationError' do
        expect { subject.remove_book(nil) }.to(
          raise_error(DigitValidationError)
        )
      end
    end

    context 'id is empty string' do
      it 'raises DigitValidationError' do
        expect { subject.remove_book('') }.to(
          raise_error(DigitValidationError)
        )
      end
    end

    context 'id is not ad digit' do
      it 'raises DigitValidationError' do
        expect { subject.remove_book('not_a_digit') }.to(
          raise_error(DigitValidationError)
        )
      end
    end

    context 'id is zero' do
      it 'raises DigitValidationError' do
        expect { subject.remove_book('0') }.to(
          raise_error(DigitValidationError)
        )
      end
    end
  end
end

```

--

## Tests are Red

```bash
Library
  .new
    initializes empty Library
    should be a kind of Array
  #add_book
    adds book with name to library
    increases books count by 1
  #show_books
    empty Library
      returns empty message
    Library with books
      returns a list of books
  #remove_book
    removes book from library (FAILED - 1)
    book with such id does not exist
      raises BookNotFound error (FAILED - 2)
    id is nil
      raises DigitValidationError (FAILED - 3)
    id is empty string
      raises DigitValidationError (FAILED - 4)
    id is not ad digit
      raises DigitValidationError (FAILED - 5)
    id is zero
      raises DigitValidationError (FAILED - 6)

Failures:

  1) Library#remove_book removes book from library
     Failure/Error:
       expect { subject.remove_book(1) }.to(
         change { subject.books.size }.from(1).to(0)
       )

     NoMethodError:
       undefined method `remove_book' for #<Library:0x000055a2a7ca42d0 @books=[{:name=>"Book 1"}]>
     # ./spec/library_spec.rb:79:in `block (4 levels) in <top (required)>'
     # ./spec/library_spec.rb:79:in `block (3 levels) in <top (required)>'

  2) Library#remove_book book with such id does not exist raises BookNotFound error
     Failure/Error: expect { subject.remove_book(999) }.to raise_error(BookNotFoundError, /with id 999 not found/)

       expected BookNotFoundError with message matching /with id 999 not found/, got #<NoMethodError: undefined method `remove_book' for #<Library:0x000055a2a7cc87e8 @books=[{:name=>"Book 1"}]>> with backtrace:
         # ./spec/library_spec.rb:86:in `block (5 levels) in <top (required)>'
         # ./spec/library_spec.rb:86:in `block (4 levels) in <top (required)>'
     # ./spec/library_spec.rb:86:in `block (4 levels) in <top (required)>'

  3) Library#remove_book id is nil raises DigitValidationError
     Failure/Error:
       expect { subject.remove_book(nil) }.to(
         raise_error(DigitValidationError)
       )

       expected DigitValidationError, got #<NoMethodError: undefined method `remove_book' for #<Library:0x000055a2a7796b58 @books=[{:name=>"Book 1"}]>> with backtrace:
         # ./spec/library_spec.rb:92:in `block (5 levels) in <top (required)>'
         # ./spec/library_spec.rb:92:in `block (4 levels) in <top (required)>'
     # ./spec/library_spec.rb:92:in `block (4 levels) in <top (required)>'

  4) Library#remove_book id is empty string raises DigitValidationError
     Failure/Error:
       expect { subject.remove_book('') }.to(
         raise_error(DigitValidationError)
       )

       expected DigitValidationError, got #<NoMethodError: undefined method `remove_book' for #<Library:0x000055a2a77d45c0 @books=[{:name=>"Book 1"}]>> with backtrace:
         # ./spec/library_spec.rb:100:in `block (5 levels) in <top (required)>'
         # ./spec/library_spec.rb:100:in `block (4 levels) in <top (required)>'
     # ./spec/library_spec.rb:100:in `block (4 levels) in <top (required)>'

  5) Library#remove_book id is not ad digit raises DigitValidationError
     Failure/Error:
       expect { subject.remove_book('not_a_digit') }.to(
         raise_error(DigitValidationError)
       )

       expected DigitValidationError, got #<NoMethodError: undefined method `remove_book' for #<Library:0x000055a2a781adb8 @books=[{:name=>"Book 1"}]>> with backtrace:
         # ./spec/library_spec.rb:108:in `block (5 levels) in <top (required)>'
         # ./spec/library_spec.rb:108:in `block (4 levels) in <top (required)>'
     # ./spec/library_spec.rb:108:in `block (4 levels) in <top (required)>'

  6) Library#remove_book id is zero raises DigitValidationError
     Failure/Error:
       expect { subject.remove_book('0') }.to(
         raise_error(DigitValidationError)
       )

       expected DigitValidationError, got #<NoMethodError: undefined method `remove_book' for #<Library:0x000055a2a783cda0 @books=[{:name=>"Book 1"}]>> with backtrace:
         # ./spec/library_spec.rb:116:in `block (5 levels) in <top (required)>'
         # ./spec/library_spec.rb:116:in `block (4 levels) in <top (required)>'
     # ./spec/library_spec.rb:116:in `block (4 levels) in <top (required)>'

Finished in 0.02378 seconds (files took 0.09701 seconds to load)
12 examples, 6 failures


```
--

### Implementation

```ruby
class Library
  EMPTY_LIBRARY_MESSAGE = 'Library is empty'.freeze

  attr_reader :books

  def initialize(books = [])
    @books = books
  end

  # ...

  def remove_book(id)
    raise DigitValidationError unless is_digit?(id)
    book_index = id.to_i - 1
    raise BookNotFoundError, "Book with id #{id} not found" if books[book_index].nil?
    books.delete_at(book_index)
  end

  private

  # ...

  def book_exists?(index)
    !books[index].nil?
  end

  def is_digit?(id)
    id.to_s.match(/^[1-9]\d*$/)
  end
end

class BookNotFoundError < StandardError; end
class DigitValidationError < StandardError; end
```
--
### Tests are green
```bash
Library
  .new
    initializes empty Library
    should be a kind of Array
  #add_book
    adds book with name to library
    increases books count by 1
  #show_books
    empty Library
      returns empty message
    Library with books
      returns a list of books
  #remove_book
    removes book from library
    book with such id does not exist
      raises BookNotFound error
    id is nil
      raises DigitValidationError
    id is empty string
      raises DigitValidationError
    id is not ad digit
      raises DigitValidationError
    id is zero
      raises DigitValidationError

Finished in 0.01005 seconds (files took 0.11026 seconds to load)
12 examples, 0 failures

```

--
## Refactoring

```ruby
class Library
  EMPTY_LIBRARY_MESSAGE = 'Library is empty'.freeze

  attr_reader :books

  def initialize(books = [])
    @books = books
  end

  # ...

  def remove_book(id)
    raise_digit_validation_error(id) unless is_digit?(id)
    book_index = id.to_i - 1
    raise_not_found_error(id) unless book_exists?(book_index)
    books.delete_at(book_index)
  end

  private

  # ...

  def raise_not_found_error(id)
    raise BookNotFoundError, "Book with id #{id} not found"
  end

  def raise_digit_validation_error(id)
    raise DigitValidationError, 'Please provide a correct digit value'
  end

  def book_exists?(index)
    !books[index].nil?
  end

    def is_digit?(id)
    id.to_s.match(/^[1-9]\d*$/)
  end
end

class BookNotFoundError < StandardError; end
class DigitValidationError < StandardError; end

```

---
### Add book name parence validation

```ruby
require 'library'

RSpec.describe Library do
  subject(:library) { described_class.new(books) }
  let(:books) { [] }

  # ...

  describe '#add_book' do
    let(:book_name) { 'First book' }

    # ...

    context 'name is nil' do
      let(:book_name) { nil }

      it 'raises PresenceValidationError' do
        expect { library.add_book(name: book_name) }.to(
          raise_error(PresenceValidationError)
        )
      end
    end

    context 'name is empty' do
      let(:book_name) { '' }

      it 'raises PresenceValidationError' do
        expect { library.add_book(name: book_name) }.to(
          raise_error(PresenceValidationError)
        )
      end
    end
  end

  # ...
end

```

--

### Implementation

```ruby
class Library
  EMPTY_LIBRARY_MESSAGE = 'Library is empty'.freeze

  attr_reader :books

  def initialize(books = [])
    @books = books
  end

  def add_book(name:)
    raise PresenceValidationError if name.nil? || name.empty?
    books << { name: name }
  end

  # ...

end

class BookNotFoundError < StandardError; end
class DigitValidationError < StandardError; end
class PresenceValidationError < StandardError; end

```

---
### Few advices:
1. Remember about encapsulation. Do not test private methods. Only public methods should be tested.

```ruby
class SomeService
  def initialize(text)
    @text = text
  end

  def call
    print_text
  end

  private

  def print_text
    puts 'Hello'
    puts @text
    puts 'Goodbye'
  end
end

# E.g. if we have test for print_text method, then next refactoring will break the tests

class SomeService
  def initialize(text)
    @text = text
  end

  def call
    print_hello
    print_text
    print_goodbye
  end

  private

  def print_hello
    puts 'Hello'
  end

  def print_text
    puts @text
  end

  def print_goodbye
    puts 'Goodbye'
  end
end
```
--
2.Do not put business logic to initializer. It will be harder to test such class.
### Bad
```ruby
class Example
  def initialize(params)
    @first = params[:first]
    @second = params[:second]
    # Bad
    validate_first_param
    validate_second_param
    validate_whatever
  end

  def process
    @first + @second
  end

  private

  def validate_first_param
    raise StandardError if @first.nil?
  end

  def validate_second_param
    raise StandardError if @second.nil?
  end

  def validate_whatever
    raise StandardError if @first.include?('first')
    raise StandardError if @second.include?('third')
  end
end
```
--
## Good

```ruby
class Example
  def initialize(params)
    @first = params[:first]
    @second = params[:second]
  end

  def process
    # Good
    validate_first_param
    validate_second_param
    validate_whatever
    @first + @second
  end

  private

  def validate_first_param
    raise StandardError if @first.nil?
  end

  def validate_second_param
    raise StandardError if @second.nil?
  end

  def validate_whatever
    raise StandardError if @first.include?('first')
    raise StandardError if @second.include?('third')
  end
end
```
---

# Other Spec::Matchers

--


## Comparisons

```ruby
expect(obj).to be >  expected
expect(obj).to be >= expected
expect(obj).to be
```

### Between

```ruby
expect(obj).to be_between(minimum, maximum).inclusive
expect(obj).to be_between(minimum, maximum).exclusive
```

```ruby
expect(10).to be_between(1, 10).inclusive
expect(10).to be_between(1, 11).exclusive
```

### Start/End

```ruby
expect(obj).to start_with expected
expect(obj).to end_with expected
```

```ruby
eexpect('first string').to start_with('first')
expect('first string').not_to start_with('second')
expect([1,3,5]).to start_with(1,3)
```

--

### Floating point numbers

Passes if given `==` expected `+/-` delta

```ruby
expect(obj).to be_within(delta).of(expected)
expect(obj).not_to be_within(delta).of(expected)
```

```ruby
expect(result).to be_within(0.01).of(expected)
```

Note that the difference between the actual and expected values must be smaller than your delta; if it is equal, the
matcher will fail.

--

### Regular Expressions

For checking strings to match regular expressions, the `match` is used. This can be very useful when dealing with
multiple-line expectations.

```ruby
expect(result).to match(/this regexp/)
```

--

### Types and responses

```ruby
expect(obj).to respond_to(expected)
expect(obj).to be_instance_of(expected)
expect(obj).to be_kind_of(expected)
```
---

End of first lection

---

## Lets create console interface to use Library

--

### Requirements
1. Show greeting message
2. Show available action
  - Show books
  - Add book
  - Remove book
3. Shut down when user typed `exit`
---
## around(:each)

Around hooks receive the example as a block argument, extended to behave as a proc. This lets you define code that should be executed before and after the example.

```ruby
class User
  def self.communication
    puts 'Hello!'
    yield
    puts 'Bye!'
  end
end

RSpec.describe 'Around filter' do
  around(:each) do |example|
    User.communication(&example)
  end

  it 'first test' do
    puts 'run the example'
  end
end
```

```bash
$ rspec spec

Hello!
run the example
Bye!
```

--

```ruby
RSpec.describe 'Test around hook' do
  around(:each) do |example|
    puts 'around each before'
    example.run
    puts 'around each after'
  end

  it 'runs' do
    puts "inside the example"
  end
end
```

```bash
around each before
inside the example
around each after
```

---
# Pending

```ruby
RSpec.describe Array do
  skip 'not implemented yet' do
  end

  context '#last' do
    it 'returns the last element', skip: true do
      array = [:first, :second, :third]
      expect(array.last).to eq(:third)
    end

    it 'does not remove the last element', skip: 'reason explanation' do
      array = [:first, :second, :third]
      array.last
      expect(array.size).to eq(3)
    end
  end

  it 'does something else' do
    skip
  end

  it 'does something else' do
    skip 'reason explanation'
  end

  context '#first' do
    it 'returns the first element'
  end
end
```

--

```bash
$ rspec spec/array_spec.rb --format documentation
Array
  not implemented yet (PENDING: No reason given)
  does something else (PENDING: No reason given)
  does something else (PENDING: reason explanation)
  #last
    returns the last element (PENDING: No reason given)
    does not remove the last element (PENDING: reason explanation)
  #first
    returns the first element (PENDING: Not yet implemented)

Pending:
  Array not implemented yet
    # No reason given
    # ./spec/models/test_spec.rb:2
  Array does something else
    # No reason given
    # ./spec/models/test_spec.rb:18
  Array does something else
    # reason explanation
    # ./spec/models/test_spec.rb:22
  Array#last should return the last element
    # No reason given
    # ./spec/models/test_spec.rb:6
  Array#last should not remove the last element
    # reason explanation
    # ./spec/models/test_spec.rb:11
  Array#first return the first element
    # Not yet implemented
    # ./spec/models/test_spec.rb:27

Finished in 0.00138 seconds
6 examples, 0 failures, 6 pending
```

New example group aliases: `xdescribe`/`xcontext`, like xit for examples, can be used to temporarily
skip an example group.

---

## Define hooks in configuration

spec/callbacks_spec.rb <!-- .element class="filename" -->

```ruby
RSpec.configure do |config|
  config.before(:suite) do
    puts 'before suite'
  end

  config.before(:all) do
    puts 'before all'
  end

  config.before(:each) do
    puts 'before each'
  end

  config.after(:each) do
    puts 'after each'
  end

  config.after(:all) do
    puts 'after all'
  end

  config.after(:suite) do
    puts 'after suite'
  end
end

RSpec.describe 'before and after callbacks in config' do
  it 'runs' do
    puts 'test 1'
  end

  it 'runs' do
    puts 'test 2'
  end
end
```

--

```bash
$ rspec spec/callbacks_spec.rb

before suite
before all
before each
test 1
after each
before each
test 2
after each
after all
after suite
```

---

# Sharing helper methods

--

```ruby
module UserHelpers
  def valid_user
    User.new(email: 'email@example.com', password: 'shhhhh')
  end

  def invalid_user
    User.new(password: 'shhhhh')
  end
end

RSpec.describe User do
  include UserHelpers

  it 'does something when it is valid' do
    user = valid_user
    # do stuff
  end

  it 'does something when it is not valid' do
    user = invalid_user
    # do stuff
  end
end
```

--

### Including helper to each test

```ruby
RSpec.configure do |config|
  config.include(UserHelpers)
end
```

```ruby
RSpec.configure do |config|
  config.include(UserHelpers), foo: :bar
  config.include Helpers, :include_helpers
  config.extend  Helpers, :extend_helpers
end
```

```ruby
it 'first test', foo: :bar do
end

it 'second test', :include_helpers do
end

it 'third test', :extend_helpers do
end
```

---

# Filters

--

spec/subject_spec.rb <!-- .element class="filename" -->

```ruby
describe Actor do
  let(:name) { 'Ivan' }

  context 'with subject redefinition', :focus do # or focus: true
    let(:actor) {  Actor.new(name) }
    subject { actor }

    it 'has name', :slow do # or slow: true
      expect(subject.name).to eq(name)
    end
  end
end
```

```bash
$ rspec spec/subject_spec.rb --tag focus --format documentation

Actor
  with subject redefinition
    has name

Finished in 1.22 seconds
1 example, 0 failures
```

--

spec/spec_helper.rb <!-- .element class="filename" -->

```ruby
Rspec.configure do |config|
  config.filter_run focus: true
  config.run_all_with_everything_filtered = true
end
```

<br>

You can also use fit/fdescription/fcontext methods instead of using focus: true
```bash
$ rspec spec/subject_spec.rb --tag ~slow --format documentation

Finished in 1.39 seconds
0 example, 0 failures
```

spec/spec_helper.rb <!-- .element class="filename" -->

```ruby
Rspec.configure do |config|
  config.filter_run_excluding slow: true
  config.run_all_with_everything_filtered = true
end
```

---

# Shared Examples

--

Shared examples let you describe behaviour of types or modules. When declared, a shared group's content is stored. It
is only realized in the context of another example group, which provides any context the shared group needs to run.

<br>

- `include_examples 'name'` # include the examples in the current context
- `it_behaves_like 'name'` # include the examples in a nested context
- `it_should_behave_like 'name'` # include the examples in a nested context
- `matching metadata` # include the examples in the current context

--

You can use any of these methods to use shared examples. Filewith share examples should be loaded before the files that
use them

```ruby
require 'set'

RSpec.shared_examples 'a collection object' do
  describe '<<' do
    it 'adds objects to the end of the collection' do
      collection << 1
      collection << 2
      expect(collection.to_a).to eq([1,2])
    end
  end
end

RSpec.describe Array do
  it_behaves_like 'a collection object' do
    let(:collection) { Array.new }
  end
end

RSpec.describe Set do
  it_behaves_like 'a collection object' do
    let(:collection) { Set.new }
  end
end
```

--

### Including helper to each test

```bash
$ rspec spec/collection_spec.rb --format documentation

Array
  behaves like a collection object
    <<
      adds objects to the end of the collection

Set
  behaves like a collection object
    <<
      adds objects to the end of the collection

Finished in 0.00443 seconds
2 examples, 0 failures
```

---

# Shared context

--

Use `shared_context` to define a block that will be evaluated in the context of example groups either explicitly, using
`include_context`, or implicitly by matching `metadata`.

```ruby
RSpec.shared_context 'shared stuff', a: :b do
  before { @some_var = :some_value }

  def shared_method
    'it works'
  end

  let(:shared_let) { {'arbitrary' => 'object'} }

  subject do
    'this is the subject'
  end
end
```

--

## include_context

```ruby
RSpec.describe "group that includes a shared context using 'include_context'" do
  include_context 'shared stuff'

  it 'has access to methods defined in shared context' do
    expect(shared_method).to eq('it works')
  end

  it 'has access to methods defined with let in shared context' do
    expect(shared_let['arbitrary']).to eq('object')
  end

  it 'runs the before hooks defined in the shared context' do
    expect(@some_var).to eq(:some_value)
  end

  it 'accesses the subject defined in the shared context' do
    expect(subject).to eq('this is the subject')
  end
end
```
--

## metadata

```ruby
RSpec.describe 'group that includes a shared context using metadata', a: :b do
  it 'has access to methods defined in shared context' do
    expect(shared_method).to eq('it works')
  end

  it 'has access to methods defined with let in shared context' do
    expect(shared_let['arbitrary']).to eq('object')
  end

  it 'runs the before hooks defined in the shared context' do
    expect(@some_var).to eq(:some_value)
  end

  it 'accesses the subject defined in the shared context' do
    expect(subject).to eq('this is the subject')
  end
end
```

```bash
$ rspec spec/shared_stuff_spec.rb

........
Finished in 0.00758 seconds
8 examples, 0 failures
```
--

## Output

```ruby
expect { obj }.to output('some output').to_stdout
expect { actual }.to output('some error').to_stderr
```

```ruby
expect { puts('output') }.to output('output').to_stdout
expect { warn('error') }.to output('error').to_stderr
```

---



### Custom matchers

When you find that none of the stock Expectation Matchers provide a natural feeling expectation, you can very easily
write your own using RSpec’s matcher DSL or writing one from scratch.

<br>

Imagine that you are writing a game in which players can be in various zones on a virtual board. To specify that bob
should be in zone 4, you could say:

```ruby
expect(bob.current_zone).to eq(Zone.new('4'))
```

<br>

But you might find it more expressive to say:
```ruby
expect(bob).to be_in_zone('4')
```

<br>

You can create such a matcher like so:
```ruby
RSpec::Matchers.define :be_in_zone do |zone|
  match do |player|
    player.in_zone?(zone)
  end
end
```

--

RSpec ships with a number of useful Expression Matchers. An Expression Matcher is any object that responds to the
following methods:
```ruby
matches?(actual)
failure_message
negative_failure_message  # optional
description               # optional
```
--

Also you can override the failure messages and the generated description:
```ruby
RSpec::Matchers.define :be_in_zone do |zone|
  match do |player|
    player.in_zone?(zone)
  end
  failure_message_for_should do |player|
    # generate and return the appropriate string.
  end
  failure_message_for_should_not do |player|
    # generate and return the appropriate string.
  end
  description do
    # generate and return the appropriate string.
  end
end
```

--

### Chaining custom matchers

You can also create matchers that obey a fluent interface using the chain method:
```ruby
RSpec::Matchers.define :have_errors_on do |attribute|
  chain :with_message do |message|
    @message = message
  end

  match do |model|
    model.valid?

    @has_errors = model.errors.key?(attribute)

    if @message
      @has_errors && model.errors[attribute].include?(@message)
    else
      @has_errors
    end
  end
end
```

And now it can be used as follows:

```ruby
RSpec.describe User do
  before { subject.email = 'foobar' }

  it { expect(subject).to have_errors_on(:email).with_message('Email has an invalid format') }
end
```

---

# Doubles

--

A `test double` is an object that stands in for another object in an example.
```ruby
thingamajig_double = double('thing-a-ma-jig')
```

The argument is a name, used for failure reporting, so you should use the role that the double is playing in the
example.

--

## Verifying doubles

Verifying doubles are a stricter alternative to normal doubles that provide guarantees about what is being verified.
When using verifying doubles, RSpec will check that the methods being stubbed are actually present on the underlying
object if it is available. Prefer using verifying doubles over normal doubles.

```ruby
# app/models/user.rb

class User
  MIN_AGE = 18

  def notify(msg)
    puts msg
  end
end

def call_user(user)
 "Hey!" if user.valid
end
```
<!-- .element: class="left width-50" -->

```ruby
# spec/models/user_spec.rb

user = instance_double('User', name: 'Peter')
expect(user).to receive(:notify).with('Warning!')

notifier = class_double('User')
  .as_stubbed_const(transfer_nested_constants: true)

expect(User::MIN_AGE).to eq(18)

user = object_double(User.new, valid: true)
expect(call_user(user)).to eq('Hey!')
```
<!-- .element: class="right width-50" -->

--

## Partial test doubles

A partial test double is an extension of a real object in a system that is instrumented with test-double like behaviour
in the context of a test.
```ruby
person = double('person')
allow(Person).to receive(:find) { person }
```

---

# Doubles, as_null_object

--

Test doubles are strict by default, raising errors when they receive messages that have not been allowed or expected.
You can chain `as_null_object` off of double in order to make the double "loose". For any message that has not
explicitly allowed or expected, the double will return itself. It acts as a black hole null object, allowing
arbitrarily deep method chains.

Use the `as_null_object` method to ignore any messages that aren't explicitly set as stubs or message expectations.
```ruby
RSpec.describe 'null object' do
  specify {
    null_object = double('null object').as_null_object
    expect(null_object).to respond_to(:any_undefined_method)
  }
end
```

---

# Method stubs

--

Test doubles are `strict` by default -- messages that have not been specifically allowed or expected will trigger an
error.
```ruby
class EmailConfirmationJob
  include Sidekiq::Worker

  def perform(user_id)
    user = User.find(user_id)
    UserMailer.send_confirmation_email(user)
  end
end

describe '#perform' do
  it 'finds the user by id' do
    allow(UserMailer).to receive(:send_confirmation_email)
    expect(User).to receive(:find).with(12)

    EmailConfirmationJob.new.perform(12)
  end
end
```

--

```ruby
class Statement
  def initialize(customer)
    @name = customer.name
  end

  def generate
    "Statement for #{@name}"
  end
end

RSpec.describe Statement do
  it "uses the customer's name in the header" do
    customer = double('customer')
    allow(customer).to receive(:name).and_return('Aslak')
    statement = Statement.new(customer)
    expect(statement.generate).to match(/^Statement for Aslak/)
  end
end
```

```ruby
RSpec.describe 'receive_messages' do
  it 'returns first and last names' do
    user = double('User')
    allow(user).to receive_messages(first_name: 'David', last_name: 'Masterson')
    expect(user.first_name).to eq('David')
    expect(user.last_name).to eq('Masterson')
  end
end
```

--

The mock object can be created with stubbed methods at once.
```ruby
customer = double('customer', name: 'Aslak')
obj = double('object', created_at: -> { Time.now })
```

--

Besides returning a value, method stub can yield a block, raise an exception, or throw the message.
```ruby
class Triviality
  def one_two_three
    yield self
  end
end

allow(triviality).to receive(:one_two_three).and_yield(triviality)
triviality.one_two_three { }
```

--

- `and_raise(ExceptionClass)`
- `and_raise('message')`
- `and_raise(ExceptionClass, 'message')`
- `and_raise(instance_of_an_exception_class)`

```ruby
allow(user).to receive(:some_method).and_raise(NoMethodError)
```

--

- `and_throw(:symbol)`
- `and_throw(:symbol, argument)`

```ruby
it 'includes the provided argument when throwing' do
  user = double
  allow(user).to receive(:confirm).and_throw(:section, 'I am not here any more')

  arg = catch :section do
    user.confirm
    fail 'should not get here'
  end

  expect(arg).to eq('I am not here any more')
end
```

---

# Removing stubs

--

Removes a stub. On a double, the object will no longer respond to message. On a real object, the original method (if it exists) is restored.

--

### New syntax

#### and_call_original

When working with a partial double object, you may occasionally want to set a message expecation without interfering with how the object responds to the message.
```ruby
RSpec.describe 'call original' do
  it 'calls original method' do
    allow(Modifier).to receive(:sum).and_call_original
    allow(Modifier).to receive(:sum).with(3, 4).and_return(-10)

    expect(Modifier.sum(1, 2)).to eq(3)
    expect(Modifier.sum(3, 4)).to eq(-10)
  end
end
```

--

### Old syntax

#### unstub (or unstub!)

```ruby
describe String do
  before(:each) { String.stub(:new).and_return('hello') }

  it "can restore it's own behavior" do
    expect(String.new('initial string')).to eq('hello')
    String.unstub(:new)

    expect(String.new('initial string')).to eq('initial string')
  end
end
```

---

# Stubbing constants

--

When the constant is already defined, the stubbed value will replace the original value for the duration of the
example.

--

### Stub top-level constant

```ruby
TOP_LEVEL_CONST = 100

RSpec.describe 'stubbing TOP_LEVEL_CONST' do
  it 'can stub TOP_LEVEL_CONST with a different value' do
    stub_const('TOP_LEVEL_CONST', 20)
    expect(TOP_LEVEL_CONST).to eq(20)
  end

  it 'restores the stubbed constant when the example completes' do
    expect(TOP_LEVEL_CONST).to eq(100)
  end
end
```

--

### Stub nested constant

```ruby
module Calculation
  class Statistic
    LEVEL = 15
  end
end

module Calculation
  RSpec.describe Statistic do
    it 'stubs the nested constant when it is fully qualified' do
      stub_const('Calculation::Statistic::LEVEL', 52)
      expect(Statistic::LEVEL).to eq(52)
    end
  end
end
```

--

### Transfer nested constants

```ruby
module Calculation
  class Statistic
    LEVEL = 15
  end
end

module Calculation
  RSpec.describe Statistic do
    let(:new_class) { Class.new }

    it 'does not transfer nested constants by default' do
      stub_const('Calculation::Statistic', new_class)
      expect { Statistic::LEVEL }.to raise_error(NameError)
    end

    it 'transfers nested constants when using transfer_nested_constants: true' do
      stub_const('Calculation::Statistic', new_class, transfer_nested_constants: true)
      expect(Statistic::LEVEL).to eq(15)
    end

    it 'can specify a list of nested constants to transfer' do
      stub_const('Calculation::Statistic', new_class, transfer_nested_constants:  [:LEVEL])
      expect(Statistic::LEVEL).to eq(15)
    end
  end
```

---

# Stub on any instance of a class

--

###  New syntax

```ruby
allow_any_instance_of(User).to receive(:name).and_return('User')
```

```ruby
RSpec.describe 'allow_any_instance_of' do
  it 'yields the receiver to the block implementation' do
    allow_any_instance_of(String).to receive(:slice) do |value, start, length|
      value[start, length]
    end

    expect('string'.slice(2, 3)).to eq('rin')
  end
end
```

--

###  Old syntax

Use any_instance.stub on a class to tell any instance of that class to return a value (or values) in response to a
given message. If no instance receives the message, nothing happens.

Messages can be stubbed on any class, including those in Ruby's core library.
```ruby
describe 'any_instance.stub' do
  it 'returns the specified value on any instance of the class' do
    String.any_instance.stub(:foo).and_return(:return_value)

    str = 'sample string'
    expect(str.foo).to eq(:return_value)
  end
end
```

---

# Stub a chain of methods

--

Stubbing methods chain lets you to stub a chain of methods in one statement - and there is no need to stub each method
in the dependency chain represented by a chain of messages to different objects.

--

### New syntax

```ruby
class User
  scope :admins, -> { where(role: 'admin').order("created_at DESC") }
end

RSpec.describe 'stubs method chain' do
  it 'returns admin' do
    admin = double('Admin')
    allow(User).to receive_message_chain(:where, :order).and_return([admin])
    // allow(User).to receive_message_chain("where.order") { [admin] }
    // allow(User).to receive_message_chain(:where, order:  [admin])
    // allow(User).to receive_message_chain(:where, :order) { [admin] }
    expect(User.admins).to include(admin)
  end
end
```

--

### Old syntax

```ruby
Article.recent.published.authored_by(params[:author_id])
```

```ruby
recent = double()
published = double()
authored_by = double()
article = double()
Article.stub(:recent).and_return(recent)
recent.stub(:published).and_return(published)
published.stub(:authored_by).and_return(article)
```

```ruby
article = double()
Article.stub_chain(:recent, :published, :authored_by).and_return(article)
```

---

# Stubs and before(:context)

--

Since `before(:context)` runs outside the scope of any individual example, usage of rspec-mocks features is not supported
there. You can, however, create a temporary scope in any arbitrary context, including in a `before(:context)` hook, using
`RSpec::Mocks.with_temporary_scope \{ }`.
```ruby
RSpec.describe 'Creating a double in a before(:context) hook' do
  before(:context) do
    RSpec::Mocks.with_temporary_scope do
      user = double(name: 'Alex')
      @result = user.name
    end
  end

  it 'allows a double to be created and used from within a with_temporary_scope block' do
    expect(@result).to eq('Alex')
  end
end
```

---

# Message expectations

--

A message expectation is an expectation that the test double will receive a message some time before the example ends.
If the message is received, the expectation is satisfied. If not, the example fails.
```ruby
RSpec.describe Zipcode do
  context 'when created' do
    it 'validates a record with provided validator' do
      validator = double('validator')
      expect(validator).to receive(:validate)

      zipcode = Zipcode.new('02134', validator)
      zipcode.valid?
    end
  end
end
```

For a negative expectation
```ruby
network_double.stub(:ping).and_return(false)
expect(network_double).not_to receive(:open_connection)
```

--

### Expecting Arguments

```ruby
expect(double).to receive(:msg).with(*args)
```

Arguments that are passed to with are compared with actual arguments received using `==`. In cases in which you want to
specify things about the arguments rather than the arguments themselves, you can use any of the matchers that ship with
rspec-expectations.
```ruby
expect(double).to receive(:msg).with(1, true)
expect(double).to receive(:msg).with(/bar/)                   # any String matching the submitted Regexp
expect(double).to receive(:msg).with(any_args)                # msg(), msg(1), msg(:bar, 2)
expect(double).to receive(:msg).with(1, any_args)             # msg(1), msg(1, :bar, 2)
expect(double).to receive(:msg).with(no_args)                 # msg()
expect(double).to receive(:msg).with(3, anything)             # msg(3, nil), msg(3, :bar)
expect(double).to receive(:msg).with(duck_type(:each))        # argument can be object that responds to #each
expect(double).to receive(:msg).with(3, boolean)              # msg(3, true), msg(3, false)
expect(double).to receive(:msg).with(hash_including(a: 1))    # msg(a: 1, b: 2)
expect(double).to receive(:msg).with(hash_excluding(a: 1))    # msg(b: 2)
expect(double).to receive(:msg).with(array_including(:a, :b)) # msg([:a, :b, :c])
expect(double).to receive(:msg).with(instance_of(Fixnum))     # any instance of Fixnum
expect(double).to receive(:msg).with(1, kind_of(Numeric))     # 2nd argument can be any kind of Numeric
expect(double).to receive(:msg).with(<matcher>)               # msg(<object that matches>)
```

--

### Receive Counts

The implicit expectation is that the message passed to should_receive will be called once. You can make the expected
counts explicit using the following
```ruby
expect(double).to receive(:msg).once
expect(double).to receive(:msg).twice
expect(double).to receive(:msg).exactly(n).times
expect(double).to receive(:msg).at_least(:once)
expect(double).to receive(:msg).at_least(:twice)
expect(double).to receive(:msg).at_least(n).times
expect(double).to receive(:msg).at_most(:once)
expect(double).to receive(:msg).at_most(:twice)
expect(double).to receive(:msg).at_most(n).times
```

--

### Ordering

When specifying interactions with a test double, the order of the calls is rarely important. In fact, the ideal
situation is to specify only a single call. But sometimes, we need to specify that messages are sent in a specific
order.
```ruby
RSpec.describe Roster do
  it 'asks database for count before adding' do
    database = double()
    student = double()

    expect(database).to receive(:count).with('Roster', course_id: 37).ordered
    expect(database).to receive(:add).with(student).ordered

    roster = Roster.new(37, database)
    roster.register(student)
  end
end
```

This example will pass only if the `count( )` and `add( )` messages are sent with the correct arguments and in the
same order.

--

### Setting responses

Whether you are setting a message expectation or a method stub, you can tell the object precisely how to respond. The
most generic way is to pass a block to stub or `should_receive`:
```ruby
expect(double).to receive(:msg) { value }
```

When the double receives the msg message, it evaluates the block and returns the result.

The same responses are available, as for stub method:
```ruby
expect(double).to receive(:msg).and_return(value)
expect(double).to receive(:msg).exactly(3).times.and_return(value1, value2, value3)
  # returns value1 the first time, value2 the second, etc
expect(double).to receive(:msg).and_raise(error)
  #error can be an instantiated object or a class
  #if it is a class, it must be instantiable with no args
expect(double).to receive(:msg).and_throw(:msg)
expect(double).to receive(:msg).and_yield(values,to,yield)
expect(double).to receive(:msg).and_yield(values,to,yield).and_yield(some,other,values,this,time)
  # for methods that yield to a block multiple times
```

---

# Spies

--

Spies are an alternate type of test double that support act-arrange-assert (or given-when-then) pattern for structuring
tests by allowing you to expect that a message has been received after the fact, using `have_received`.

--

### Using a spy

```ruby
RSpec.describe 'have_received' do
  it 'passes when the message has been received' do
    email = spy('email')
    email.deliver
    expect(email).to have_received(:deliver)
  end
end
```

--

### Spy on a method on a partial double

```ruby
class Email
  def self.deliver; end
end

RSpec.describe 'have_received' do
  it 'passes when the expectation is met' do
    allow(Email).to receive(:deliver)
    Email.deliver
    expect(Email).to have_received(:deliver)
  end
end
```

--

### Failure when the message has not been received

```ruby
class Email
  def self.deliver; end
end

RSpec.describe 'failure when the message has not been received' do
  example 'for a spy' do
    email = spy('email')
    expect(email).to have_received(:deliver)
  end

  example 'for a partial double' do
    allow(Email).to receive(:deliver)
    expect(Email).to have_received(:deliver)
  end
end
```

```bash
1) failure when the message has not been received for a spy
   Failure/Error: expect(email).to have_received(:deliver)
     (Double "email").deliver(*(any args))
         expected: 1 time with any arguments
         received: 0 times with any arguments
 2) failure when the message has not been received for a partial double
    Failure/Error: expect(Email).to have_received(:deliver)
     (Email (class)).deliver(*(any args))
         expected: 1 time with any arguments
         received: 0 times with any arguments
```

---

# So, let's create an application

--

### Introducing Codebreaker

Codebreaker is a logic game in which a code-breaker tries to break a secret code created by a code-maker. The
code-maker, which will be played by the application we’re going to write, creates a secret code of four numbers between
1 and 6.
<br>
<br>
Task details are [here](https://docs.google.com/document/d/1VW3Mk1W-pGkq0FadPih689_k971Zy8inzk6UCPHDLzs/edit?usp=sharing)

---

# Creating codebreaker gem

--

```bash
$ rvm use 2.3.0@codebreaker --create
ruby-2.3.0 - #gemset created /Users/ty/.rvm/gems/ruby-2.3.0@codebreaker
ruby-2.3.0 - #generating codebreaker wrappers - please wait
Using /Users/ty/.rvm/gems/ruby-2.3.0 with gemset codebreaker
```

```bash
$ gem install bundler
```

```bash
$ bundle gem codebreaker
  create  codebreaker/Gemfile
  create  codebreaker/Rakefile
  create  codebreaker/LICENSE.txt
  create  codebreaker/README.md
  create  codebreaker/.gitignore
  create  codebreaker/codebreaker.gemspec
  create  codebreaker/lib/codebreaker.rb
  create  codebreaker/lib/codebreaker/version.rb
  Initializing git repo in /Users/ty/Projects/codebreaker
```

--

codebreaker.gemspec <!-- .element class="filename" -->

```ruby
# ...
Gem::Specification.new do |spec|
  # ...

  spec.add_development_dependency 'rspec'
end
```

```bash
$ bundle install
```

---

# Describing Code with RSpec

--

### Now we're going to describe the expected behavior of instances of the Game class.

spec/spec_helper.rb <!-- .element class="filename" -->

```ruby
require 'bundler/setup'
require 'codebreaker'
```

spec/codebreaker/game_spec.rb <!-- .element class="filename" -->

```ruby
require 'spec_helper'

module Codebreaker
  RSpec.describe Game do
    describe '#start' do
      it 'generates secret code'
      it 'saves 4 numbers secret code'
      it 'saves secret code with numbers from 1 to 6'
    end
  end
end
```

```bash
$ rspec spec/codebreaker/game_spec.rb --format doc

/Users/ty/Projects/codebreaker/game_spec.rb:4:in '<module:Codebreaker>':
  uninitialized constant Codebreaker::Game (NameError)
...
```

--

### So let's add some code structure

lib/codebreaker.rb <!-- .element class="filename" -->

```ruby
require 'codebreaker/game'
```

lib/codebreaker/game.rb <!-- .element class="filename" -->

```ruby
module Codebreaker
  class Game
    def start
    end
  end
end
```

```bash
$ rspec spec/codebreaker/game_spec.rb --format doc

Codebreaker::Game
  #start
    generates secret code
    saves 4 numbers secret code
    saves secret code with numbers from 1 to 6
```

--

## Red: Start with a Failing Code Example

spec/codebreaker/game_spec.rb <!-- .element class="filename" -->

```ruby
require 'spec_helper'

module Codebreaker
  describe Game do
    describe '#start' do
      it 'saves secret code' do
        game = Game.new
        game.start
        expect(game.instance_variable_get(:@secret_code)).not_to be_empty
      end
      it 'saves 4 numbers secret code'
      it 'saves secret code with numbers from 1 to 6'
    end
  end
end
```

--

```bash
$ rspec spec/codebreaker/game_spec.rb
F**

Pending:
  Codebreaker::Game#start saves 4 numbers secret code
    # Not yet implemented
    # ./spec/codebreaker/game_spec.rb:35
  Codebreaker::Game#start saves secret code with numbers from 1 to 6
    # Not yet implemented
    # ./spec/codebreaker/game_spec.rb:36

Failures:

  1) Codebreaker::Game#start saves secret code
     Failure/Error: expect(game.instance_variable_get(:@secret_code)).not_to be_empty
       expected empty? to return false, got true
     # ./spec/codebreaker/game_spec.rb:33:in `block (3 levels) in <module:Codebreaker>'

Finished in 0.00842 seconds
3 examples, 1 failure, 2 pending

Failed examples:

rspec ./spec/codebreaker/game_spec.rb:30 # Codebreaker::Game#start saves secret code
```

--

## Green: Get the Example to Pass

lib/codebreaker/game.rb <!-- .element class="filename" -->

```ruby
module Codebreaker
  class Game
    def initialize
      @secret_code = ''
    end

    def start
      @secret_code = 'Secret Code, LOL :)'
    end
  end
end
```

```bash
$ rspec spec/codebreaker/game_spec.rb
.**

Pending:
  Codebreaker::Game#start saves 4 numbers secret code
    # Not yet implemented
    # ./spec/codebreaker/game_spec.rb:35
  Codebreaker::Game#start saves secret code with numbers from 1 to 6
    # Not yet implemented
    # ./spec/codebreaker/game_spec.rb:36

Finished in 0.00215 seconds
3 examples, 0 failures, 2 pending
```

--

## Next step

spec/codebreaker/game_spec.rb <!-- .element class="filename" -->

```ruby
require 'spec_helper'

module Codebreaker
  RSpec.describe Game do
    describe '#start' do
      it 'saves secret code' do
        game = Game.new
        game.start
        expect(game.instance_variable_get(:@secret_code)).not_to be_empty
      end

      it 'saves 4 numbers secret code' do
        game = Game.new
        game.start
        expect(game.instance_variable_get(:@secret_code).size).to eq 4
      end

      it 'saves secret code with numbers from 1 to 6'
    end
  end
end
```

--

```bash
$ rspec spec/codebreaker/game_spec.rb
.F*

Pending:
  Codebreaker::Game#start saves secret code with numbers from 1 to 6
    # Not yet implemented
    # ./spec/codebreaker/game_spec.rb:40

Failures:

  1) Codebreaker::Game#start saves 4 numbers secret code
     Failure/Error: expect(game.instance_variable_get(:@secret_code).size).to eq 4
       expected 4 items, got 19
     # ./spec/codebreaker/game_spec.rb:38:in `block (3 levels) in <module:Codebreaker>'

Finished in 0.02608 seconds
3 examples, 1 failure, 1 pending

Failed examples:

rspec ./spec/codebreaker/game_spec.rb:35 # Codebreaker::Game#start saves 4 numbers secret code
```

--

## Trying to get green again

lib/codebreaker/game.rb <!-- .element class="filename" -->

```ruby
module Codebreaker
  class Game
    def initialize
      @secret_code = ''
    end

    def start
      @secret_code = 'Secr'
    end
  end
end
```

```bash
$ rspec spec/codebreaker/game_spec.rb
..*

Pending:
  Codebreaker::Game#start saves secret code with numbers from 1 to 6
    # Not yet implemented
    # ./spec/codebreaker/game_spec.rb:40

Finished in 0.00314 seconds
3 examples, 0 failures, 1 pending
```

--

## Next step

spec/codebreaker/game_spec.rb <!-- .element class="filename" -->

```ruby
require 'spec_helper'

module Codebreaker
  RSpec.describe Game do
    describe '#start' do
      it 'saves secret code' do
        game = Game.new
        game.start
        expect(game.instance_variable_get(:@secret_code)).not_to be_empty
      end

      it 'saves 4 numbers secret code' do
        game = Game.new
        game.start
        expect(game.instance_variable_get(:@secret_code).size).to eq 4
      end

      it 'saves secret code with numbers from 1 to 6' do
        game = Game.new
        game.start
        expect(game.instance_variable_get(:@secret_code)).to match(/[1-6]+/)
      end
    end
  end
end
```

--

```bash
$ rspec spec/codebreaker/game_spec.rb
..F

Failures:

  1) Codebreaker::Game#start saves secret code with numbers from 1 to 6
     Failure/Error: expect(game.instance_variable_get(:@secret_code)).to match(/[1-6]+/)
       expected "Secr" to match /[1-6]+/
       Diff:
       @@ -1,2 +1,2 @@
       -/[1-6]+/
       +"Secr"
     # ./spec/codebreaker/game_spec.rb:43:in `block (3 levels) in <module:Codebreaker>'

Finished in 0.02563 seconds
3 examples, 1 failure

Failed examples:

rspec ./spec/codebreaker/game_spec.rb:40 # Codebreaker::Game#start saves secret code with numbers from 1 to 6
```

--

## Trying to get green again

lib/codebreaker/game.rb <!-- .element class="filename" -->

```ruby
module Codebreaker
  class Game
    def initialize
      @secret_code = ''
    end

    def start
      @secret_code = '1234'
    end
  end
end
```

```bash
$ rspec spec/codebreaker/game_spec.rb
...

Finished in 0.00409 seconds
3 examples, 0 failures
```

--

## Refactor

Refactoring is the process of changing a software system in such a way that it does not alter the external behavior
of the code yet improves its internal structure.

--

In this case, we have a very clear break between what is context and what is behavior, so let’s take advantage of that
and move the context to a block that is executed before each of the examples.

spec/codebreaker/game_spec.rb <!-- .element class="filename" -->

```ruby
module Codebreaker
  RSpec.describe Game do
    context '#start' do
      let(:game) { Game.new }

      before do
        game.start
      end

      it 'saves secret code' do
        expect(game.instance_variable_get(:@secret_code)).not_to be_empty
      end

      it 'saves 4 numbers secret code' do
        expect(game.instance_variable_get(:@secret_code).size).to eq 4
      end

      it 'saves secret code with numbers from 1 to 6' do
        expect(game.instance_variable_get(:@secret_code)).to match(/[1-6]+/)
      end
    end
  end
end
```

--

```bash
$ rspec spec/codebreaker/game_spec.rb
...

Finished in 0.00409 seconds
3 examples, 0 failures
MacBookPro-C8BCC89CA02E-2:codebreaker sparrow$ rspec spec/codebreaker/game_spec.rb
...

Finished in 0.00412 seconds
3 examples, 0 failures
```

---

# The End
