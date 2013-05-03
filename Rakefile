require 'bundler/setup'
require 'fire/forget'
require 'benchmark'
require 'logger'
require 'uri'

@log = Logger.new(STDOUT)
@log.level = Logger::DEBUG


url =  ENV['url']
threads_cnt = ENV['threads'] || 10
threads_cnt = threads_cnt.to_i

requests = ENV['requests'] || 100
requests = requests.to_i

def fire(url)
  timer = Benchmark.measure{ FAF.get url }
  request_length = timer.to_a.last
end

def fire_n_times(n_times, url)
  (0..n_times).each do |n|
    request_length = fire(url)
    @log.debug "Requests sent: #{n}, last one took #{request_length}" if (n%10 == 0)
  end
end

task :default => 'stressi:test'
namespace :stressi do
  desc "Run test"
  task :test do
    fire_n_times(requests, url)
    @log.debug "All #{requests} requests sent. No s$#t was given."
  end

  desc "parallel stressi"
  task :parallel do
    threads = []
    (0..threads_cnt).each do |t|
      threads << Thread.new {fire_n_times(requests, url)}
    end
    threads.map{|t| t.join }
    @log.debug "All #{requests} requests multiplied by #{threads_cnt} threads sent. No s$#t was given."
  end
end
