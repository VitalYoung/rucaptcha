# RuCaptcha


This is a Captcha gem for Rails Application. It run ImageMagick command to draw Captcha image.

So it's NO performance issue, and memory leak issue.

Idea by: https://ruby-china.org/topics/20558#reply4

### Requirements

- ImageMagick

### Example

![simple4](https://cloud.githubusercontent.com/assets/5518/10726106/9442b1fe-7c0b-11e5-8c06-f88fce5e7a58.png)  ![simple3](https://cloud.githubusercontent.com/assets/5518/10726119/a844dfce-7c0b-11e5-99c3-a818f3ef3dd2.png)


### Usage

Put rucaptcha in your `Gemfile`:

```
gem 'rucaptcha'
```

Create `config/initializes/rucaptcha.rb`

```rb
RuCaptcha.configure do
  # Number of chars, default: 4
  self.len = 4
  # Image width, default: 180
  self.width = 180
  # Image height, default: 48
  self.height = 48
end
```

Controller `app/controller/account_controller.rb`

```rb
class AccountController < ApplicationController
  def create
    @user = User.new(params[:user])
    if verify_rucaptcha?(@user) && @user.save
      redirect_to root_path, notice: 'Sign up successed.'
    else
      render 'account/new'
    end
  end
end
```

View `app/views/account/new.html.erb`

```erb
<form>
  ...
  <div class="form-group">
    <%= rucaptcha_input_tag(class: 'form-control', placeholder: 'Input Captcha') %>
    <%= rucaptcha_image_tag(alt: 'Captcha') %>
  </div>
  ...
</form>
```

