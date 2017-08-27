**Operation System: Ubuntu16.04**
# Requirements

1. Open Terminal
2. Check whether you have Ruby 2.1.0 or higher installed:
	```
	ruby --version
	Outputs:
	ruby 2.3.1p112 (2016-04-26) [x86_64-linux-gnu]
	```
3. If you don't have Ruby 2.1.0 or higher installed, just [install Ruby][1]:
	```
	sudo apt install ruby-full
	```
4. install Bundler:
	```
	sudo gem install bundler
	Outputs:
	Successfully installed bundler-1.15.4
	Parsing documentation for bundler-1.15.4
	Done installing documentation for bundler after 4 seconds
	1 gem installed
	```
5. If you already have a local repository for your Jekyll site, skip to Step 2.  

# Step 1: Create a local repository for your Jekyll site

1. If you haven't already downloaded Git, install it.
2. Open Terminal.
3. On your local computer, initialize a new Git repository for your Jekyll site:
	```
	git init JekyIItest
	```
4. `cd JekyIItest`
5. Create a new index.html as the home of your site:
	```
	 <!DOCTYPE html>
	 <html>
	 	<head>
	 		<meta charset="utf-8">
	 	</head>
	 	<body>
	 		Hello Jekyll!
	 	</body>
	 </html>
	```
> Note: You can skip this step 1.6 if you would rather use the master branch for
your Project Page. If you haven't checked out any branches, once you make a Community
in your local repository, your change will appear on the *master* branch by default.

6. If your new local repository is for a Project Page site, create a new gh-pages branch:
	```
	# Creates a new branch called 'gh-pages', and checks it out
	git checkout -b gh-pages
	```

# Step 2: Install Jekyll using bundler

1. create a new file Gemfile, and add these lines to Gemfile:
	```
	>>> vim Gemfile

	source 'https://rubygems.org'
	gem 'github-pages', group: :jekyll_plugins
	```
2. Make sure that the file which name is Gemfile should be saved to the root directory of your local Jekyll site repository.
3. Install Jekyll and other [dependencies][2] from the GitHub Pages gem:
	```
	bundle install
	Outputs:
	......
	-------------------------------------------------
	Thank you for installing html-pipeline!
	You must bundle Filter gem dependencies.
	See html-pipeline README.md for more details.
	https://github.com/jch/html-pipeline#dependencies
	-------------------------------------------------
	```

# Step 3: Build your local Jekyll site

1. Navigate into the root directory of your local Jekyll site repository.
2. Run your Jekyll site locally:
	```
	bundle exec jekyll serve
	Outputs:
	Source: /home/zj/JekyIItest
	Destination: /home/zj/JekyIItest/_site
	Incremental build: disabled. Enable with --incremental
	Generating...
			done in 0.011 seconds.
	Auto-regeneration: enabled for '/home/zj/JekyIItest'
	Server address: http://127.0.0.1:4000
	Server running... press ctrl-c to stop.
	```
3. **Congratulations**! You can preview your local Jekyll site in your web browser at http:/127.0.0.1:4000.

# Keeping your site up to date with the GitHub Pages gem

Jekyll is an activate open source project and is updated frequently. As the Gitub
Pages server is updated, the software on your computer may became out of date,
resulting in your sit appearing different locally from how it looks when published
on GitHub.
1. Open Terminal.
2. Run this update command:
    - If you followed our setup recommendation and installed Bundler, run `bundle update github-pages` or simply `bundle update` and your gem will update to the latest versions.
    - If you don't have Bundler installed, run `gem update github-paegs`.

[1]: https://www.ruby-lang.org/en/documentation/installation/#apt
[2]: https://pages.github.com/versions/
