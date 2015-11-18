lass Repo < Thor
  REPO_PATH = '/home/git/repo'

  desc "list", "List all repository"
  def list
    `ls #{REPO_PATH}/`.chomp.split("\n").each do
      |repo| puts repo.sub(/\.git$/, "")
    end
  end

  desc "cydia", "cydia"
  def create(cydia)
    `sudo -u git git init --bare --shared #{REPO_PATH}/#{name}.git`
    if $?.success? then
      say("# Clone this repo", :yellow)
      say("git clone ssh://yann@ks355140.kimsufi.com/home/git/repo/#{name}.git")
      say("# Add a remote", :yellow)
      say("git remote add origin ssh://yann@ks355140.kimsufi.com/home/git/repo/#{name}.git")
    end
  end

  desc "delete NAME", "Delete repository NAME"
  method_option :force, :type => :boolean, :aliases => '-f', :default => false, :desc => "Do not ask for a confirmation"
  def delete(name)
    if options.force? || yes?("Really delete #{name} ? (y/N)", :yellow) then
      `sudo -u git rm -r #{REPO_PATH}/#{name}.git`
      if $?.success? then
        say("Repo #{name} successfully deleted", :green)
      else
        say("Unable to delete #{name} repository", :red)
      end
    end
  end
end
