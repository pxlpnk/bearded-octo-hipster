require 'bundler/setup'
require 'fire/forget'
require 'uri'

url = "http://an-ti.eu/"
task :default => 'stressi:test'

namespace :stressi do
  desc "Run test"
  task :test do
    (0..100).each do |n|
      puts "requests sent: #{n}" if (n%10 == 0)
      FAF.get url
    end
  end
end
