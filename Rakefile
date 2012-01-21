# Rakefile

require 'time'

deploy_default = "heroku"
deploy_branch = "master"
deploy_dir = "_heroku"
public_dir = '_site'
jekyll_path = '~/Workspace/jekyll/bin/jekyll'
app_name = 'gentle-galaxy-3818.heroku.com'

desc "deploy basic rack app to heroku"
multitask :heroku do
  puts "## Deploying to Heroku "
  (Dir["#{deploy_dir}/public/*"]).each { |f| rm_rf(f) }
  system "cp -R #{public_dir}/* #{deploy_dir}/public"
  puts "\n## copying #{public_dir} to #{deploy_dir}/public"
  cd "#{deploy_dir}" do
    system "git add ."
    system "git add -u"
    puts "\n## Committing: Site updated at #{Time.now.utc}"
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m '#{message}'"
    puts "\n## Pushing generated #{deploy_dir} website"
    system "git push heroku #{deploy_branch}"
    puts "\n## Heroku deploy complete"
  end
end

desc 'Generate Layout'
task :new_post do
  t = Time.now
  d = '_posts/' + t.strftime('%Y-%m-%d') + '.md'
  l = t.strftime('%d %B %Y')
  puts 'Generating new post'
  layout = <<DOC
---
layout: post
title: Title
---

{{ page.title }}
================

DOC
  layout += "\n <p class='meta'>" + l + "</p>\n"
  File.open(d, 'w') do |f|
    f.puts layout
  end
  puts 'Created: ' + d
end

task :launch do
  system 'open http://' + app_name
end

task :jekyll do
  system jekyll_path + ' --auto --server'
end
