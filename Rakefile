require 'yaml'
require 'open3'

EDITOR = ENV.fetch('EDITOR', 'atom')

task :default => :help

task :help do
  puts "This is what you can do here:"
  system("rake -sT")
  puts "Ex. ['Day 12', 1996-04-21, MTC]"
end

desc "Add a new post"
task :new_post, [:title, :date, :place] do |t, args|

  title = args[:title]
  date = args[:date]
  place = args[:place]

  filename = make_filename(date,title,place)

  puts "Creating new post file #{filename}"

  open(filename, 'wb') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title} - #{place}\""
    post.puts "date: #{date}"
    post.puts "category: #{place.downcase}"
    post.puts "---"
    post.puts "# #{date}. #{title} - #{place}"
    post.puts ""
  end

  `atom #{filename}`
end

def make_filename(date, title, place)
  clean = clean_title(title)
  "_posts/#{date}-#{clean}-#{place}.md"
end

def clean_title(title)
  title.gsub(/&/,'and').gsub(/[,'":\-\.\?!\(\)\[\]]/,'').gsub(/[\W]/,'-').gsub(/-+$/,'')
end
