---
title: Rails 5 - Send Mail to Local Directory
layout: post
categories: [rails, programming]
---

Add the following lines to application.rb (Rails 5):

```ruby
config.action_mailer.delivery_method = :file
config.action_mailer.file_settings = { :location => Rails.root.join('tmp/mail') }
```

This will send the mail to a folder at the top level of the project called ‘tmp’.
