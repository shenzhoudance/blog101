# README

# 构建 blog101 的专案
```
rails new blog101
cd blog101
git init
git add .
git commit -m "first commit"
```

# 构建 posts 的分支
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

# git checkout -b styling

https://necolas.github.io/normalize.css/latest/normalize.css

app/assets/stylesheets/normalize.css.scss
```
/*! normalize.css v8.0.0 | MIT License | github.com/necolas/normalize.css */

/* Document
   ========================================================================== */

/**
 * 1. Correct the line height in all browsers.
 * 2. Prevent adjustments of font size after orientation changes in iOS.
 */

html {
  line-height: 1.15; /* 1 */
  -webkit-text-size-adjust: 100%; /* 2 */
}

/* Sections
   ========================================================================== */

/**
 * Remove the margin in all browsers.
 */

body {
  margin: 0;
}

/**
 * Correct the font size and margin on `h1` elements within `section` and
 * `article` contexts in Chrome, Firefox, and Safari.
 */

h1 {
  font-size: 2em;
  margin: 0.67em 0;
}

/* Grouping content
   ========================================================================== */

/**
 * 1. Add the correct box sizing in Firefox.
 * 2. Show the overflow in Edge and IE.
 */

hr {
  box-sizing: content-box; /* 1 */
  height: 0; /* 1 */
  overflow: visible; /* 2 */
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

pre {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/* Text-level semantics
   ========================================================================== */

/**
 * Remove the gray background on active links in IE 10.
 */

a {
  background-color: transparent;
}

/**
 * 1. Remove the bottom border in Chrome 57-
 * 2. Add the correct text decoration in Chrome, Edge, IE, Opera, and Safari.
 */

abbr[title] {
  border-bottom: none; /* 1 */
  text-decoration: underline; /* 2 */
  text-decoration: underline dotted; /* 2 */
}

/**
 * Add the correct font weight in Chrome, Edge, and Safari.
 */

b,
strong {
  font-weight: bolder;
}

/**
 * 1. Correct the inheritance and scaling of font size in all browsers.
 * 2. Correct the odd `em` font sizing in all browsers.
 */

code,
kbd,
samp {
  font-family: monospace, monospace; /* 1 */
  font-size: 1em; /* 2 */
}

/**
 * Add the correct font size in all browsers.
 */

small {
  font-size: 80%;
}

/**
 * Prevent `sub` and `sup` elements from affecting the line height in
 * all browsers.
 */

sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}

/* Embedded content
   ========================================================================== */

/**
 * Remove the border on images inside links in IE 10.
 */

img {
  border-style: none;
}

/* Forms
   ========================================================================== */

/**
 * 1. Change the font styles in all browsers.
 * 2. Remove the margin in Firefox and Safari.
 */

button,
input,
optgroup,
select,
textarea {
  font-family: inherit; /* 1 */
  font-size: 100%; /* 1 */
  line-height: 1.15; /* 1 */
  margin: 0; /* 2 */
}

/**
 * Show the overflow in IE.
 * 1. Show the overflow in Edge.
 */

button,
input { /* 1 */
  overflow: visible;
}

/**
 * Remove the inheritance of text transform in Edge, Firefox, and IE.
 * 1. Remove the inheritance of text transform in Firefox.
 */

button,
select { /* 1 */
  text-transform: none;
}

/**
 * Correct the inability to style clickable types in iOS and Safari.
 */

button,
[type="button"],
[type="reset"],
[type="submit"] {
  -webkit-appearance: button;
}

/**
 * Remove the inner border and padding in Firefox.
 */

button::-moz-focus-inner,
[type="button"]::-moz-focus-inner,
[type="reset"]::-moz-focus-inner,
[type="submit"]::-moz-focus-inner {
  border-style: none;
  padding: 0;
}

/**
 * Restore the focus styles unset by the previous rule.
 */

button:-moz-focusring,
[type="button"]:-moz-focusring,
[type="reset"]:-moz-focusring,
[type="submit"]:-moz-focusring {
  outline: 1px dotted ButtonText;
}

/**
 * Correct the padding in Firefox.
 */

fieldset {
  padding: 0.35em 0.75em 0.625em;
}

/**
 * 1. Correct the text wrapping in Edge and IE.
 * 2. Correct the color inheritance from `fieldset` elements in IE.
 * 3. Remove the padding so developers are not caught out when they zero out
 *    `fieldset` elements in all browsers.
 */

legend {
  box-sizing: border-box; /* 1 */
  color: inherit; /* 2 */
  display: table; /* 1 */
  max-width: 100%; /* 1 */
  padding: 0; /* 3 */
  white-space: normal; /* 1 */
}

/**
 * Add the correct vertical alignment in Chrome, Firefox, and Opera.
 */

progress {
  vertical-align: baseline;
}

/**
 * Remove the default vertical scrollbar in IE 10+.
 */

textarea {
  overflow: auto;
}

/**
 * 1. Add the correct box sizing in IE 10.
 * 2. Remove the padding in IE 10.
 */

[type="checkbox"],
[type="radio"] {
  box-sizing: border-box; /* 1 */
  padding: 0; /* 2 */
}

/**
 * Correct the cursor style of increment and decrement buttons in Chrome.
 */

[type="number"]::-webkit-inner-spin-button,
[type="number"]::-webkit-outer-spin-button {
  height: auto;
}

/**
 * 1. Correct the odd appearance in Chrome and Safari.
 * 2. Correct the outline style in Safari.
 */

[type="search"] {
  -webkit-appearance: textfield; /* 1 */
  outline-offset: -2px; /* 2 */
}

/**
 * Remove the inner padding in Chrome and Safari on macOS.
 */

[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}

/**
 * 1. Correct the inability to style clickable types in iOS and Safari.
 * 2. Change font properties to `inherit` in Safari.
 */

::-webkit-file-upload-button {
  -webkit-appearance: button; /* 1 */
  font: inherit; /* 2 */
}

/* Interactive
   ========================================================================== */

/*
 * Add the correct display in Edge, IE 10+, and Firefox.
 */

details {
  display: block;
}

/*
 * Add the correct display in all browsers.
 */

summary {
  display: list-item;
}

/* Misc
   ========================================================================== */

/**
 * Add the correct display in IE 10+.
 */

template {
  display: none;
}

/**
 * Add the correct display in IE 10.
 */

[hidden] {
  display: none;
}

```
app/assets/stylesheets/application.scss
```
/*
 * This is a manifest file that'll be compiled into application.css, which will include all the files
 * listed below.
 *
 * Any CSS and SCSS file within this directory, lib/assets/stylesheets, or any plugin's
 * vendor/assets/stylesheets directory can be referenced here using a relative path.
 *
 * You're free to add application-wide styles to this file and they'll appear at the bottom of the
 * compiled file so the styles you add here take precedence over styles defined in any other CSS/SCSS
 * files in this directory. Styles in this file should be added after the last require_* statement.
 * It is generally better to create a new file per style scope.
 *
 *= require_tree .
 *= require_self
 */
 @import 'normalize';

 html, body {
 	font-family: 'Raleway', sans-serif;
 }

 h1, h2, h3, h4, h5, h6 {
 	font-weight: 500;
 }

 a {
 	text-decoration: none;
 	color: inherit;
 }

 #sidebar {
 	width: 250px;
 	position: fixed;
 	left: 0;
 	top: 0;
 	height: 100%;
 	background: #f5f7f9;
 	padding: 7em 0 0 0;
 	border-right: 1px solid #d6dce0;
 	#logo {
 		width: 40px;
 		position: absolute;
 		right: 3em;
 		top: 3em;
 	}
 	ul {
 		list-style: none;
 		text-align: right;
 		padding-right: 3em;
 		.category {
 			font-weight: 700;
 			font-size: 0.7em;
 			text-transform: uppercase;
 			color: #33acb7;
 		}
 		li {
 			padding: .5em 0;
 			a {
 				color: #9eafba;
 				text-decoration: none;
 				transition: all .4s ease;
 				&:hover {
 					color: #33acb7;
 				}
 			}
 		}
 		.active {
 			a {
 				color: #33acb7;
 			}
 		}
 	}
 	.sign_in {
 		position: absolute;
 		right: 3em;
 		top: 80%;
 		font-size: .8em;
 		color: #9eafba;
 	}
 }

 .button {
 	outline: none;
 	background: transparent;
 	border: 1px solid #d6dce0;
 	padding: .5em 1.5em;
 	border-radius: 1.5em;
 	&:hover {
 		border: 1px solid #33acb7;
 		color: #33acb7;
 		a {
 			color: #33acb7 !important;
 		}
 	}
 }

 .clearfix:after {
    content: ".";
    visibility: hidden;
    display: block;
    height: 0;
    clear: both;
 }

 #main_content {
 	margin-left: 250px;
 	#header {
 		padding: 1em 3em;
 		border-bottom: 1px solid #d6dce0;
 		background: #f5f7f9;
 		color: #9eafba;
 		p {
 			display: inline;
 		}
 		a {
 			color: #9eafba;
 			text-decoration: none;
 		}
 		.buttons {
 			float: right;
 			margin-top: -6px;
 			.button {
 				font-size: .8em;
 				margin-left: .5em;
 			}
 		}
 	}
 	.post_wrapper {
 		padding: 3em;
 		border-bottom: 1px solid #d6dce0;
 		.title {
 			margin: 0;
 			a {
 				font-weight: 500;
 				text-decoration: none;
 				color: #2a2f35;
 				font-size: 1.5em;
 				&:hover {
 					color: #33acb7;
 				}
 			}
 		}
 		.date_and_author {
 			color: #9eafba;
 			margin: .5em 0 0 0;
 		}
 	}
 	#post_content {
 		padding: 1em 3em;
 		.title {
 			font-weight: 500;
 			text-decoration: none;
 			color: #2a2f35;
 			font-size: 2.5em;
 			margin-bottom: 0;
 		}
 		.body {
 			font-size: 1.1em;
 			line-height: 1.75;
 		}
 		.date_and_author {
 			color: #9eafba;
 			margin: .5em 0 2em 0;
 		}
 		#comments {
 			h2 {
 				margin: 3em 0 1em 0;
 				border-bottom: 1px solid #d6dce0;
 				padding-bottom: 0.5em;
 			}
 			h3 {
 				margin-top: 2em;
 			}
 			.comment {
 				border-bottom: 1px solid #d6dce0;
 				padding: 1.5em 2em;
 				.clear_both {
 					clear: both;
 				}
 				&:after {
 					clear: both;
 				}
 				.comment_content {
 					float: left;
 					.comment_name {
 						margin: 1em 0 0 0;
 						font-size: 0.7em;
 						text-transform: uppercase;
 					}
 					.comment_body {
 						font-size: 1.2em;
 						margin: 0.2em 0 0 0;
 					}
 					.comment_time {
 						margin-top: 1.2em;
 						font-size: .8em;
 					}
 				}
 				.button {
 					float: right;
 				}
 			}
 			input[type="text"], textarea {
 				width: 50%;
 			}
 		}
 	}
 	#page_wrapper {
 		padding: 3em;
 		#profile_image {
 			width: 300px;
 			float: left;
 			margin-right: 2em;
 			img {
 				width: 100%;
 				border-radius: 0.35em;
 			}
 		}
 		#content {
 			h1 {
 				font-weight: 500;
 			}
 			p {
 				font-size: 1.1em;
 				line-height: 1.75;
 			}
 			a {
 				color: #33acb7;
 				font-weight: 700;
 				text-decoration: none;
 			}
 		}
 	}
 	.links {
 		margin: 2em 0;
 	}
 	input[type="text"], input[type="email"], input[type="password"], textarea {
 		width: 90%;
 		border: 1px solid #d6dce0;
 		border-radius: .35em;
 		margin-top: 10px;
 		padding: .5em 1em;
 		line-height: 1.75;
 	}
 	input[type="text"] {
 		height: 35px;
 	}
 	textarea {
 		min-height: 180px;
 	}
 	input[type="submit"] {
 		outline: none;
 		background: transparent;
 		border: 1px solid #d6dce0;
 		padding: .5em 1.5em;
 		font-size: 1.1em;
 		border-radius: 1.5em;
 		margin-left: .5em;
 		&:hover {
 			border: 1px solid #33acb7;
 			color: #33acb7;
 		}
 	}
 }

```
app/views/layouts/application.html.erb

