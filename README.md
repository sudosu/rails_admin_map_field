Rails Admin Map Field
=====================

rails_admin_map_field is a gem that works with sferik's **[rails_admin](https://github.com/sferik/rails_admin)** gem to provide an easy-to-use Google Maps interface for displaying and setting geographic co-ordinates in a model.

Where a ``latitude`` and ``longitude`` are set on the model, this location is represented by a marker shown on a Google map centered at the marker. The administrator also has the option of adding street ``address``, ``city``, and ``state`` fields.  As these fields are filled in, the Maps API is used to geocode the address in order to determine the latitude and longitude of the map marker, which is updated on the fly.

New Features
------------

- map resizing in config
- map marker draggable
- custom label for latitude field
- adds ``:latitude``, ``:longitude`` text fields below map which update dynamically as the map marker is dragged


Usage
-----

rails_admin_map_field expects that the model will have two attributes, one for latitude and one for longitude of the point represented. To enable rails_admin_map_field, add the following to your `Gemfile`:

```ruby
gem "rails_admin_map_field", :github => "sudosu/rails_admin_map_field"
```

Then, add in your `config/initializers/rails_admin.rb` initializer:

```ruby
RailsAdmin.config do |config|
  config.model User do
    configure :latitude, :map
    configure(:longitude) { visible false }
  end
end
```

**Note**: The field which is set as a map-type field must be the latitude field, not the longitude. By default, rails_admin_map_field will guess that the longitude field is called "longitude".

Configuration
=============

For different configurations, rails_admin_map_field can be configured with the following:

- `longitude_field` - the name of the longitude field that forms the the co-ordinate with the latitude field specified. Defaults to "longitude"
- `address_field` - the name of the address field. Defaults to "address"
- `city_field` - the name of the city field. Defaults to "city"
- `state_field` - the name of the state field. Defaults to "state"
- `google_api_key` - if you use a Google Maps API Key, it can be specified here.
- `default_latitude` - the latitude to center the map shown on if the latitude field is blank. Defaults to 40.711417, the latitude of New Jersey City, NJ, USA
- `default_longitude` - the longitude used if the longitude field is blank. Defaults to 74.0647, the longitude of New Jersey City, NJ, USA.
- `map_width` - map width in pixels, e.g., '400'
- `map_height` - map height in pixels
- `map_label` - label for map field. Defaults to "Map"


A more complicated configuration example:

```ruby
RailsAdmin.config do |config|
  config.model Point do
    configure :lat, :map do
      longitude_field :lon
      google_api_key "a1b2c3d4e5f6deadbeef"
      default_latitude -34.0  # Sydney, Australia
      default_longitude 151.0
    end
  end
end
```

LICENSE
=======
rails_admin_map_field is licensed under the MIT license.

Copyright (C) 2011 by Jason Langenauer, Jules Laplace, Valentin
Ballestrino, Bartlomiej Skwira, Oleg Popadyuk

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
