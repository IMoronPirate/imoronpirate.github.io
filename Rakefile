SITE_DIR = "_site"


desc "Build Jekyll site, copy files to master and commit/push to github"

task :build, :message do |t, args|
  raise "Missing \"message\" argument for commit. Build with `rake build[\"message\"]`".red unless args.message

  build_jekyll

  # checkout master, copy files and commit
  system "git checkout master" or fail "## [FAILED] master checkout".red
  puts "## [SUCCESS] Master checked out".green

#  system "rm -r *"
  system "cp -r #{SITE_DIR}/* ."
  system "rm -r #{SITE_DIR}"
  system "git add -A" # commit all changes, removed and new files
  system "git commit -m \"#{args.message}\"" or fail "## [FAILED] commit to master ".red
  puts "## [SUCCESS] webpage committed".green

  system "git push" or fail "## [FAILED] can't push".red
  puts "## [SUCCESS] push done. Webpage is alive".green
end


def build_jekyll
  puts "## Building jekyll"
  system "jekyll build" or fail "## [FAILED] Jekyll build".red
  puts "## [SUCCESS] Jekyll Build".green
end


class String
  # colorization
  def colorize(color_code)
    "\e[#{color_code}m#{self}\e[0m"
  end

  def red
    colorize(31)
  end

  def green
    colorize(32)
  end

  def yellow
    colorize(33)
  end

  def blue
    colorize(34)
  end

  def pink
    colorize(35)
  end

  def light_blue
    colorize(36)
  end
end

