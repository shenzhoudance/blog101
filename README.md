# README

构建 blog101 的专案
```
rails new blog101
cd blog101
git init
git add .
git commit -m "first commit"
```

构建 posts 的分支
```
git checkout -b posts
rails g controller posts
resources :posts
```
app/controllers/posts_controller.rb
```
def index
end

def new
end

end
```
app/views/posts/index.html.erb
```
<h1>欢迎来到才华横溢</h1>
```
app/views/posts/new.html.erb
```
<h1>new post</h1>

<%= form_for :post,url: posts_path do |f| %>
<p>
  <%= f.label :title %><br>
  <%= f.text_field :title,class:"form-control" %>
</p>

<p>
  <%= f.label :body %><br>
  <%= f.text_area :body,class:"form-control" %>
</p>

<p class="btn btn-primary" >
  <%= f.submit %>
</p>
<% end %>
```

```
rails g model Post title:string body:text
rake db:migrate
```

app/controllers/posts_controller.rb
```
def index
  @posts = Post.all.order('created_at DESC')
end

def new
end

def create
  @post = Post.new(post_params)
  @post.save

  redirect_to @post
end

def show
  @post = Post.find(params[:id])

end

private
 def post_params
   params.require(:post).permit(:title,:body)
end
end
```
app/views/posts/show.html.erb
```
<h1 class="title">
<%= @post.title %>
</h1>

<p class="date">
  Submitted <%= time_ago_in_words(@post.created_at) %> Ago
</p>

<p class="body">
  <%= @post.body %>
</p>
```
git add .
git commit -m "Add the posts"
git push origin posts
---
https://necolas.github.io/normalize.css/latest/normalize.css
