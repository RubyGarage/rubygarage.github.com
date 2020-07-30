---
layout: slide
title:  Rails
---

# Rails

David Heinemeier Hansson (DHH), [37signals](http://37signals.com)

--

## The Rails philosophy includes two major guiding principles

`DRY` - "Don't Repeat Yourself" - suggests that writing the same code over and over again is a bad thing.

`Convention Over Configuration` - means that Rails makes assumptions about what you want to do and how you're going to
do it, rather than requiring you to specify every little thing through endless configuration files.

---

## Instaling Rails

### Preparing environment

```bash
$ rvm use 2.7.1@blog --create
Using /Users/ty/.rvm/gems/ruby-2.7.1 with gemset blog
```

--

## Installing Rails

### The latest stable version

```bash
$ gem install rails
```

```bash
$ gem install rails -v 6.0.3.2
```

---

## Creating rails application

```bash
$ rails new -h
Usage:
  rails new APP_PATH [options]

Options:
      [--skip-namespace], [--no-skip-namespace]              # Skip namespace (affects only isolated applications)
  -r, [--ruby=PATH]                                          # Path to the Ruby binary of your choice
                                                             # Default: /usr/share/rvm/rubies/ruby-2.6.5/bin/ruby
  -m, [--template=TEMPLATE]                                  # Path to some application template (can be a filesystem path or URL)
  -d, [--database=DATABASE]                                  # Preconfigure for selected database (options: mysql/postgresql/sqlite3/oracle/frontbase/ibm_db/sqlserver/jdbcmysql/jdbcsqlite3/jdbcpostgresql/jdbc)
                                                             # Default: sqlite3
      [--skip-gemfile], [--no-skip-gemfile]                  # Don't create a Gemfile
  -G, [--skip-git], [--no-skip-git]                          # Skip .gitignore file
      [--skip-keeps], [--no-skip-keeps]                      # Skip source control .keep files
  -M, [--skip-action-mailer], [--no-skip-action-mailer]      # Skip Action Mailer files
      [--skip-action-mailbox], [--no-skip-action-mailbox]    # Skip Action Mailbox gem
      [--skip-action-text], [--no-skip-action-text]          # Skip Action Text gem
  -O, [--skip-active-record], [--no-skip-active-record]      # Skip Active Record files
      [--skip-active-storage], [--no-skip-active-storage]    # Skip Active Storage files
  -P, [--skip-puma], [--no-skip-puma]                        # Skip Puma related files
  -C, [--skip-action-cable], [--no-skip-action-cable]        # Skip Action Cable files
  -S, [--skip-sprockets], [--no-skip-sprockets]              # Skip Sprockets files
      [--skip-spring], [--no-skip-spring]                    # Don't install Spring application preloader
      [--skip-listen], [--no-skip-listen]                    # Don't generate configuration that depends on the listen gem
  -J, [--skip-javascript], [--no-skip-javascript]            # Skip JavaScript files
      [--skip-turbolinks], [--no-skip-turbolinks]            # Skip turbolinks gem
  -T, [--skip-test], [--no-skip-test]                        # Skip test files
      [--skip-system-test], [--no-skip-system-test]          # Skip system test files
      [--skip-bootsnap], [--no-skip-bootsnap]                # Skip bootsnap gem
      [--dev], [--no-dev]                                    # Setup the application with Gemfile pointing to your Rails checkout
      [--edge], [--no-edge]                                  # Setup the application with Gemfile pointing to Rails repository
      [--rc=RC]                                              # Path to file containing extra configuration options for rails command
      [--no-rc], [--no-no-rc]                                # Skip loading of extra configuration options from .railsrc file
      [--api], [--no-api]                                    # Preconfigure smaller stack for API only apps
  -B, [--skip-bundle], [--no-skip-bundle]                    # Don't run bundle install
  --webpacker, [--webpack=WEBPACK]                           # Preconfigure Webpack with a particular framework (options: react, vue, angular, elm, stimulus)
      [--skip-webpack-install], [--no-skip-webpack-install]  # Don't run Webpack install

Runtime options:
  -f, [--force]                    # Overwrite files that already exist
  -p, [--pretend], [--no-pretend]  # Run but do not make any changes
  -q, [--quiet], [--no-quiet]      # Suppress status output
  -s, [--skip], [--no-skip]        # Skip files that already exist

Rails options:
  -h, [--help], [--no-help]        # Show this help message and quit
  -v, [--version], [--no-version]  # Show Rails version number and quit

Description:
    The 'rails new' command creates a new Rails application with a default
    directory structure and configuration at the path you specify.

    You can specify extra command-line arguments to be used every time
    'rails new' runs in the .railsrc configuration file in your home directory.

    Note that the arguments specified in the .railsrc file don't affect the
    defaults values shown above in this help message.

Example:
    rails new ~/Code/Ruby/weblog

    This generates a skeletal Rails installation in ~/Code/Ruby/weblog.
```

--

## Rails new

```bash
$ rails new blog
create
create  README.md
create  Rakefile
create  .ruby-version
create  config.ru
create  .gitignore
create  Gemfile
   run  git init from "."
Initialized empty Git repository in /home/user/temp/blog/.git/
create  package.json
create  app
create  app/assets/config/manifest.js
create  app/assets/stylesheets/application.css
create  app/channels/application_cable/channel.rb
create  app/channels/application_cable/connection.rb
create  app/controllers/application_controller.rb
create  app/helpers/application_helper.rb
create  app/javascript/channels/consumer.js
create  app/javascript/channels/index.js
create  app/javascript/packs/application.js
create  app/jobs/application_job.rb
create  app/mailers/application_mailer.rb
create  app/models/application_record.rb
create  app/views/layouts/application.html.erb
create  app/views/layouts/mailer.html.erb
create  app/views/layouts/mailer.text.erb
create  app/assets/images
create  app/assets/images/.keep
create  app/controllers/concerns/.keep
create  app/models/concerns/.keep
create  bin
create  bin/rails
create  bin/rake
create  bin/setup
create  bin/yarn
create  config
create  config/routes.rb
create  config/application.rb
create  config/environment.rb
create  config/cable.yml
create  config/puma.rb
create  config/spring.rb
create  config/storage.yml
create  config/environments
create  config/environments/development.rb
create  config/environments/production.rb
create  config/environments/test.rb
create  config/initializers
create  config/initializers/application_controller_renderer.rb
create  config/initializers/assets.rb
create  config/initializers/backtrace_silencers.rb
create  config/initializers/content_security_policy.rb
create  config/initializers/cookies_serializer.rb
create  config/initializers/cors.rb
create  config/initializers/filter_parameter_logging.rb
create  config/initializers/inflections.rb
create  config/initializers/mime_types.rb
create  config/initializers/new_framework_defaults_6_0.rb
create  config/initializers/wrap_parameters.rb
create  config/locales
create  config/locales/en.yml
create  config/master.key
append  .gitignore
create  config/boot.rb
create  config/database.yml
create  db
create  db/seeds.rb
create  lib
create  lib/tasks
create  lib/tasks/.keep
create  lib/assets
create  lib/assets/.keep
create  log
create  log/.keep
create  public
create  public/404.html
create  public/422.html
create  public/500.html
create  public/apple-touch-icon-precomposed.png
create  public/apple-touch-icon.png
create  public/favicon.ico
create  public/robots.txt
create  tmp
create  tmp/.keep
create  tmp/pids
create  tmp/pids/.keep
create  tmp/cache
create  tmp/cache/assets
create  vendor
create  vendor/.keep
create  test/fixtures
create  test/fixtures/.keep
create  test/fixtures/files
create  test/fixtures/files/.keep
create  test/controllers
create  test/controllers/.keep
create  test/mailers
create  test/mailers/.keep
create  test/models
create  test/models/.keep
create  test/helpers
create  test/helpers/.keep
create  test/integration
create  test/integration/.keep
create  test/channels/application_cable/connection_test.rb
create  test/test_helper.rb
create  test/system
create  test/system/.keep
create  test/application_system_test_case.rb
create  storage
create  storage/.keep
create  tmp/storage
create  tmp/storage/.keep
remove  config/initializers/cors.rb
remove  config/initializers/new_framework_defaults_6_0.rb
   run  bundle install
...
```

--

## Add `.ruby-version` and `.ruby-gemset`

```bash
$ cd blog
```

.ruby-version <!-- .element: class="filename" -->

```ruby
2.7.1
```

.ruby-gemset <!-- .element: class="filename" -->

```ruby
blog
```

---

## Directories structure

| File/Folder          | Purpose                                                                                                                                                                                                                                                                    |
| -------------        | ---------                                                                                                                                                                                                                                                                  |
| app/                 | Contains the controllers, models, views, helpers, mailers and assets for your application. You'll focus on this folder for the remainder of this guide.                                                                                                                    |
| bin/                 | Contains the rails script that starts your app and can contain other scripts you use to deploy or run your application.                                                                                                                                                    |
| config/              | Configure your application's runtime rules, routes, database, and more. This is covered in more detail in Configuring Rails Applications
| config.ru            | Rack configuration for Rack based servers used to start the application.                                                                                                                                                                                                   |
| db/                  | Contains your current database schema, as well as the database migrations.                                                                                                                                                                                                 |
| Gemfile Gemfile.lock | These files allow you to specify what gem dependencies are needed for your Rails application. These files are used by the Bundler gem. For more information about Bundler, see [the Bundler website](http://gembundler.com)                                                |
| lib/                 | Extended modules for your application.                                                                                                                                                                                                                                     |
| log/                 | Application log files.                                                                                                                                                                                                                                                     |

--

## Directories structure

| File/Folder          | Purpose                                                                                                                                                                                                                                                                    |
| -------------        | ---------                                                                                                                                                                                                                                                                  |
| public/              | The only folder seen to the world as-is. Contains the static files and compiled assets.                                                                                                                                                                                    |
| Rakefile             | This file locates and loads tasks that can be run from the command line. The task definitions are defined throughout the components of Rails. Rather than changing Rakefile, you should add your own tasks by adding files to the lib/tasks directory of your application. |
| README.md            | This is a brief instruction manual for your application. You should edit this file to tell others what your application does, how to set it up, and so on.                                                                                                                 |
| test/                | Unit tests, fixtures, and other test apparatus. These are covered in Testing Rails Applications
| tmp/                 | Temporary files (like cache, pid and session files)                                                                                                                                                                                                                        |
| vendor/              | A place for all third-party code. In a typical Rails application, this includes Ruby Gems and the Rails source code (if you optionally install it into your project).                                                                                                      |

---

## Gemfile

```ruby
source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '2.7.1'

# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
gem 'rails', '~> 6.0.3', '>= 6.0.3.1'
# Use sqlite3 as the database for Active Record
gem 'sqlite3', '~> 1.4'
# Use Puma as the app server
gem 'puma', '~> 4.1'
# Use SCSS for stylesheets
gem 'sass-rails', '>= 6'
# Transpile app-like JavaScript. Read more: https://github.com/rails/webpacker
gem 'webpacker', '~> 4.0'
# Turbolinks makes navigating your web application faster. Read more: https://github.com/turbolinks/turbolinks
gem 'turbolinks', '~> 5'
# Build JSON APIs with ease. Read more: https://github.com/rails/jbuilder
gem 'jbuilder', '~> 2.7'
# Use Redis adapter to run Action Cable in production
# gem 'redis', '~> 4.0'
# Use Active Model has_secure_password
# gem 'bcrypt', '~> 3.1.7'

# Use Active Storage variant
# gem 'image_processing', '~> 1.2'

# Reduces boot times through caching; required in config/boot.rb
gem 'bootsnap', '>= 1.4.2', require: false

group :development, :test do
  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
end

group :development do
  # Access an interactive console on exception pages or by calling 'console' anywhere in the code.
  gem 'web-console', '>= 3.3.0'
  gem 'listen', '~> 3.2'
  # Spring speeds up development by keeping your application running in the background. Read more: https://github.com/rails/spring
  gem 'spring'
  gem 'spring-watcher-listen', '~> 2.0.0'
end

group :test do
  # Adds support for Capybara system testing and selenium driver
  gem 'capybara', '>= 2.15'
  gem 'selenium-webdriver'
  # Easy installation and use of web drivers to run system tests with browsers
  gem 'webdrivers'
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
```

---

## Database config

config/database.yml <!-- .element: class="filename" -->

```yaml
# SQLite version 3.x
#   gem install sqlite3
#
#   Ensure the SQLite 3 gem is defined in your Gemfile
#   gem 'sqlite3'
#
default: &default
  adapter: sqlite3
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  timeout: 5000

development:
  <<: *default
  database: db/development.sqlite3

# Warning: The database defined as "test" will be erased and
# re-generated from your development database when you run "rake".
# Do not set this db to the same as development or production.
test:
  <<: *default
  database: db/test.sqlite3

production:
  <<: *default
  database: db/production.sqlite3
```

--

## Postgresql

```yaml
development:
  adapter: postgresql
  encoding: unicode
  database: blog_development
  username: root
  password:
```

## MySQL

```yaml
development:
  adapter: mysql2
  encoding: utf8
  database: blog_development
  username: root
  password:
  socket: /tmp/mysql.sock
```

---

## Creating the Database

```bash
$ rake db:create
```

## Starting up the Web Server

```bash
$ rails server
```

```bash
$ rails server -e production -p 6789
```

```bash
$ rails s
=> Booting Puma
=> Rails 6.0.3.2 application starting in development
=> Run `rails server --help` for more startup options
Puma starting in single mode...
* Version 4.3.5 (ruby 2.6.5-p114), codename: Mysterious Traveller
* Min threads: 5, max threads: 5
* Environment: development
* Listening on tcp://127.0.0.1:3000
* Listening on tcp://[::1]:3000
Use Ctrl-C to stop
```

---

## Generate scaffold

```bash
$ rails generate scaffold Post title:string text:text
  Running via Spring preloader in process 24696
  invoke  active_record
  create    db/migrate/20200730214810_create_posts.rb
  create    app/models/post.rb
  invoke    test_unit
  create      test/models/post_test.rb
  create      test/fixtures/posts.yml
  invoke  resource_route
   route    resources :posts
  invoke  scaffold_controller
  create    app/controllers/posts_controller.rb
  invoke    erb
  create      app/views/posts
  create      app/views/posts/index.html.erb
  create      app/views/posts/edit.html.erb
  create      app/views/posts/show.html.erb
  create      app/views/posts/new.html.erb
  create      app/views/posts/_form.html.erb
  invoke    test_unit
  create      test/controllers/posts_controller_test.rb
  create      test/system/posts_test.rb
  invoke    helper
  create      app/helpers/posts_helper.rb
  invoke      test_unit
  invoke    jbuilder
  create      app/views/posts/index.json.jbuilder
  create      app/views/posts/show.json.jbuilder
  create      app/views/posts/_post.json.jbuilder
  invoke  assets
  invoke    scss
  create      app/assets/stylesheets/posts.scss
  invoke  scss
  create    app/assets/stylesheets/scaffolds.scss
```

---

## Migrations

db/migrate/20200730214810_create_posts.rb <!-- .element: class="filename" -->

```ruby
class CreatePosts < ActiveRecord::Migration[6.0]
  def change
    create_table :posts do |t|
      t.string :title
      t.text :text

      t.timestamps
    end
  end
end
```

--

## Run migration

```bash
$ rake db:migrate

== CreatePosts: migrating ====================================================
-- create_table(:posts)
   -> 0.0020s
== CreatePosts: migrated (0.0021s) ===========================================
```

---

## DB schema

db/schema.rb <!-- .element: class="filename" -->

```ruby
ActiveRecord::Schema.define(version: 2020_07_30_214810) do

  create_table "posts", force: :cascade do |t|
    t.string "title"
    t.text "text"
    t.datetime "created_at", precision: 6, null: false
    t.datetime "updated_at", precision: 6, null: false
  end

end
```

---

## Routes

config/routes.rb <!-- .element: class="filename" -->

```ruby
Rails.application.routes.draw do
  resources :posts
end
```

```bash
$ rake routes

    Prefix  Verb   URI Pattern               Controller#Action
    posts   GET    /posts(.:format)          posts#index
            POST   /posts(.:format)          posts#create
 new_post   GET    /posts/new(.:format)      posts#new
edit_post   GET    /posts/:id/edit(.:format) posts#edit
     post   GET    /posts/:id(.:format)      posts#show
            PATCH  /posts/:id(.:format)      posts#update
            PUT    /posts/:id(.:format)      posts#update
            DELETE /posts/:id(.:format)      posts#destroy
```

---

## Models

app/models/post.rb before v5.0.0 <!-- .element: class="filename" -->

```ruby
class Post < ActiveRecord::Base
end
```

since v5.0.0 <!-- .element: class="filename" -->

```ruby
class Post < ApplicationRecord
end
```

```ruby
class ApplicationRecord < ActiveRecord::Base
  self.abstract_class = true
end
```

`abstract_class = true` tells Rails to not use `application_records` as table name for all classes inheriting `ApplicationRecord`.

---

## Controllers

app/controllers/posts_controller.rb <!-- .element: class="filename" -->

```ruby
class PostsController < ApplicationController
  before_action :set_post, only: [:show, :edit, :update, :destroy]

  # GET /posts
  # GET /posts.json
  def index
    @posts = Post.all
  end

  # GET /posts/1
  # GET /posts/1.json
  def show
  end

  # GET /posts/new
  def new
    @post = Post.new
  end

  # GET /posts/1/edit
  def edit
  end

  # POST /posts
  # POST /posts.json
  def create
    @post = Post.new(post_params)

    respond_to do |format|
      if @post.save
        format.html { redirect_to @post, notice: 'Post was successfully created.' }
        format.json { render :show, status: :created, location: @post }
      else
        format.html { render :new }
        format.json { render json: @post.errors, status: :unprocessable_entity }
      end
    end
  end

  # PATCH/PUT /posts/1
  # PATCH/PUT /posts/1.json
  def update
    respond_to do |format|
      if @post.update(post_params)
        format.html { redirect_to @post, notice: 'Post was successfully updated.' }
        format.json { render :show, status: :ok, location: @post }
      else
        format.html { render :edit }
        format.json { render json: @post.errors, status: :unprocessable_entity }
      end
    end
  end

  # DELETE /posts/1
  # DELETE /posts/1.json
  def destroy
    @post.destroy
    respond_to do |format|
      format.html { redirect_to posts_url, notice: 'Post was successfully destroyed.' }
      format.json { head :no_content }
    end
  end

  private
  # Use callbacks to share common setup or constraints between actions.
  def set_post
    @post = Post.find(params[:id])
  end

  # Only allow a list of trusted parameters through.
  def post_params
    params.require(:post).permit(:title, :text)
  end
end
```

---

## Listing posts

GET localhost:3000/posts <!-- .element: class="filename" -->

<div class="html-example">
<table>
<thead>
<tr>
<th>Title</th>
<th>Text</th>
<th></th>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td>Facebook’s New Colocation And Image Recognition Patents Tease The Future Of Sharing</td>
<td>Facebook’s empire was built on photo tags and sharing, but it’s a grueling process many neglect. Luckily, new Facebook patents give it tech to continuously capture video whenever your camera is open, rank and surface the best images, and auto-tag them with people, places, and businesses. They tease a future where pattern, facial, and audio recognition identify what you’re seeing for easy sharing.</td>
<td><a href="">Show</a></td>
<td><a href="">Edit</a></td>
<td><a href="">Destroy</a></td>
</tr>
</tbody>
</table>
<br />
<a href="">New Post</a>
</div>

GET localhost:3000/posts.json <!-- .element: class="filename" -->

```json
[
  {
    "title": "Facebook’s New Colocation And Image Recognition Patents Tease The Future Of Sharing",
    "text": "Facebook’s empire was built on photo tags and sharing, but it’s a grueling process many neglect. Luckily, new Facebook patents give it tech to continuously capture video whenever your camera is open, rank and surface the best images, and auto-tag them with people, places, and businesses. They tease a future where pattern, facial, and audio recognition identify what you’re seeing for easy sharing.",
    "url": "http://localhost:3000/posts/1.json"
  }
]
```

--

## Post Controller

app/controllers/posts_controller.rb <!-- .element: class="filename" -->

```ruby
class PostsController < ApplicationController

  # ...

  # GET /posts
  # GET /posts.json
  def index
    @posts = Post.all
  end

  # ...

end
```

--

## Post Index View

app/views/posts/index.html.erb <!-- .element: class="filename" -->

```html
<p id="notice"><%= notice %></p>

<h1>Posts</h1>

<table>
  <thead>
    <tr>
      <th>Title</th>
      <th>Text</th>
      <th colspan="3"></th>
    </tr>
  </thead>

  <tbody>
    <% @posts.each do |post| %>
      <tr>
        <td><%= post.title %></td>
        <td><%= post.text %></td>
        <td><%= link_to 'Show', post %></td>
        <td><%= link_to 'Edit', edit_post_path(post) %></td>
        <td><%= link_to 'Destroy', post, method: :delete, data: { confirm: 'Are you sure?' } %></td>
      </tr>
    <% end %>
  </tbody>
</table>

<br>

<%= link_to 'New Post', new_post_path %>
```

--

## Post Index JBuilder

app/views/posts/index.json.jbuilder <!-- .element: class="filename" -->

```ruby
json.array! @posts, partial: "posts/post", as: :post
```

app/views/posts/_post.json.jbuilder <!-- .element: class="filename" -->

```ruby
json.extract! post, :id, :title, :text, :created_at, :updated_at
json.url post_url(post, format: :json)
```

---

## New post

GET localhost:3000/posts/new <!-- .element: class="filename" -->

<div class="html-example">
<form accept-charset="UTF-8" action="" class="new_post" id="new_post" method="post">
<div>
<input name="utf8" type="hidden" value="&#x2713;" />
<input name="authenticity_token" type="hidden" value="n4Djzu/hPGSd5oMdGdfJ3sqePMR+E/1fs2679AMHLE0=" />
</div>
<div class="form-group">
<label for="post_title">Title</label>
<input id="post_title" class="form-control" name="post[title]" type="text" />
</div>
<div class="form-group">
<label for="post_text">Text</label>
<textarea id="post_text" class="form-control" name="post[text]"></textarea>
</div>
<div class="actions">
<input class="btn btn-default" name="commit" type="submit" value="Create Post" />
</div>
</form>
<br />
<a href="">Back</a>
</div>

app/controllers/posts_controller.rb <!-- .element: class="filename" -->

```ruby
class PostsController < ApplicationController

  # ...

  # GET /posts/new
  def new
    @post = Post.new
  end

  # ...

end
```

--

## Post Form

app/views/posts/new.html.erb <!-- .element: class="filename" -->

```html
<h1>New Post</h1>

<%= render 'form', post: @post %>

<%= link_to 'Back', posts_path %>
```

app/views/posts/_form.html.erb <!-- .element: class="filename" -->

```html
<%= form_with(model: post, local: true) do |form| %>
  <% if post.errors.any? %>
    <div id="error_explanation">
      <h2><%= pluralize(post.errors.count, "error") %> prohibited this post from being saved:</h2>

      <ul>
        <% post.errors.full_messages.each do |message| %>
          <li><%= message %></li>
        <% end %>
      </ul>
    </div>
  <% end %>

  <div class="field">
    <%= form.label :title %>
    <%= form.text_field :title %>
  </div>

  <div class="field">
    <%= form.label :text %>
    <%= form.text_area :text %>
  </div>

  <div class="actions">
    <%= form.submit %>
  </div>
<% end %>
```

---

## Create post

app/controllers/posts_controller.rb <!-- .element: class="filename" -->

```ruby
class PostsController < ApplicationController

  # ...

  # POST /posts
  # POST /posts.json
  def create
    @post = Post.new(post_params)

    respond_to do |format|
      if @post.save
        format.html { redirect_to @post, notice: 'Post was successfully created.' }
        format.json { render :show, status: :created, location: @post }
      else
        format.html { render :new }
        format.json { render json: @post.errors, status: :unprocessable_entity }
      end
    end
  end

  # ...

end
```

---

## Show post

GET localhost:3000/posts/1 <!-- .element: class="filename" -->

<div class="html-example">
Post was successfully created.
<br>
<br>
<b>Title:<b> Facebook’s New Colocation And Image Recognition Patents Tease The Future Of Sharing
<br>
<br>
<b>Text:</b> Facebook’s empire was built on photo tags and sharing, but it’s a grueling process many neglect. Luckily, new Facebook patents give it tech to continuously capture video whenever your camera is open, rank and surface the best images, and auto-tag them with people, places, and businesses. They tease a future where pattern, facial, and audio recognition identify what you’re seeing for easy sharing.
<br>
</div>

GET localhost:3000/posts/1.json <!-- .element: class="filename" -->

```json
{
  "title": "Facebook’s New Colocation And Image Recognition Patents Tease The Future Of Sharing ",
  "text": "Facebook’s empire was built on photo tags and sharing, but it’s a grueling process many neglect. Luckily, new Facebook patents give it tech to continuously capture video whenever your camera is open, rank and surface the best images, and auto-tag them with people, places, and businesses. They tease a future where pattern, facial, and audio recognition identify what you’re seeing for easy sharing.",
  "created_at": "2013-06-09T17:07:29.179Z",
  "updated_at": "2013-06-09T17:07:29.179Z"
}
```

--

## Post Controller

app/controllers/posts_controller.rb <!-- .element: class="filename" -->

```ruby
class PostsController < ApplicationController

  # ...

  # GET /posts/1
  # GET /posts/1.json
  def show
  end

  # ...

end
```

--

## Post View

app/views/posts/show.html.erb <!-- .element: class="filename" -->

```html
<p id="notice"><%= notice %></p>

<p>
  <strong>Title:</strong>
  <%= @post.title %>
</p>

<p>
  <strong>Text:</strong>
  <%= @post.text %>
</p>

<%= link_to 'Edit', edit_post_path(@post) %> |
<%= link_to 'Back', posts_path %>
```

app/views/posts/show.json.jbuilder <!-- .element: class="filename" -->

```ruby
json.partial! "posts/post", post: @post
```

app/views/posts/_post.json.jbuilder <!-- .element: class="filename" -->

```ruby
json.extract! post, :id, :title, :text, :created_at, :updated_at
json.url post_url(post, format: :json)

```

---

## Edit post

GET localhost:3000/posts/1/edit <!-- .element: class="filename" -->

<div class="html-example">
<form accept-charset="UTF-8" action="/posts" class="new_post" id="new_post" method="post">
<div>
<input name="utf8" type="hidden" value="&#x2713;" />
<input name="authenticity_token" type="hidden" value="n4Djzu/hPGSd5oMdGdfJ3sqePMR+E/1fs2679AMHLE0=" />
</div>
<div class="form-group">
<label for="post_title">Title</label>
<input id="post_title" class="form-control" name="post[title]" type="text" value="Facebook’s New Colocation And Image Recognition Patents Tease The Future Of Sharing" />
</div>
<div class="form-group">
<label for="post_text">Text</label>
<textarea id="post_text" class="form-control" name="post[text]" rows="4">Facebook’s empire was built on photo tags and sharing, but it’s a grueling process many neglect. Luckily, new Facebook patents give it tech to continuously capture video whenever your camera is open, rank and surface the best images, and auto-tag them with people, places, and businesses. They tease a future where pattern, facial, and audio recognition identify what you’re seeing for easy sharing.</textarea>
</div>
<div class="actions">
<input class="btn btn-default" name="commit" type="submit" value="Update Post" />
</div>
</form>
<br />
<a href="">Show</a> |
<a href="">Back</a>
</div>

app/controllers/posts_controller.rb <!-- .element: class="filename" -->

```ruby
class PostsController < ApplicationController

  # ...

  # GET /posts/1/edit
  def edit
  end

  # ...

end
```

--

app/views/posts/edit.html.erb <!-- .element: class="filename" -->

```html
<h1>Editing Post</h1>

<%= render 'form', post: @post %>

<%= link_to 'Show', @post %> |
<%= link_to 'Back', posts_path %>
```

app/views/posts/_form.html.erb <!-- .element: class="filename" -->

```html
<%= form_with(model: post, local: true) do |form| %>
  <% if post.errors.any? %>
    <div id="error_explanation">
      <h2><%= pluralize(post.errors.count, "error") %> prohibited this post from being saved:</h2>

      <ul>
        <% post.errors.full_messages.each do |message| %>
          <li><%= message %></li>
        <% end %>
      </ul>
    </div>
  <% end %>

  <div class="field">
    <%= form.label :title %>
    <%= form.text_field :title %>
  </div>

  <div class="field">
    <%= form.label :text %>
    <%= form.text_area :text %>
  </div>

  <div class="actions">
    <%= form.submit %>
  </div>
<% end %>
```

---

## Update Post

app/controllers/posts_controller.rb <!-- .element: class="filename" -->

```ruby
class PostsController < ApplicationController

  # ...

  # PATCH/PUT /posts/1
  # PATCH/PUT /posts/1.json
  def update
    respond_to do |format|
      if @post.update(post_params)
        format.html { redirect_to @post, notice: 'Post was successfully updated.' }
        format.json { render :show, status: :ok, location: @post }
      else
        format.html { render :edit }
        format.json { render json: @post.errors, status: :unprocessable_entity }
      end
    end
  end

  # ...

end
```

```html
<form accept-charset="UTF-8" action="/posts/1" class="edit_post" id="edit_post_1" method="post">
  <div>
    <input name="utf8" type="hidden" value="✓" />
    <input name="_method" type="hidden" value="patch" />
    <input name="authenticity_token" type="hidden" value="n4Djzu/hPGSd5oMdGdfJ3sqePMR+E/1fs2679AMHLE0=" />
  </div>
</form>
```

---

## Delete post

app/controllers/posts_controller.rb <!-- .element: class="filename" -->

```ruby
class PostsController < ApplicationController

  # ...

  # DELETE /posts/1
  # DELETE /posts/1.json
  def destroy
    @post.destroy
    respond_to do |format|
      format.html { redirect_to posts_url, notice: 'Post was successfully destroyed.' }
      format.json { head :no_content }
    end
  end

  # ...

end
```

```html
<form accept-charset="UTF-8" action="/posts/1" class="edit_post" id="edit_post_1" method="post">
  <input name="_method" type="hidden" value="delete" />

  ...

</form>
```

---

## Layout

app/views/layouts/application.html.erb <!-- .element: class="filename" -->

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Blog</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <%= yield %>
  </body>
</html>
```

---

## Application Controller

app/controllers/application_controller.rb <!-- .element: class="filename" -->

```ruby
class ApplicationController < ActionController::Base
  # Prevent CSRF attacks by raising an exception.
  # For APIs, you may want to use :null_session instead.
  protect_from_forgery with: :exception
end
```

---

## Helpers

app/helpers/posts_helper.rb <!-- .element: class="filename" -->

```ruby
module PostsHelper
  def post_short_description(post)
    return post.text if post.text.length <= 30

    post.text.slice(0, 27).concat("...")
  end

  def news_count
    "News count is (#{ Post.where('title LIKE ?', '%news%').count })"
  end
end
```

app/views/posts/index.html.erb <!-- .element: class="filename" -->

```html
<h1>Posts</h1>

<p><%= news_count %></p>

<table>
  <thead>
    <tr>
      <th>Title</th>
      <th>Text</th>
      <th colspan="3"></th>
    </tr>
  </thead>

  ...

</table>
```

---

## Assets

app/javascript/packs/application.js <!-- .element: class="filename" -->

```javascript
require("@rails/ujs").start()
require("turbolinks").start()
require("@rails/activestorage").start()
require("channels")
```

app/assets/stylesheets/application.css <!-- .element: class="filename" -->

```css
/*
 *= require_self
 *= require_tree .
 */
```

--

## Layout

```html
<!--
<!DOCTYPE html>
<html>
  <head>
    <title>Blog</title>
    <meta name="csrf-param" content="authenticity_token" />
<meta name="csrf-token" content="l+gq/e/RzeQzbgRi4pY1H71ff2y4lRmKK8iV4f3osLh1bRgA9ipOdbDQxZABF6aM3kYUMp+gh2AcLRWA2QAzOg==" />

    <link rel="stylesheet" media="all" href="/assets/application.debug-86435a3da7ccdbdbe471db77c4e963257e72df29b5dd28831a9d47af7daf59d7.css" data-turbolinks-track="reload" />
    <script src="/packs/js/application-9afcbb5693aa87623e69.js" data-turbolinks-track="reload"></script>
  </head>

  <body>

    ...

  </body>
</html>
-->
```

---

# The End
