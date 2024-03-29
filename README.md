# Sinatra Views: Using ERB

## Overview

We'll look at the benefits of view templating and learn how to write ERB tags that do more than just display data.

## Objectives

1. Define and explain the benefits of view templating
2. Use ERB substitution and scripting tags to modify the content and structure of HTML code
3. Incorporate logic and iteration using ERB. 


## Overview

Most major web frameworks provide some means of view templating, i.e., allowing the view, in our case an HTML document, to be constructed using a combination of HTML and Ruby code.

This allows us to greatly reduce duplication of HTML as well as generate content that can change based on the available data. This is how Facebook can support 2 billion users –– they create one template for the profile page, which then gets filled out with distinct, individualized user data from their servers.

For this lesson, we will be using the ERB templating engine, which comes standard with every Ruby installation.

## Embedding Ruby

ERB and other templating engines allow us to modify the content and structure of our HTML code. With ERB, we do this using two different types of tags: the substitution tag (`<%=`) and the scripting tag (`<%`).

### Substitution Tags

The substitution tag evaluates Ruby code and then displays the results into the view. It opens with `<%=` and closes with `%>`. Inside of these tags, you can write any valid Ruby code that you want.

There aren't any tests for this lesson, but feel free to reopen the `index.erb` file from the previous lesson and code along. You'll also want to restart your Shotgun server by entering `shotgun` from the lesson directory in terminal. In `index.erb`, add the following code, which should render in the browser as `I love Ruby!!`:

```erb
<%= "I love " + "Ruby!!" %>
```

The strings are concatenated first and then displayed on the page. What do you think would be displayed by the following lines of code?

```erb
<%= 1 + 1 %>
```

If you guessed `2`, you're right! In general, we use substitution tags when we want to display some evaluation on the page.

We can wrap the substitution tags in any other HTML tags that we like. The code below will output `<h1>I love Ruby!!</h1>`:

```erb
<h1><%= "I love " + "Ruby!!" %></h1>
```

### Scripting Tags

Scripting tags open with `<%` and close with `%>`. They evaluate –– but do not actually display –– Ruby code. Add the following lines of code to `index.erb`:

```erb
<% if 1 == 2 %>
  <p>1 equals 2.</p>
<% else %>
  <p>1 does not equal 2.</p>
<% end %>
```

As you can see, only the second `<p>` tag was sent to the browser. This example is a bit silly, because 1 will never be equal to 2. 

However, imagine that you work at Facebook and that you have a method called `logged_in?` that returns `true` if a user is logged in and `false` if they're not. You could then show different content based on whether or not a user is logged in. The following is an example of what this code may look like:

```erb
<% if logged_in? %>
  <a href="/logout">Click here to Log Out</a>
<% else %>
  <a href="/login">Click here to Log In</a>
<% end %>
```

**Note:** This code is not part of the codealong, you will receive a `NoMethodError`.

### Iteration

We can also use iteration to manage lists of items. For instance, given an array `squares = [1,4,9,16]`:

```erb
<ul>
  <% squares = [1, 4, 9, 16] %>
  <% squares.each do |square| %>
    <li><%= square %></li>
  <% end %>
</ul>
```

Would produce:

```html
<ul>
  <li>1</li>
  <li>4</li>
  <li>9</li>
  <li>16</li>
</ul>
```

Notice that we use the substitution tag to display the value of the inner `square` variable. Again, imagine you're at Facebook and you want to print out all of the wall posts on a given profile page. They could store the posts in an array called `wall_posts`. Add the following line of code to your `index.erb` file:

```erb
<% wall_posts = ["First post!", "Second post!", "Hello, it's your mother. Why don't you ever call me?"] %>
```

Here, we're defining a variable called `wall_posts` and assigning its value to an array of strings. Now we can iterate through our `wall_posts` array and create a new `<li>` item for each one. 

```erb
<ul>
  <% wall_posts.each do |post| %>
    <li><%= post %></li>
  <% end %>
</ul>
```

This should display: 

```html
<ul>
  <li>First Post!</li>
  <li>Second Post!</li>
  <li>Hello, it's your mother. Why don't you ever call me?</li>
</ul>
```

## Resources

- [An Introduction to ERB Templating - Stuart Ellis](https://www.stuartellis.name/articles/erb/)
- [A cheatsheet on choosing ERB tags](https://medium.com/swlh/cheatsheet-which-erb-tag-should-i-use-4b3de261f15f)

