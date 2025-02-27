+++
title = "Writing Command Line Tools with Ruby"
date = 2015-02-13T17:16:00Z
weight = 100

[taxonomies]
tags = ["LinuxDev", "Business and Legal", "Ruby"]

+++

I've written a lot of Ruby code over the years from web applications, to rack frameworks, to rake tasks, even packaged a few up as gems, but one thing I've never done is write a command line tool directly in ruby. This post just sums up my initial foray into making Ruby cli tools, as usual with Ruby it's not nearly as hard as it sounds.

<!-- more -->

## The Basics

Typically when you write a ruby script you execute it with the Ruby command followed by a file path, like so:

~~~
$ ruby ../path/to/some_example.rb
~~~

But that puts a lot of weight on the user, they need to know 1) this is a Ruby program, 2) where it was 'installed', and 3) the file extension for Ruby. The API we want is this:

~~~
$ some_example
~~~

To accomplish this we first need to add a 'shebang' to the top of our main entry point to the application, like this:

~~~
#!/usr/bin/env ruby
~~~

This line tells the shell how we want the following file interpreted. We could hard code a path to ruby, but by using the env dir we let the user's shell decide what ruby is, this way people can install ruby however they want and our program will still run. To run the program directly we also need to make it executable:

~~~
$ chmod +x ../path/to/some_example.rb
~~~

And now the program can be run without specifying Ruby:

~~~
$ ../path/to/some_example.rb
~~~

Or we can optionally leave off the Ruby extension (.rb) and run it without any knowledge that it is Ruby under the hood:

~~~
$ mv ../path/to/some_example.rb ../path/to/some_example
$ ../path/to/some_example
~~~

But what about that annoying `../path/to/` nonsense, the user shouldn't have to even know, much less have to type the full path to the program to run it. To solve this we have two main options (though there are certainly a number of ways to accomplish this).

The first and 'easiest' approach is to simply add the executable to the users PATH either in the shell, a init script, or by typing it right in the shell:

~~~
$ export PATH=/abs/path/to/some_example:$PATH
$ some_example
~~~

This prepends our code to the lookup PATH ($PATH is a variable for the current PATH, the colon separates different parts of the PATH) so that we don't need to know where the code is located in order to execute it.

This meets our original requirements, but comes with a number of problems. Are we going to make the user manage the PATH themselves? Is this run with an install shell script? What it the users' shell of choice doesn't use the `export` API? What if they want to move where the install directory is on their computer? All these questions lead us to believe there must be a better or at least more standardized approach to this.

And as it turns out there is! The people behind RubyGems have put a lot of thought into this, so that when you create a gem you can define a set of files that can be used as executables and it then copies them to `#{ruby-prefix}/bin/{#gem_name}`, which is already added to their PATH during the installation of Ruby and is managed by tools like rbenv, chruby, or RVM so that you don't have to.

The downside to this is that their is a bit of extra boilerplate needed to comply with the whole gemspec standard, but in the long run this is well worth the extra startup time. Luckily the bundler gem, a popular gem manager (that itself is a gem), comes with a scaffold-er to keep the amount of boilerplate you need to write to a minimum as well as giving you a set of best-practices/conventions that the rest of the Ruby community often follows. To create a new project run `bundler gem #{your_gem_name_here}`, which initializes a git repo and gives us the following file structure:

~~~
$ tree
├── Gemfile
├── LICENSE.txt
├── README.md
├── Rakefile
├── gem_cli.gemspec
└── lib
    ├── gem_cli
    │   └── version.rb
    └── gem_cli.rb

2 directories, 7 files
~~~

By default it gives you a copy of the MIT license, this is by far the most popular license within the Ruby community, but you are free to change it to whatever you like (just make sure you update those changes in your gemspec as well). You should also add your dependencies in the Gemfile (if you have any), add your code to the `lib/` dir, and then create a new `bin/` dir with the cli code (which hopefully require's whatever the rest of your lib does for DRY purposes). Then it's just a matter of updating the `*.gemspec` file to meet your requirements. The key bit that bundler gives us by default is what does the making `bin/` executable business:

~~~
  spec.files         = `git ls-files -z`.split("\x0")
  spec.executables   = spec.files.grep(%r{^bin/}) { |f| File.basename(f) }
  spec.test_files    = spec.files.grep(%r{^(test|spec|features)/})
  spec.require_paths = ["lib"]
~~~

The first line adds only files tracked by git (a classic error is not adding changes to git before building if you leave this line in), you can of course use any other Ruby/shell code to grab the paths you want. The second line does the job of telling RubyGems what files to add to the users path, basically it looks through the list of files regex-ing for the bin and adding the files in that dir. Of course if you don't want to put your executables in `bin/`, you could rename that dir and regex for that something different here. Bin is just a convention of course and the `*.gemspec` file is just a plain old Ruby file, so anything you want to add here will work just fine.
