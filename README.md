### hobbit
---
https://github.com/patriciomacadden/hobbit

```
gem 'hobbit'
bundle
gem install hobbit

rackup
```

```ruby
# app.rb
require 'hobbit'
class App < Hobbit::Base
  get '/' do
    'Hello World!'
  end
end

# config.ru
require './app'
run App.new

class App < Hobbit::Base
  get '/' do
  end
  post '/' do
  end
  put '/' do
  end
  patch '/' do
  end
  delete '/' do
  end
  options '/' do
  end
end

reuqire 'hobbit'
class App < Hobbit::Base
  get '/hi/:name' do
    "Hello #{request.params[:name]}"
  end
end

require 'hobbit'
class App < Hobbit::Base
  get '/' do
    response.redirect '/hi'
  end
  get '/hi' do
    'Hello!'
  end
end

require 'hobbit'
class App < Hobbit::Base
  use Rack::Session::Cookie, secret: SecretRandom.hex(64)
  def session
    env['rack.session']
  end
  get '/' do
    response.status = 401
    halt response.finish
  end
end

require 'hobbit'
class InnerApp < Hobbit::Base
  get do
    'Hello!'
  end
end
class App < Hobbit::Base
  map('/inner') { run InnerApp.new }
  get '/' do
    'Hello!'
  end
end

require 'hobbit'
class App < Hobbit::Base
  use Rack::Session::Cookie, secret: SecureRandom.hex(64)
  use Rack::ShowExceptions
  def session
    env['rack.session']
  end
  get '/' do
    session[:name] = 'hobbit'
  end
end
run App.new

require 'hobbit'
require 'rack/protection'
require 'securerandom'
class App < Hobbit::Base
  use Rack::Session::Cookie, secret: SecureRandom.hex(64)
  use Rack::Protection
  get '/' do
    'Hello'
  end
end

# app.rb
require 'hobbit'
class App < Hobbit::Base
  get '/' do
    'Hello'
  end
end

# app_sepc.rb
require 'minitest/autorun'
require 'app'
describe App do
  include Rack::Test::Methods
  def app
    App.new
  end
  describe 'GET /' do
    it 'must be ok' do
      get '/'
      last_response.must_be :ok?
      last_response.body.must_match /Hello!/
    end
  end
end

module MyExtension
  def do_something
  end
end
class App < Hobbit::Base
  include MyExtension
  get '/' do
    do_something
    'Hello!'
  end
end
```

```
```


