# encoding: utf-8

require 'rubygems'
require 'bundler'
begin
  Bundler.setup(:default, :development)
rescue Bundler::BundlerError => e
  $stderr.puts e.message
  $stderr.puts "Run `bundle install` to install missing gems"
  exit e.status_code
end
require 'rake'

require 'jeweler'
Jeweler::Tasks.new do |gem|
  # gem is a Gem::Specification... see http://docs.rubygems.org/read/chapter/20 for more options
  gem.name = "swot"
  gem.homepage = "http://github.com/leereilly/swot"
  gem.license = "MIT"
  gem.summary = %Q{email helpers}
  gem.description = %Q{email helpers}
  gem.email = "lee@leereilly.net"
  gem.authors = ["Lee Reilly"]
  # dependencies defined in Gemfile
end
Jeweler::RubygemsDotOrgTasks.new

require 'rake/testtask'
Rake::TestTask.new(:test) do |test|
  test.libs << 'lib' << 'test'
  test.pattern = 'test/**/test_*.rb'
  test.verbose = true
end

task :default => :test

require 'rdoc/task'
Rake::RDocTask.new do |rdoc|
  version = File.exist?('VERSION') ? File.read('VERSION') : ""

  rdoc.rdoc_dir = 'rdoc'
  rdoc.title = "swot #{version}"
  rdoc.rdoc_files.include('README*')
  rdoc.rdoc_files.include('lib/**/*.rb')
end

task :add, :sld, :tld, :name do |t, args|
  file_path = "#{File.expand_path(__FILE__+'/..')}/lib/domains/#{args.tld}/#{args.sld}"
  if File.exists?(file_path)
    puts "already exists"
  elsif
    begin
      FileUtils.mkdir_p(File.dirname(file_path))
      File.open( file_path, "w" ) do |contents|
        contents.print args.name
      end
      `git add #{file_path}`
      `git commit -m "Add #{args.name}"`
      puts "commit successful"
    rescue
      puts "commit failed"
    end
  end
end  