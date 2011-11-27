# encoding: utf-8

require "#{File.dirname(__FILE__)}/lib/unicode_utils/version"

gem_filename = "unicode_utils-#{UnicodeUtils::VERSION}.gem"

task "default" => "quick-test"

desc "Run unit tests."
task "test" do
  sh "ruby -I lib -I . test/suite.rb"
end

desc "Quick test run."
task "quick-test" do
  sh "ruby -I lib -I . test/test_unicode_utils.rb"
end

desc "Build unicode_utils gem."
task "gem" do
  sh "gem build unicode_utils.gemspec"
  mkdir "pkg" unless File.directory? "pkg"
  mv gem_filename, "pkg"
end

desc "Run rdoc to generate html documentation."
task "doc" do
  sh "rdoc -o doc --charset=UTF-8 --title=UnicodeUtils --main=README.txt lib README.txt INSTALL.txt CHANGES.txt LICENSE.txt"
end

desc "Publish doc/ on unicode-utils.rubyfore.org. " +
     "Note: scp will prompt for rubyforge password."
task "publish-doc" => "doc" do
    sh "scp -r doc/* langi@rubyforge.org:/var/www/gforge-projects/unicode-utils/"
end

desc "Compile Unicode data files from data/ to cdata/."
task "compile-data" do
  sh "ruby data/compile.rb"
end

desc "Remove generated packages and documentation."
task "clean" do
  rm_r "pkg" if File.exist? "pkg"
  rm_r "doc" if File.exist? "doc"
end
