# ActiveRecord

## Model Definition Order

```ruby
class Model

  # Module inclusions
  extend  Module
  include Module

  # Subclasses
  class Error < StandardError
  end

  # Constants
  CONSTANTS = nil

  # Relationships
  belongs_to  :model
  has_one     :model
  has_many    :models

  # Attribute definition, visibility
  attr_reader     :attribute
  attr_accessor   :attribute
  attr_accessible :attribute
  attr_protected  :attribute

  # Extensions
  acts_as_list  :scope => :keyword

  # Before/After filters
  before_save   :method
  before_create :method
  before_update :method
  after_update  :method

  # Validations
  validates_presence_of :attribute

  # Named scopes
  named_scope   :one, lambda { }
  named_scope   :two, :conditions => ""


  private

end
```
