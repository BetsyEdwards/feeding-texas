require 'rubygems'
require 'rake'
require 'rdoc'
require 'date'
require 'yaml'
require 'tmpdir'
require 'jekyll'
require 's3_website'

task :default => :server

desc 'Build site with Jekyll'
task :build do
  system 'bundle exec compass compile'
  system 'bundle exec jekyll build'
end

desc 'Build and start local server'
task :serve do
  system 'bundle exec compass compile'
  system 'bundle exec jekyll serve -w --baseurl="" --drafts'
end

def jekyll(opts = '')
  system 'rm -rf _site'
  system 'jekyll ' + opts
end

# Amazon S3 publishing options
desc "Generate and publish site to feedingtexas.org on Amazon S3."
task :publish => [:build] do
  system 'bundle exec s3_website push'
end

desc "Generate and publish site to stage.feedingtexas.org on Amazon S3."
task :stage => [:build] do
  system 'bundle exec s3_website push --config-dir=stage_config'
end
