value-object
============
[![Build Status](https://travis-ci.org/noflopsquad/valueobjects.svg?branch=master)](https://travis-ci.org/noflopsquad/valueobjects)
[![Code Climate](https://codeclimate.com/github/noflopsquad/valueobjects/badges/gpa.svg)](https://codeclimate.com/github/noflopsquad/valueobjects)
[![Test Coverage](https://codeclimate.com/github/noflopsquad/valueobjects/badges/coverage.svg)](https://codeclimate.com/github/noflopsquad/valueobjects/coverage)

A simple module to provide value objects semantics to a class.


## Usage

### Fields

```ruby
require 'value_object'

class Point
  extend ValueObject
  fields :x, :y
end

point = Point.new(1, 2)
=> #<Point:0x00000001d1a780 @x=1, @y=2>

point.x
=> 1

point.y
=> 2

point.x = 3
NoMethodError: undefined method `x=' for #<Point:0x00000001d1a780 @x=1, @y=2>

```

### Invariants

You can declare invariants to restrict field values on initialization

```ruby
require 'value-object'

class Point
  extend ValueObject
  fields :x, :y
  invariants :x_less_than_y, :inside_first_quadrant

  private
  def inside_first_quadrant
    x > 0 && y > 0
  end

  def x_less_than_y
    x < y
  end
end

point = Point.new(-5, 3)
ValueObject::ViolatedInvariant: Fields values [-5, 3] violate invariant: inside_first_cuadrant

Point.new(6, 3)
ValueObject::ViolatedInvariant: Fields values [6, 3] violate invariant: x_less_than_y

```


