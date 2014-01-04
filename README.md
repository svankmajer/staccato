# Staccato

Ruby Google Analytics Measurement

[![Build Status](https://travis-ci.org/tpitale/staccato.png?branch=master)](https://travis-ci.org/tpitale/staccato)
[![Code Climate](https://codeclimate.com/github/tpitale/staccato.png)](https://codeclimate.com/github/tpitale/staccato)

## Installation

Add this line to your application's Gemfile:

    gem 'staccato'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install staccato

## Usage ##

    tracker = Staccato.tracker('UA-XXXX-Y') # REQUIRED, your Google Analytics Tracking ID

`#tracker` optionally takes a second param for the `client_id` value
By default, the `client_id` is set to a random UUID with `SecureRandom.uuid`

### Track some data ###

    # Track a Pageview (all values optional)
    tracker.pageview(path: '/page-path', hostname: 'mysite.com', title: 'A Page!')

    # Track an Event (all values optional)
    tracker.event(category: 'video', action: 'play', label: 'cars', value: 1)

    # Track social activity (all values REQUIRED)
    tracker.social(action: 'like', network: 'facebook', target: '/something')

    # Track exceptions (all values optional)
    tracker.exception(description: 'RuntimeException', fatal: true)

    # Track timing (all values optional, but should include time)
    tracker.timing(category: 'runtime', variable: 'db', label: 'query', time: 50) # time in milliseconds

    tracker.timing(category: 'runtime', variable: 'db', label: 'query') do
      some_code_here
    end

    # Track transaction (transaction_id REQUIRED)
    tracker.transaction({
      transaction_id: 12345,
      affiliation: 'clothing',
      revenue: 17.98,
      shipping: 2.00,
      tax: 2.50,
      currency: 'EUR'
    })

    # Track transaction item (matching transaction_id and item name REQUIRED)
    tracker.transaction_item({
      transaction_id: 12345,
      name: 'Shirt',
      price: 8.99,
      quantity: 2,
      code: 'afhcka1230',
      variation: 'red',
      currency: 'EUR'
    })

### "Global" Options ###

    # Track a Non-Interactive Event
    tracker.event(category: 'video', action: 'play', non_interactive: true)

Non-Interactive events are useful for tracking things like emails sent, or other
events that are not directly the result of a user's interaction.

The option `non_interactive` is accepted for all methods on `tracker`.

## Google Documentation

https://developers.google.com/analytics/devguides/collection/protocol/v1/devguide
https://developers.google.com/analytics/devguides/collection/protocol/v1/reference
https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
