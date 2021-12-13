# Action Text

**Action Text** is responsible for provide rich text content. This means that instead of plain text, we can add bold, quotes, attachments and other stuff. **Action Text** includes the **Trix** editor, which deals with text format.

### Setup

To use image embedding and other attachments, **Active Storage** must be configured.

rails action_text: install

This command will include **.js** and **.css** files for **Trix** and **Action Text **

### Example

``` Ruby
class Article < ApplicationRecord
  has_rich_text :content
end

# Edit content
<%= form_with model: article do |form| %>
  <%= form.rich_text_area :content %>
<% end %>

# Display content
<%= @article.content %>
```

### Custom styling

By default, the appearance of the editor and content is set by default by **Trix**. If we want to change it, we just need to overwrite the **actiontext.scss** file.