```
<!DOCTYPE html>
<html>
  <head>
    <title>Blog101</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track' => true %>


  </head>

  <body>
    <div id="sidebar">
		<div id="logo">
			<%= link_to root_path do %>

			<% end %>
		</div>

		<ul>
			<li class="category">Website</li>
			<li><%= link_to "Blog", root_path %></li>

		</ul>

		<ul>
			<li class="category">Social</li>
			<li><a href="https://twitter.com/shenzhoudance">Twitter</a></li>
			<li><a href="http://facebook.com/wei.xiao.ruby">Facebook</a></li>
			<li><a href="https://github.com/shenzhoudance">Github</a></li>
			<li><a href="mailto:494410617@qq.com">Email</a></li>
		</ul>
    <p class="sign_in">admin login</p>
   </div>

   <div id="main_content">
     <div id="header">


     <p><%= link_to "All Posts", root_path %></p>



     <div class="buttons">
       <button class="button"><%= link_to "New Post", new_post_path %></button>
       <button class="button">Log Out</button>
     </div>

 </div>

 <% flash.each do |name, msg| %>
   <%= content_tag(:div, msg, class: "alert") %>
 <% end %>

     <%= yield %>
    </div>
  </body>
</html>

```
app/views/posts/new.html.erb
```
<div id="page_wrapper">
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
</div>
```
app/views/posts/show.html.erb
```
<div id="post_content">
      <h1 class="title">
    <%= @post.title %>
    </h1>

    <p class="date">
      Submitted <%= time_ago_in_words(@post.created_at) %> Ago
    </p>

    <p class="body">
      <%= @post.body %>
    </p>
</div>
```
---
git add .
git commit -m "Styling and Structure“
git push origin styling
---
