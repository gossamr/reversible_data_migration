# Reversible Data Migration

Need to update a small amount of data in migration? But still want to make it reversable? Reversable Data Migration comes to the rescue.

## Example usage

```ruby
class RemoveStateFromProduct < ActiveRecord::Migration
  def self.up
    backup_data = []
    Product.all.each do |product|
      backup_data << {:id => product.id, :state => product.state}
    end
    backup backup_data
    remove_column :products, :state
  end
  def self.down
    add_column :products, :state, :string
    restore Product
  end
end
```
## Installing

    gem install reversible_data_migration

## Rails 2 & 3 supported