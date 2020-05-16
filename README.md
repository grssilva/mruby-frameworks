# MRuby iOS, tvOS and macOs Catalyst xcframework

Based on [ruby2d/mruby-frameworks](https://github.com/ruby2d/mruby-frameworks)

Run `rake` to cross compile and build the xcframework.
To update the MRuby submodule, use `rake mruby_latest` to set to the latest release and `rake mruby_master` to set the master branch.

The prebuilt xcframework is located in `xcframework/`.

## How to add to your project:
1. on `Build Settings`, on `Other Code Signing Flags`, add `--deep`
2. on the project `Signing & Capabilities`, on `Hardened Runtime`, check `Disable Library Validation`
3. copy the `MRuby.xcframework` to a folder in your project (i recommend a folder named `Frameworks` where your xcproject is).
4. add the `MRuby.xcframework`  to your xcode project on the `Frameworks, Libraries, and Embedded Content`.

## Easy way to test:
1. Create an Objective-C project
2. In the class you want to test (ex. `ViewController.m`), add the includes:
```
#include <mruby.h>
#include <mruby/compile.h>
```
3. Where you want the code to run (ex. `- (void)viewDidLoad):
```
mrb_state *mrb = mrb_open();
char code[] = "5.times { puts 'mruby is awesome!' }";

printf("Executing Ruby code with mruby:\n");
mrb_load_string(mrb, code);

mrb_close(mrb);
```
4. Run and you should see 'mruby is awesome!' 5 times in the Output window.
