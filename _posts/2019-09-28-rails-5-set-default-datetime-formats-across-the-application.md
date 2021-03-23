---
title: Rails 5 - Set Default DateTime Formats Across the Application
layout: post
categories: [rails, programming]
---
Scenario: You have a preferred default time format you want to use in your app and you need a way to capture this.

Fix: Add the format you want to use to the config/locales/en.yml file

```yaml
time:
  formats:
    default: '%d/%m/%Y'
```

Now you can use the l helper method in your views or wherever you like (prefix with i18n module where you need to) and it will pick up this format.

```ruby
<%= l(@transaction.transaction_date) %>
```
You can also specify a named format to use where you like too:

```yaml
time:
  formats:
    fun: '%d-%m-%Y'
```

Then we can use it like so:

```ruby
<%= l(@transaction.transaction_date), format: :fun %>
```
