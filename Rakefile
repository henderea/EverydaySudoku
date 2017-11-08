# -*- coding: utf-8 -*-
$:.unshift('/Library/RubyMotion/lib')
require 'motion/project/template/ios'

begin
  require 'bundler'
  Bundler.require
rescue LoadError
# ignored
end

require 'rubygems'
require 'motion-yaml'

Motion::Project::App.setup do |app|
  # Use `rake config' to see complete project settings.
  app.name = 'EverydaySudoku'
end

task :build_puzzles do
  COUNT_EACH = 200

  if Dir.exist?('resources/puzzles')
    Dir.foreach('resources/puzzles') { |file| File.delete("resources/puzzles/#{file}") unless file.start_with?('.') }
  else
    Dir.mkdir('resources/puzzles')
  end

  require_relative 'app/lib/sudoku'
  require 'yaml'

  sudoku = Sudoku.new

  [:easy, :medium, :hard].each { |diff|
    (1..COUNT_EACH).each { |i|
      print "\r#{diff.to_s} #{i}"
      file_name = "resources/puzzles/#{diff.to_s}-#{i}.yaml"
      sudoku.generate_difficulty(diff)
      IO.write(file_name, sudoku.to_hash.to_yaml)
    }
  }
end