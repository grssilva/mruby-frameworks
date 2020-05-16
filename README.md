# MRuby iOS, tvOS and macOs Catalyst xcframework

Based on [ruby2d/mruby-frameworks](https://github.com/ruby2d/mruby-frameworks)

Run `rake` to cross compile and build the xcframework.
To update the MRuby submodule, use `rake mruby_latest` to set to the latest release and `rake mruby_master` to set the master branch.

The prebuilt xcframework is located in `xcframework/`.

## How to add the XCFramework to your project:
1. On project settings ->`Build Settings` -> `Other Code Signing Flags`, add `--deep`
2. On project settings -> `Signing & Capabilities` -> `Hardened Runtime`, check the `Disable Library Validation` option
3. Copy `MRuby.xcframework` to a folder in your project (usually a folder named `Frameworks` where your xcodeproj is)
4. On target settings -> `Frameworks, Libraries, and Embedded Content`, add `MRuby.xcframework`

## How to test in 5 min or less:
1. Create an new iOs Objective-C project
2. On `ViewController.m`, add:
```
#include <mruby.h>
#include <mruby/compile.h>
```
3. On `- (void)viewDidLoad)` of that class, add:
```
mrb_state *mrb = mrb_open();
char code[] = "5.times { puts 'mruby is awesome!' }";

printf("Executing Ruby code with mruby:\n");
mrb_load_string(mrb, code);

mrb_close(mrb);
```
4. Run and you should see 'mruby is awesome!' 5 times in the Output window.
