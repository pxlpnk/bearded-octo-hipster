require 'bundler/setup'
require 'fire/forget'
require 'uri'

url =  ENV['url']
requests = ENV['requests'] || 100
requests = requests.to_i

task :default => 'stressi:test'
namespace :stressi do
  desc "Run test"
  task :test do
    (0..requests).each do |n|
      puts "requests sent: #{n}" if (n%10 == 0)
      FAF.get url
    end
  end
end
