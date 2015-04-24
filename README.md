An example of the rugged gem on Heroku. It requires cmake during the build so we include it in the Aptfile.

Be sure to set the Multi buildpack on your app before pushing:

```
$ heroku buildpack:set https://github.com/heroku/heroku-buildpack-multi.git
```

Here is what it displays when building:

```
$ git push heroku master
Counting objects: 9, done.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (9/9), 751 bytes | 0 bytes/s, done.
Total 9 (delta 1), reused 0 (delta 0)
remote: Compressing source files... done.
remote: Building source:
remote: 
remote: -----> Fetching custom git buildpack... done
remote: -----> Multipack app detected
remote: =====> Downloading Buildpack: https://github.com/ddollar/heroku-buildpack-apt.git
remote: =====> Detected Framework: Apt
remote: -----> Updating apt caches
remote:        Ign http://archive.ubuntu.com trusty InRelease
remote:        Ign http://archive.ubuntu.com trusty-security InRelease
remote:        Ign http://archive.ubuntu.com trusty-updates InRelease
remote:        Get:1 http://archive.ubuntu.com trusty Release.gpg [933 B]
remote:        Get:2 http://archive.ubuntu.com trusty-security Release.gpg [933 B]
remote:        Get:3 http://archive.ubuntu.com trusty-updates Release.gpg [933 B]
remote:        Get:4 http://archive.ubuntu.com trusty Release [58.5 kB]
remote:        Get:5 http://archive.ubuntu.com trusty-security Release [63.5 kB]
remote:        Get:6 http://archive.ubuntu.com trusty-updates Release [63.5 kB]
remote:        Get:7 http://archive.ubuntu.com trusty/main amd64 Packages [1,350 kB]
remote:        Get:8 http://archive.ubuntu.com trusty/universe amd64 Packages [5,859 kB]
remote:        Get:9 http://archive.ubuntu.com trusty/main Translation-en [762 kB]
remote:        Get:10 http://archive.ubuntu.com trusty/universe Translation-en [4,089 kB]
remote:        Get:11 http://archive.ubuntu.com trusty-security/main amd64 Packages [259 kB]
remote:        Get:12 http://archive.ubuntu.com trusty-security/main Translation-en [131 kB]
remote:        Get:13 http://archive.ubuntu.com trusty-updates/main amd64 Packages [502 kB]
remote:        Get:14 http://archive.ubuntu.com trusty-updates/main Translation-en [237 kB]
remote:        Ign http://archive.ubuntu.com trusty/main Translation-en_US
remote:        Ign http://archive.ubuntu.com trusty/universe Translation-en_US
remote:        Fetched 13.4 MB in 8s (1,667 kB/s)
remote:        Reading package lists...
remote: -----> Fetching .debs for cmake
remote:        Reading package lists...
remote:        Building dependency tree...
remote:        The following extra packages will be installed:
remote:          cmake-data libarchive13 libnettle4
remote:        Suggested packages:
remote:          codeblocks eclipse lrzip
remote:        The following NEW packages will be installed:
remote:          cmake cmake-data libarchive13 libnettle4
remote:        0 upgraded, 4 newly installed, 0 to remove and 63 not upgraded.
remote:        Need to get 3,674 kB of archives.
remote:        After this operation, 17.7 MB of additional disk space will be used.
remote:        Get:1 http://archive.ubuntu.com/ubuntu/ trusty/main libnettle4 amd64 2.7.1-1 [121 kB]
remote:        Get:2 http://archive.ubuntu.com/ubuntu/ trusty-security/main libarchive13 amd64 3.1.2-7ubuntu2.1 [259 kB]
remote:        Get:3 http://archive.ubuntu.com/ubuntu/ trusty/main cmake-data all 2.8.12.2-0ubuntu3 [676 kB]
remote:        Get:4 http://archive.ubuntu.com/ubuntu/ trusty/main cmake amd64 2.8.12.2-0ubuntu3 [2,618 kB]
remote:        Fetched 3,674 kB in 2s (1,714 kB/s)
remote:        Download complete and in download only mode
remote: -----> Installing cmake_2.8.12.2-0ubuntu3_amd64.deb
remote: -----> Installing cmake-data_2.8.12.2-0ubuntu3_all.deb
remote: -----> Installing libarchive13_3.1.2-7ubuntu2.1_amd64.deb
remote: -----> Installing libnettle4_2.7.1-1_amd64.deb
remote: -----> Writing profile script
remote: =====> Downloading Buildpack: https://github.com/heroku/heroku-buildpack-ruby.git
remote: =====> Detected Framework: Ruby
remote: -----> Compiling Ruby
remote: -----> Using Ruby version: ruby-2.0.0
remote: -----> Installing dependencies using 1.7.12
remote:        Running: bundle install --without development:test --path vendor/bundle --binstubs vendor/bundle/bin -j4 --deployment
remote:        Fetching gem metadata from https://rubygems.org/..
remote:        Using bundler 1.7.12
remote:        Installing rugged 0.21.4
remote:        Your bundle is complete!
remote:        Gems in the groups development and test were not installed.
remote:        It was installed into ./vendor/bundle
remote:        Bundle completed (59.84s)
remote:        Cleaning up the bundler cache.
remote: 
remote: ###### WARNING:
remote:        You have not declared a Ruby version in your Gemfile.
remote:        To set your Ruby version add this line to your Gemfile:
remote:        ruby '2.0.0'
remote:        # See https://devcenter.heroku.com/articles/ruby-versions for more information.
remote: 
remote: ###### WARNING:
remote:        No Procfile detected, using the default web server (webrick)
remote:        https://devcenter.heroku.com/articles/ruby-default-web-server
remote: 
remote: Using release configuration from last framework (Ruby).
remote: -----> Discovering process types
remote:        Procfile declares types     -> (none)
remote:        Default types for Multipack -> console, rake
remote: 
remote: -----> Compressing... done, 31.2MB
remote: -----> Launching... done, v5
remote:        https://fathomless-peak-4331.herokuapp.com/ deployed to Heroku
remote: 
remote: Verifying deploy... done.
To https://git.heroku.com/fathomless-peak-4331.git
 * [new branch]      master -> master
```

And here it is on the dyno:

```
$ heroku run bash
Running `bash` attached to terminal... up, run.1446
~ $ irb
irb(main):001:0> require 'rugged'
=> true
irb(main):002:0> Rugged::Version
=> "0.21.4"
```
