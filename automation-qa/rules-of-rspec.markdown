---
layout: slide
title: Rules of Rspec
---

## Rules of Rspec

- `let` and `let!`

- Hooks types 
  - `before`
  
  - `after`

  - `around`

- `db cleaning`

---

## How works `let`

Use `let` to define a `memoized` helper method. The value will be cached across multiple calls in the same example but not across examples. Note that `let` is `lazy-evaluated`: it is not evaluated until the first time the method it defines is invoked.

In Ruby, it’s common to use `memoization` to make sure that instance variables in a method only get set once regardless of how many times the method is called.

--

If you call `let` multiple times in the same example, it evaluates the let block just once (the first time it’s called).

```ruby
describe GetTime do
  let(:current_time) { Time.now }

  it "gets the same time over and over again" do
    puts current_time # => 2018-07-19 09:35:29 +0300
    sleep(3)
    puts current_time # => 2018-07-19 09:35:29 +0300
  end

  it "gets the time again" do
    puts current_time # => 2018-07-19 09:35:32 +0300
  end
end
```

As you can see, in the first example (the first `it` block), even though there is a three-second delay between the two calls to `current_time`, the value returned is the same.

However, when you call it again in the second `it` block, the `{ Time.now }` block gets re-evaluated. And, as before, the value is cached for all the subsequent calls inside that second block.

---

##  How works `let!`

You can use `let!` to force the method’s invocation before each example.

The difference between `let`, and `let!` is that `let!` is called in an implicit before block. So the result is evaluated and cached before the `it` block.

```ruby
describe "GetTime" do
  let!(:current_time) { Time.now }

  before(:each) do
    puts Time.now # => 2018-07-19 09:57:52 +0300
  end

  it "gets the time" do
    sleep(3)
    puts current_time # => 2018-07-19 09:57:52 +0300
  end
end
```

This behavior is useful when you need to set some state before the `it` block runs.

---

## RSpec - Hooks

Provides `before`, `after` and `around` hooks as a means of supporting common setup and teardown. This module is extended on to `ExampleGroup`, making the methods available from any `describe` or `context` block.

The most common hooks used in RSpec are `before` and `after` hooks. They provide a way to define and run the setup and teardown code.

--

### Hooks types

- **after**

  ```ruby
  after(*args, &block)
  ```

  Declare a block of code to be run after each example (using `:example`) or once after all examples in the context (using `:context`).

- **around**

  ```ruby
  around(*args) {|Example| ... }
  ```

  Declare a block of code, parts of which will be run before and parts after the example.

- **before**

  ```ruby
  before(*args, &block)
  ```

  Declare a block of code to be run before each example (using `:example`) or once before any example (using `:context`).

  **`Note`**: The `:example` and `:context` scopes are also available as `:each` and `:all`, respectively. Use whichever you prefer.
  
--

### Here is a simple example that illustrates when each hook is called.

```ruby
describe "Before and after hooks" do 
   before(:each) do 
      puts "Runs before each Example" 
   end 
   after(:each) do 
      puts "Runs after each Example" 
   end 
   before(:all) do 
      puts "Runs before all Examples" 
   end 
   after(:all) do 
      puts "Runs after all Examples"
   end 

   it 'is the first Example in this spec file' do 
      puts 'Running the first Example' 
   end 

   it 'is the second Example in this spec file' do 
      puts 'Running the second Example' 
   end 
end
```

```
Runs before all Examples 
Runs before each Example 
Running the first Example 
Runs after each Example 
.Runs before each Example 
Running the second Example 
Runs after each Example 
.Runs after all Examples
```

--

The syntax of around is similar to that of `before` and `after` but the semantics are quite different. `before` and `after` hooks are run in the context of of the examples with which they are associated, whereas `around` hooks are actually responsible for running the examples. Consequently, `around` hooks do not have direct access to resources that are made available within the examples and their associated `before` and `after` hooks.


```ruby
RSpec.describe "around hook" do
  around(:each) do |example|
    puts "around example before"
    example.run
    puts "around example after"
  end

  it "gets run in order" do
    puts "in the example"
  end
end
```
Output should contain:

```
around example before
in the example
around example after
```

---

# Database cleaning

---

## Setup Database cleaning

### If you are using Rails later than 5.1.5

The main idea `Database cleaning` is to start each example with a clean database, create whatever data
is necessary for that example, and then remove that data by simply rolling back
the `transaction` at the end of the example.

--

Make sure that `use_transactional_fixtures = true` it will run every example within a transaction

spec/rails_helper.rb <!-- .element: class="filename" -->

```ruby
config.use_transactional_fixtures = true
```

Define `basic_configure` file, which manages the Capybara driver configuration:

spec/support/basic_configure.rb <!-- .element: class="filename" -->

```ruby
RSpec.configure do |config|
  config.before(:each, type: :system) do
    driven_by :rack_test
  end

  config.before(:each, type: :system, js: true) do
    driven_by :selenium_chrome_headless
  end
end
```

`driven_by` - is Rails method which manages the Capybara driver configuration. The argument to driven_by is the Capybara driver.

`:type` - is rspec-rails method which define directory structure (system, feature, model, controller, [etc](https://relishapp.com/rspec/rspec-rails/v/3-9/docs/directory-structure).)

`:system` - is system specs are RSpec's wrapper around Rails' own [system tests](https://relishapp.com/rspec/rspec-rails/docs/system-specs/system-spec)

--

### Data created in before(`:each`) are **rolled back**

Any data you create in a before(`:each`) hook will be rolled back at the end of
the example. This is a good thing because it means that each example is
isolated from state that would otherwise be left around by the examples that
already ran. For example:

```ruby
describe Widget do
  before(:each) do
    @widget = Widget.create
  end

  it "does something" do
    expect(@widget).to do_something
  end

  it "does something else" do
    expect(@widget).to do_something_else
  end
end
```

The `@widget` is recreated in each of the two examples above, so each example
has a different object, and the underlying data is rolled back so the data
backing the `@widget` in each example is new.

`Note` Data created in before(`:all`) are **not rolled back**

---

## Setup Database cleaning

### If you are using Rails earlier than 5.1.5

Earlier versions of Rails 5.1 had a defect in ActionDispatch::SystemTesting::Server that caused problems with previous method of cleaning database.

--

The first thing we need to do is add our gem to Gemfile in `:test` group

```ruby
group :test do
  gem "database_cleaner"
  gem "selenium-webdriver" # from box only in Rails later than 5.1
end
```

Then, run `bundle` to download and instal new gem

```bash
$ bundle install
```

Change `use_transactional_fixtures = false` this will disable rspec-rails’ implicit wrapping of tests in a
database transaction. 

spec/rails_helper.rb <!-- .element: class="filename" -->

```ruby
config.use_transactional_fixtures = false
```

--

Define `database_cleaner` file, which manages the [Database cleaner](https://github.com/DatabaseCleaner/database_cleaner) configuration:

spec/support/database_cleaner.rb <!-- .element: class="filename" -->

```ruby
RSpec.configure do |config|
  config.before(:suite) do
    DatabaseCleaner.clean_with(:truncation)
  end

  config.before(:each) do
    DatabaseCleaner.strategy = :transaction
  end

  config.before(:each, :js => true) do
    DatabaseCleaner.strategy = :truncation
  end

  config.before(:each) do
    DatabaseCleaner.start
  end

  config.after(:each) do
    DatabaseCleaner.clean
  end
end
```
