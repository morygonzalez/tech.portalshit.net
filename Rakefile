desc "Given a title as an argument, create a new post file"
task :write, [:title, :category] do |t, args|
  filename = "#{Time.now.strftime('%Y-%m-%d')}-#{args.title.gsub(/\s/, '_').downcase}.markdown"
  path = File.join("_posts", filename)
  if File.exist? path; raise RuntimeError.new("Won't clobber #{path}"); end
  File.open(path, 'w') do |file|
    file.write <<-EOS
---
layout: post
category: #{args.category}
title: #{args.title}
date: #{Time.now.strftime('%Y-%m-%d %k:%M:%S')}
---
EOS
  end
  puts "Now open #{path} in an editor."
end

desc "Publish"
task :publish do
  path = File.expand_path("_site")
  if system("rsync -avz --delete #{path}/ morygonzalez@portalshit.net:sites/tech.portalshit.net/_site/")
    puts "Your blog was successfully published!"
  else
    puts "Something went wrong..."
  end
end
