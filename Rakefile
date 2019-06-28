# frozen_string_literal: true

require 'rake'
require 'rake/testtask'
require "rake/clean"
CLOBBER.include "pkg"

%w(smart_proxy_salt smart_proxy_salt_core).each do |plugin|
  namespace plugin do
    require 'bundler/gem_helper'
    Bundler::GemHelper.install_tasks(:name => plugin)
  end
end


desc 'Default: run unit tests.'
task :default => :test

desc 'Test Salt plugin'
Rake::TestTask.new(:test) do |t|
  t.libs << '.'
  t.libs << 'lib'
  t.libs << 'test'
  t.test_files = FileList['test/**/*_test.rb']
  t.verbose = true
end

require 'rubocop/rake_task'

desc 'Run RuboCop on the lib directory'
RuboCop::RakeTask.new(:rubocop) do |task|
  task.patterns = ['lib/**/*.rb', 'test/**/*.rb']
  task.fail_on_error = false
end
