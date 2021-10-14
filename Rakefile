# frozen_string_literal: true

@youtube_playlist_url = ''
@box_path = './downloads'

namespace :youtube do
    desc 'Downloads the latest YouTube videos'
    task :download do
        command = "youtube-dlc --ignore-errors --format bestaudio --extract-audio --audio-format mp3 --audio-quality 160K -o '#{@box_path}/%(title)s.%(ext)s' --yes-playlist #{@youtube_playlist_url}"
        system(command)
    end
end

namespace :convert do
    desc 'Convert all the files in the current directory'
    task :all do
        Dir.glob("#{@box_path}/**/*.{webm,mkv,flv,ogg,ogv,avi,mov,wmv,mp4,mpg,m4v}").each do |file|
            convert_file(file)
        end
    end

    desc 'Convert a single file'
    task :file do
        convert_file(ARGV[0])
    end

    def convert_file(file)
        puts "Converting #{file}"
        name = File.basename(file, '.*')
        system("ffmpeg -i #{file} -b:a -vn #{name}.mp3")
    end
end
