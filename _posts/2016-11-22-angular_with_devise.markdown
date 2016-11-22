---
layout: post
title:  "Angular with Devise"
date:   2016-11-22 00:20:15 +0000
---


For this blog post, I have decided to create a video walkthrough of how to create an Angular application with Devise for basic authentication. 

Getting started on my Angular portfolio project, this was one of the my biggest hurdles. Online resources were sparce, incomplete, or overwhelming, so I decided to create a guide.

The link can be found here: https://youtu.be/ieoxzX-VPL4

Here are the steps I took:

`$ rails new YOUR-APP`

Add the following to your `Gemfile`:
`gem 'bower-rails'`
`gem 'devise'`
`gem 'angular-rails-templates'`
`gem 'active-model-serializer'`
`gem 'bootstrap-sass', '~> 3.3.6'`
* remove turbolinks gem

`$ rake db:create`
`$ rails g bower_rails:initialize json`
`$ rails g devise:install`
`$ rails g migration AddUsernametoUsers username:string:uniq`
`$ rake db:migrate`

Add the following vendor dependencies to `bower.json`:
`"angular": "v1.5.8"`
`"angular-ui-router": "latest"`
`"angular-devise": "latest"`

`$ bundle install`
`$ rake bower:install`
`$ rails g serializer user`
Then add `:username` to `user_serializer.rb`

#config/routes.rb
add `root 'application#index'`

Create `app/views/application/index.html.erb`
Copy contents from `views/layouts/application.html.erb` to `index.html.erb`, then delete `application.html.erb`
replace `<%= yield %>` with `<ui-view></ui-view>`

Add the following in `config/application.rb` directly under `class Application < Rails::Application`:
```
config.to_prepare do
	DeviseController.respond_to :html, :json
end
```

#app/controllers/application_controller.rb
```
class ApplicationController < ActionController::Base
  protect_from_forgery with: :exception
  before_action :configure_permitted_parameters, if: :devise_controller?
  skip_before_action :verify_authenticity_token

  respond_to :json

  def index
    render 'application/index'
  end

  protected

  def configure_permitted_parameters
    added_attrs = [:username, :email, :password, :password_confirmation, :remember_me]
    devise_parameter_sanitizer.permit :sign_up, keys: added_attrs
    devise_parameter_sanitizer.permit :account_update, keys: added_attrs
  end
end
```

#app/controllers/users_controller.rb
```
def show
  user = User.find(params[:id])
  render json: user
end
```

Require the following in `app/assets/javascript/application.js`:
```
//= require jquery
//= require jquery_ujs
//= require angular
//= require angular-ui-router
//= require angular-devise
//= require angular-rails-templates
//= require bootstrap-sprockets
//= require_tree .
```

Rename `app/assets/stylesheets/application.css` to `application.scss` and add
```
*
 *= require_tree .
 *= require_self
 */
@import "bootstrap-sprockets";
@import "bootstrap";
```

Now stub out your Angular tree:
```
/javascript/controllers/AuthCtrl.js
/javascript/controllers/HomeCtrl.js
/javascript/controllers/NavCtrl.js
/javascript/directives/NavDirective.js
/javascript/views/home.html
/javascript/views/login.html
/javascript/views/register.html
/javascript/views/nav.html
/javascript/app.js
/javascript/routes.js
```

Finally I would suggest visiting the repo I published to review the route.js and controller logic which is easy to mess up if you're not careful. 

https://github.com/jessenovotny/angular-devise-demo

Essentially, you're going to setup states to use the AuthCtrl which will have the Devise `Auth` service injected and used for authenticating the user and broadcasting the result (signup/login/logout) as an event to the application and provide your controllers with a `user` to get info from and/or manipulate data for.
