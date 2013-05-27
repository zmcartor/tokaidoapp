directory "tmp/zips"

namespace :bootstrap do
  task :update => "tmp/zips" do
    if File.exist?("tmp/zips/Bootstrap")
      cd "tmp/zips/Bootstrap" do
        sh "git pull"
      end
    else
      sh "git clone https://github.com/tokaido/tokaido-bootstrap.git tmp/zips/Bootstrap"
    end

    cd "tmp/zips/Bootstrap" do
      sh "bundle --standalone --without development"
    end
  end

  task :zip => :update do
    require "zip/zip"

    rm "tmp/zips/tokaido-bootstrap.zip"

    directory = "tmp/zips/Bootstrap/"
    zipfile_name = "tmp/zips/tokaido-bootstrap.zip"

    Zip::ZipFile.open(zipfile_name, Zip::ZipFile::CREATE) do |zipfile|
      Dir[File.join(directory, '**', '**')].each do |file|
        zipfile.add("Bootstrap/" + file.sub(directory, ''), file)
      end
    end
  end

  task :copy => :zip do
    cp "tmp/zips/tokaido-bootstrap.zip", "Tokaido/tokaido-bootstrap.zip"
  end
end

