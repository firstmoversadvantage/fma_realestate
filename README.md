# FmaRealestate

FMA Real Estate and CASS Ruby Client

## Installation

Add this line to your application's Gemfile:

    gem 'fma_realestate'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install fma_realestate

## Requirements

* Ruby 1.8.7 or above

## Usage

```ruby
# Global config
# if using rails, create initializer: /config/initializers/fma_realestate.rb
# Global config is optional
FmaRealestate.configure do |config|
  config.access_token  = 'your_access_token' # string
  config.raise_errors  = true_or_false       # boolean
  config.retries       = number_of_retries   # integer
  config.read_timeout  = number_of_seconds   # integer
  config.write_timeout = number_of_seconds   # integer
end

# or

FmaRealestate.access_token  = 'your_access_token'
FmaRealestate.raise_errors  = true_or_false
FmaRealestate.retries       = number_of_retries
FmaRealestate.read_timeout  = number_of_seconds
FmaRealestate.write_timeout = number_of_seconds
```

```ruby
# Sample client configuration, shown with default values:
# Client config is optional
config = {
  :access_token => FmaRealestate.access_token,  # initialize the client with an access token
  :raise_errors => false,                       # choose between returning false or raising a proper exception when API calls fails

  # Connection properties
  :retries       => 0,    # automatically retry a certain number of times before returning
  :read_timeout  => 10,   # set longer read_timeout, default is 10 seconds
  :write_timeout => 10,   # set longer write_timeout, default is 10 seconds
  :persistent    => false # when true, make multiple requests calls using a single persistent connection. Use +close_connection+ method on the client to manually clean up sockets
}
```

```ruby
# Example Cass client usage
client = Cass.new # using default config

# Cass#tiger
response_hash = client.tiger(
  :street_address => "123 N Easy St.", # optional
  :city           => "Boulder",        # optional
  :state          => "CO",             # optional
  :zip            => ""                # optional
)

# Cass#address
response_hash = client.address(
  :street_address => "123 N Easy St.", # optional
  :city           => "Boulder",        # optional
  :state          => "CO",             # optional
  :zip            => ""                # optional
)

# Cass#city_zip
response_hash = client.city_zip(
  :city           => "Boulder",        # optional
  :state          => "CO",             # optional
)

# Cass#city_county
response_hash = client.city_county(
  :zip            => "80302"           # optional
)

# Cass#state_county
response_hash = client.state_county(
  :state          => "CO",             # optional
)
```

```ruby
# Example PublicRecord client usage
client = PublicRecord.new # using default config

# PublicRecord#search_by_address
response_hash = client.search_by_address(
  :street_address => "123 N Easy St.", # optional
  :city           => "Boulder",        # optional
  :state          => "CO",             # optional
  :zip            => ""                # optional
)

# PublicRecord#search_by_advanced
response_hash = client.search_by_advanced(
  :legal_description => ""                # optional
  :owner_name        => "Jon Doe"         # optional
  :street_address    => "123 N Easy St.", # optional
  :city              => "Boulder",        # optional
  :state             => "CO",             # optional
  :zip               => "",               # optional
  :county            => "Boulder"         # optional
)

# PublicRecord#search_by_address_advanced
response_hash = client.search_by_address_advanced(
  :legal_description => ""                # optional
  :owner_name        => "Jon Doe"         # optional
  :street_address    => "123 N Easy St.", # optional
  :city              => "Boulder",        # optional
  :state             => "CO",             # optional
  :zip               => "",               # optional
  :county            => "Boulder"         # optional
)

# PublicRecord#search_by_global
response_hash = client.search_by_address_advanced(
  :q => "123 N Easy St." # required
)
```

```ruby
# Example PublicRecordSale client usage
client = PublicRecordSale.new # using default config

# PublicRecordSale#search_by_cass_search_key
response_hash = client.search_by_cass_search_key(
  :cass_search_key => "90803513805UNIT405", # optional
)
```

## FmaRealstate API Reference
Please refer to the <a href="http://realestate.firstmoversadvantage.com/api_documentation" target="_blank">official api documentation</a>

## Contributing

1. Fork it ( https://github.com/[my-github-username]/fma_realestate/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
