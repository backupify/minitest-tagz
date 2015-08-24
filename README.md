# Minitest::Tagz

[![Build Status](https://travis-ci.org/backupify/minitest-tagz.svg)](https://travis-ci.org/backupify/minitest-tagz)
[![Code Climate](https://codeclimate.com/github/backupify/minitest-tagz/badges/gpa.svg)](https://codeclimate.com/github/backupify/minitest-tagz)
[![Gem Version](https://badge.fury.io/rb/minitest-tagz.svg)](http://badge.fury.io/rb/minitest-tagz)

yet another tags implementation for Minitest

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'minitest-tagz'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install minitest-tagz

## Setup

In your `test_helper.rb` you'll need to require `Minitest::Tagz`. You'll also
want to tell `Tagz` which tags you want to use. I suggest using the `TAGS` environment
variable:

```rb
require 'minitest/tagz'
Minitest::Tagz.choose_tags(*ENV['TAGS'].split(',')) if ENV['TAGS']
```

This wil let you do this like: `bundle exec rake test TAGS=fast,login` to run all
tests with the fast and login tags.

## Usage

`Minitest::Tagz` works with both `Minitest::Test` and `Minitest::Spec`. You can declare
tags by using the `tag` helper.

```rb
# Using Minitest::Spec
class MySpec < Minitest::Spec
  tag :fast, :unit
  it 'should run' do
    assert true
  end

  tag :fast
  it 'should not run' do
    refute true
  end

  it 'also should not run' do
    refute true
  end
end

# Using Minitest::Test
class MyTest < Minitest::Test
  tag :fast
  def test_my_stuff
    assert true
  end
end
```

With `Minitest::Spec` adding tags to a `describe` will add the tags to all of the
tests in the block:

```rb
class MySpec < Minitest::Spec
  tag :login
  describe 'all tests in this are tagged with :login' do
    it 'tests this' do
      assert true
    end

    it 'also tests this' do
      assert true
    end
  end
end
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release` to create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

1. Fork it ( https://github.com/backupify/minitest-tagz/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
