---
layout: post
title: "Debugging 'render_template' errors in Rspec"
date: 2012-12-12 19:19
comments: true
categories: 
---

Debugging rspec can be a b*tch sometimes! I spent way too long stuck on this one error today, and only realized what was happening after stepping away and clearing my head. Here is a simple controller spec that verifies that the `new` action is working as expected:

```ruby
describe AssignmentsController do
  describe 'GET #new' do
    it "assigns a new Assignment to @assignment" do
      get :new
      assigns(:assignment).should be_a_new(Assignment)
    end

    it "renders the :new template" do
      get :new, :format => "html"
      response.should render_template :new
    end
  end
end
```

However this would fail awfully over and over and over. Check out how unhelpful the error message is below:
```
Failure/Error: response.should render_template("new")
     expecting <"new"> but rendering with <"">
```

So what does this really mean? It means that the response is being directed elsewhere, either before or doing the `new` action. For myself, this was occurring because this portion of the application requires user authentication. So the test request was being redirected to login instead. To fix this, you need to fake authentication in your tests. I added a before condition to these tests and they passed with flying colors.

```ruby
before :each do
  @user = FactoryGirl.create(:user)
  session[:user_id] = @user.id
end
```

Ahh rspec, why do you make me hate you? And why do I keep coming back? =/