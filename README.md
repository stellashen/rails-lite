# Rails Lite

In this project, we implement some of the basic functionality from
Rails.

## Phase I: Rack

Let's start out by building what happens when you run `rails server`.

Run the file with `bundle exec ruby bin/p01_basic_server.rb` (ensures you run with local gems), then in your browser navigate to `http://localhost:3000`. You should
see `Hello world!`. Congratulations, you've written a Rack application.

Replace ``'Hello world!'`` with ``env["REQUEST_PATH"]`` to make it respond to requests with a string of the requested path.

## Phase II: ControllerBase Class

ApplicationController inherits from ActionController::Base.  Let's write a version of ActionController::Base.

We'll call the class that we're about to write `ControllerBase` instead of `ActionController::Base`, but ControllerBase will have most of the same methods. For example, we'll write the `render` and `redirect_to` methods.

**Write a "double render" error:**

First, write a method named `#render_content(content, content_type)`. This
should set the response object's `content_type` and `body`. It should
also set an instance variable, `@already_built_response`, so that it
can check that content is not rendered twice.

Next, write a method named `#redirect_to(url)`. Issuing a redirect consists of
two parts, setting the 'Location' field of the response header to the redirect
url and setting the response status code to 302. Do not use #redirect; set each
piece of the response individually. Check the [Rack::Response][rack-response]
docs for how to set response header fields and statuses. Again, set
`@already_built_response` to avoid a double render.

Run `bundle exec ruby bin/p02_controller_server.rb`. Now look at the code to see
what it does. By extending `ControllerBase`, `MyController` can test our `#render_content` and `#redirect_to` methods. Go to localhost:3000 and make sure
it works correctly.

Lastly, run the spec: `bundle exec rspec spec/p02_controller_spec.rb`.
