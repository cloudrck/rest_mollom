# RestMollom

A Ruby wrapper for Mollom Rest API

## Installation

Add this line to your application's Gemfile:

    gem 'rest_mollom'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install rest_mollom


## Usage

After you have requested a public/private key-pair from Mollom (on http://www.mollom.com), you can start using this class.

    require 'rubygems'
    require 'rest_mollom'
  
    m = RMollom.new(:private_key => 'your-private-key', :public_key => 'your-public-key')

    content = m.check_content(:post_title => 'Mollem is an open API', 
							:post_body => "Lorem Ipsum dolor...",
							:author_name => 'Jan De Poorter',
							:author_url => 'http://workswithruby.com')
    if content.spam?
    	puts "You, sir, are a spammer.. Goodbye!"
     elsif content.unsure?
       # possible spam, possible ham, show CAPTCHA
       puts "CAPTCHA: " + m.image_captcha(:session_id => content.session_id)["url"]
    
      captcha_correct = m.check_captcha(:session_id => content.session_id, :solution => STDIN.gets.chomp)
    else
      puts "The post is perfect! No spam!"
    end

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
