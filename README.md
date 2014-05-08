pagination_rails
================

You got a honking ActiveRecord result and want to let users page through the result? Read on.

Overview
The general gist looks like you need to first, set an optional configuration in the model to limit records returned per query, second adjust the controller or  scope in the model, to use the pagination, with the limit records config, third in the ERB, add the pagination control with <%= will_paginate %>

https://github.com/mislav/will_paginate

doc
https://github.com/mislav/will_paginate/wiki

css
http://mislav.uniqpath.com/will_paginate/


Gem file
```
## pagination
gem 'will_paginate', '~> 3.0'
```
be sure to run:
```
bundle install
```
Model
optional to add this( I put in Controller )
```
class Post < ActiveRecord::Base

  self.per_page = 20
```
Controller

# set per_page globally, or optionally in the ActiveRecord - see 2nd example below.
```
WillPaginate.per_page = 20

@posts = Post.paginate(:page => params[:page])
```
OR
```
@posts = Post.paginate(:page => params[:page], :per_page => 20)
```

Within ERB/View

To show the nice page count with links, put it after your loop through the model result.  I ended up removing the :page_links => false so I could see the page numbers for faster navigation.
```
<%= will_paginate @posts, :page_links => false %>
```
