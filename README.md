# calabash parallel execution

## Watch a quick demo here:

https://www.youtube.com/watch?v=sK3s0txeJvc


Run calabash-android tests in parallel on multiple connected devices. This is inspired by parallel_tests  https://rubygems.org/gems/parallel_tests

eg. bundle exec parallel_calabash -a my.apk -o'--format pretty' features/ --serialize-stdout

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'parallel_calabash'
```

And then execute:

    $ bundle install

Or install it yourself as:

    $ gem install parallel_calabash

## Usage

Usage: parallel_calabash [options]

Example: parallel_calabash -a my.apk -o 'cucumber_opts_like_tags_profile_etc_here' features/


    -h, --help                       Show this message
    -v, --version                    Show version
    -a, --apk apk_path               apk file path
    -o, --cucumber_opts '[OPTIONS]'  execute with those cucumber options
    -f, --filter                     Filter devices to run tests against using partial device id or model name matching. Multiple filters separated by ','
    --serialize-stdout               Serialize stdout output, nothing will be written until everything is done
    --group-by-scenarios             Distribute equally as per scenarios. This uses cucumber dry run
    --concurrent                     Run tests concurrently. Each test will run once on each device.


## FILTERING
Filters are partial matches on the device id, or model name.
> adb devices -l
List of devices attached
4100142545f271b5       device usb:14200000 product:sltexx model:SM_G850F device:slte
4366432135f271c6       device usb:14200000 product:sltexx model:SM_G9901 device:slte
emulator-5554          device product:sdk_phone_x86_64 model:Android_SDK_built_for_x86_64 device:generic_x86_64

To run against just the emulator: -f emulator
To run against a device id list: -f 4100142545f271b5,4366432135f271c6

## REPROTING

use ENV['TEST_PROCESS_NUMBER'] environment variable in your ruby scripts to find out the process number. you can use this for reporting purpose OR process specific action.

To get device model info, use ENV['DEVICE_INFO'] env variable.

eg. modify default profile in cucumber.yml as below to get different report from different process

default: --format html --out reports/Report_<%=ENV['DEVICE_INFO']%>_<%= ENV['TEST_PROCESS_NUMBER']%>.html --format pretty

## Contributing

1. Fork it ( https://github.com/[my-github-username]/parallel_calabash/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
