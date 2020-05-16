mruby_version = '2.1.0'

task default: 'mruby_xcframework'

desc 'Clean the project build files'
task :clean do
  FileUtils.remove_dir 'ios/MRuby.framework', true
  FileUtils.remove_dir 'tvos/MRuby.framework', true
  FileUtils.remove_dir 'macosx/MRuby.framework', true
  FileUtils.remove_dir 'xcframework/MRuby.xcframework', true
  FileUtils.remove_dir 'mruby/build', true
end

desc 'Build MRuby for iOS and tvOS'
task :build_mruby => :clean do
  Dir.chdir('mruby') do
    ENV['MRUBY_CONFIG'] = '../build_config.rb'
    system 'rake'

    # Dir.chdir('build') do
    #   FileUtils.mkdir_p 'ios-universal/lib'
    #   `lipo ios/lib/libmruby.a ios-simulator/lib/libmruby.a -create -output ios-universal/lib/libmruby.a`
    #
    #   FileUtils.mkdir_p 'tvos-universal/lib'
    #   `lipo tvos/lib/libmruby.a tvos-simulator/lib/libmruby.a -create -output tvos-universal/lib/libmruby.a`
    # end
  end

  FileUtils.mkdir_p 'ios/MRuby.framework/Headers'
  FileUtils.cp_r 'mruby/include/.', 'ios/MRuby.framework/Headers'
  FileUtils.cp 'Info.plist', 'ios/MRuby.framework'
  FileUtils.cp 'mruby/build/ios-universal/lib/libmruby.a', 'ios/MRuby.framework/MRuby'

  FileUtils.mkdir_p 'macosx/MRuby.framework/Headers'
  FileUtils.cp_r 'mruby/include/.', 'macosx/MRuby.framework/Headers'
  FileUtils.cp 'Info.plist', 'macosx/MRuby.framework'
  FileUtils.cp 'mruby/build/macosx/lib/libmruby.a', 'macosx/MRuby.framework/MRuby'

  FileUtils.mkdir_p 'tvos/MRuby.framework/Headers'
  FileUtils.cp_r 'mruby/include/.', 'tvos/MRuby.framework/Headers'
  FileUtils.cp 'Info.plist', 'tvos/MRuby.framework'
  FileUtils.cp 'mruby/build/tvos-universal/lib/libmruby.a', 'tvos/MRuby.framework/MRuby'
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

desc 'Create XCFramework'
task :mruby_xcframework => :build_mruby do
  FileUtils.remove_dir 'xcframework'
  FileUtils.mkdir_p 'xcframework'

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
