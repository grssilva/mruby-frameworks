# MRuby iOS, tvOS and macOs Catalyst xcframework

Based on [ruby2d/mruby-frameworks](https://github.com/ruby2d/mruby-frameworks)

Run `rake` to cross compile and build the xcframework.
To update the MRuby submodule, use `rake mruby_latest` to set to the latest release and `rake mruby_master` to set the master branch.

The prebuilt xcframework is located in `xcframework/`.

How to generate:
1. run `rake mruby_latest` on folder to update MRuby
2. run `rake` to generate the xcframework
3. on `Build Settings`, on `Other Code Signing Flags`, add `--deep`
4. on the project `Signing & Capabilities`, on `Hardened Runtime`, check `Disable Library Validation`
5. copy the `MRuby.xcframework` to a folder in your project.
6. add the `MRuby.xcframework`  to your xcode project on the `Frameworks, Libraries, and Embedded Content`.

Easy way to test:
Create an Objective-C project
In the class you want to test, add the includes:
```
#include <mruby.h>
#include <mruby/compile.h>
```
Then, where you want the code to run (like the viewDidLoad):
```
mrb_state *mrb = mrb_open();
char code[] = "5.times { puts 'mruby is awesome!' }";

printf("Executing Ruby code with mruby:\n");
mrb_load_string(mrb, code);

mrb_close(mrb);
```
Run and you should see 'mruby is awesome!' 5 times in the Output window.
