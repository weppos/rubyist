---
title: Models
---

# Models


## Model Definition Order

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
      validates :attribute, :presence => true

      # Named scopes
      named_scope   :one, lambda { }
      named_scope   :two, :conditions => ""

      # Business Logic
      def public_method_a
      end

      protected

        def protected_method
        end

      private

        def private_method
        end

    end
