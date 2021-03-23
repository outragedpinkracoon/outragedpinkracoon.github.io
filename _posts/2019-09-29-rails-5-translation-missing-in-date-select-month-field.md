---
title: Rails 5 - Translation Missing in date_select Month Field
layout: post
categories: [rails, programming]
---
Scenario: You’ve used a date_select and everything was fine with the ‘en’ default locale. You’ve added a new locale like en-GB and now you see a strange thing in your dropdown:

![screenshot of missing translation message](/assets/images/rails-5-month-translation-missing/1.png)


Fix: We need to either manually populate the new translation file with the keys for month names like so

```yaml
en-GB:
  date:
    month_names: [January, Febuary, March, April, May, June, July, August, September, October, November, December]
    abbr_month_names: [Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec]
    day_names: [Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday]
```

OR add a fallback to application.rb where we use the a default translation if we are missing the keys in our custom file.

```ruby
config.i18n.fallbacks =[:en]
```
