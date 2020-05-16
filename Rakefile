mruby_version = '2.1.0'

task default: 'mruby_xcframework'

desc 'Clean the project build files'
task :clean do
  FileUtils.remove_dir 'xcframework/MRuby.xcframework', true
  FileUtils.remove_dir 'mruby/build', true
end

desc 'Build MRuby for iOS, tvOS & macOs Catalyst'
task :build_mruby => :clean do
  Dir.chdir('mruby') do
    ENV['MRUBY_CONFIG'] = '../build_config.rb'
    system 'rake'
  end
end

desc 'Create XCFramework'
task :mruby_xcframework => :build_mruby do
  system 'xcodebuild -create-xcframework '\
  '-library mruby/build/ios/lib/libmruby.a '\
  '-headers mruby/include '\
  '-library mruby/build/ios-simulator/lib/libmruby.a '\
  '-headers mruby/include '\
  '-library mruby/build/macosx/lib/libmruby.a '\
  '-headers mruby/include '\
  '-library mruby/build/tvos/lib/libmruby.a '\
  '-headers mruby/include '\
  '-library mruby/build/tvos-simulator/lib/libmruby.a '\
  '-headers mruby/include '\
  '-output xcframework/MRuby.xcframework'
end

desc 'Set MRuby submodule to latest release'
task :mruby_latest do
  system 'git submodule update --remote && '\
         'cd mruby && '\
         "git checkout tags/#{mruby_version}"
end

desc 'Set MRuby submodule to master branch'
task :mruby_master do
  system 'git submodule update --remote && '\
         'cd mruby && '\
         'git checkout master && '\
         'git pull --rebase'
end
