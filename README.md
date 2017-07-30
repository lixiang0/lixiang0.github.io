
## my blog


# how to install
In command line:
```
sudo apt-get update
sudo apt-get install ruby ruby-dev make gcc
sudo gem install jekyll bundler
sudo ufw status
sudo ufw allow 4000
sudo apt-add-repository ppa:brightbox/ruby-ng
sudo apt-get update
sudo apt-get install ruby2.3 ruby2.3-dev
sudo gem install posix-spawn
cd ~
sudo jekyll new blog
cd ~/blog
bundle install
vim Gemfile #delete 'x64_mingw' string
bundle exec jekyll serve
```
finally you can see:
```
Configuration file: /home/ruben/git/blog/_config.yml
            Source: /home/ruben/git/blog
       Destination: /home/ruben/git/blog/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 0.204 seconds.
 Auto-regeneration: enabled for '/home/ruben/git/blog'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.

```
# tip1
if occurs error:
```
/usr/lib/ruby/vendor_ruby/bundler/dsl.rb:227:in `block in _normalize_options': `x64_mingw` is not a valid platform
```
delete 'x64_mingw' in Gemfile.

