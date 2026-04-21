---
title: Rails 5 - Set Defaults for date_select Date Formats
layout: post
categories: [rails, programming]
---
Scenario: You’re using a date_select form helper and the parts of the date are displaying in YYYY/MM/DD format.

Fix: You can add this to your en.yml file to set a default that Rails will pick up for any date_select elements that you use across the app. I assume it also affects other date specific controls too, drop me a comment if you come across any.

```yaml
en:
  date:
    order:
      - :day
      - :month
      - :year
```

To override formats for specific date_select elements we can use the order property of the form helper:

```ruby
<%= f.date_select :transaction_date, order: [:day, :month, :year] %>
```

or

```ruby
<% date_select :transaction, :transaction_date, order: [:day, :month, :year] %>
```
