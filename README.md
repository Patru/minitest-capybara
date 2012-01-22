# minitest-matchers-capybara

Capybara matchers support for minitest unit & spec

## Why?

Capybara has good support for RSpec. If you want to use it with minitest,
you can of course write:

    assert page.has_content?("Hello")

but:
1) it's kinda ugly
2) you don't have meaningfull error messages.

With this project minitest gets all the good stuff.

## Usage

Add to Gemfile:

    # Gemfile
    group :test do
      gem "minitest-matchers-capybara"
    end

Next, I like to create seperate test class for acceptance tests.
Note, Rails 4.0 will support minitest/spec out of the box, so you would just
subclass `ActiveSupport::TestCase` instead of `MiniTest::Spec.`

    # test/test_helper.rb
    require "capybara/rails"

    class AcceptanceTest < MiniTest::Spec
      include Capybara::RSpecMatchers
      include Capybara::DSL
    end

Finally, you can use it like this:

    # test/acceptance/home_test.rb
    require "test/test_helper.rb"

    class HomeTest < AcceptanceTest
      it "home test" do
        visit "/"
        must_have_content "Homepage"
      end
    end

## License

(The MIT License)

Copyright (c) Wojciech Mach

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.