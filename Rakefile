require "bundler"
Bundler.setup

require "json"
require "rom/sql/rake_task"
require "rspec/core/rake_task"
require_relative "core/trug/container"

RSpec::Core::RakeTask.new(:spec)

namespace :db do
  task :setup do
    Trug::Container.boot!(:rom)
  end
end

desc "Fetch video thumb url"
task :fetch_vimeo_thumb_url, [:video_id] do |t, args|
  if args[:video_id]
    uri = URI("http://vimeo.com/api/v2/video/#{args[:video_id]}.json")
    response = Net::HTTP.get_response(uri)
    if response.is_a?(Net::HTTPSuccess)
      puts JSON.parse(response.body).first["thumbnail_large"] 
    else
      puts "Something went wrong:\n #{response.inspect}"
    end
  else
    puts "Video id is empty"
  end
end
