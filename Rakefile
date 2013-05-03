require 'bundler/setup'
require 'fire/forget'
require 'uri'
require 'logger'
log = Logger.new(STDOUT)
log.level = Logger::DEBUG


url =  ENV['url']
requests = ENV['requests'] || 100
requests = requests.to_i

task :default => 'stressi:test'
namespace :stressi do
  desc "Run test"
  task :test do
    (0..requests).each do |n|
      log.debug "Requests sent: #{n}" if (n%10 == 0)
      FAF.get url
    end

    log.debug "All #{requests} requests sent. No s$#t was given."

  end
end
