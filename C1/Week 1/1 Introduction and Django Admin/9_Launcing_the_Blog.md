# Launching the Blog

Now we’re ready to check it all out. Start the Django test server by entering the following command in the terminal. The blog should load in the top panel.

```bash
python3 manage.py runserver 0.0.0.0:8000
```

Once, Django is up and running, you need to navigate to the admin page. In the project URL, add a `/admin` and press **Enter** on the keyboard.

![Django Admin URL](https://apollo-media.codio.com/media%2F1%2F30a8f6cbbbafb3a6c667dc6edaf679ed-0954713d41321fcc.webp)

## View in External Tab

If you want to see the Django application in its own tab, click the blue arrow in the top-left corner of the blog panel.

![View Blog Project in an External Tag](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

You’ll need to log in with the username and password you created earlier. Then, you should see a list of all the available models: Groups and Users (which are part of the Django auth system), then Posts and Tags, which are part of our Blog app.

![Models List](https://apollo-media.codio.com/media%2F1%2F37852841d1a6ed6d17a5f6dd8d4ae5c6-d4b51bf5815e2c9a.webp)

We’ll now quickly walk through how to create a Post. First, click on `Posts` to go to the Posts list view. You should see an empty table, with an **Add Post** button at the top.

![Add Post](https://apollo-media.codio.com/media%2F1%2F57a222bf46418758706a92dd2f47615b-9f2a3559344c87c8.webp)

Click this button, and you’ll see the Post edit form. Note that since `created_at` and `modified_at` are set automatically, they don’t show up in the fields. Likewise, the model instance’s `id`/`pk` (primary key) doesn’t show as it shouldn’t be changed.

![Post Form](https://apollo-media.codio.com/media%2F1%2F71564ff5d8777a6f53f748c6b9c0b899-8689a780664079bd.webp)

You can go through and enter some information to create a post. Note that as you enter a title, the slug automatically updates.

![Slug Updates](https://apollo-media.codio.com/media%2F1%2Fd4294672f715119f084b15ce505b5fad-8d18d5b02391e205.webp)

You can add multiple tags by clicking the green plus icon to the right of the tags list. The tag editor opens in a new window.

![Tag Editor](https://apollo-media.codio.com/media%2F1%2F7ee1216d9c27d993e605c47104777650-7700787762382b3a.webp)

Click **Save** after entering a Value for the tag, and then the Tag editor will close and you’ll return to the Post editor.

![Tags Entered](https://apollo-media.codio.com/media%2F1%2Ff285dadaf9e1f2d0448d04258b0336f4-c4a96b5760fd4754.webp)

Make sure the tags are selected, then click **Save** . You’ll go back to the Post list, and you’ll see the Post you have created.

![Posts List](https://apollo-media.codio.com/media%2F1%2F1d7b520ed323748217a85feb5031eee0-abcd656b8fec15fd.webp)

This was a quick intro to the Django Admin site.

## Try this variation:

* Try changing the `PostAdmin` to show the `slug` and `published_at` in the Post list. Use the link below to open `admin.py` to make your changes.

[Open admin.py]()

<details open=""><summary><strong>Solution</strong></summary>

Use `list_display` to change the information presented in the Post list. See the [Django Model Admin Options Documenatation](https://docs.djangoproject.com/en/3.2/ref/contrib/admin/#modeladmin-options) for more information.

```python
class PostAdmin(admin.ModelAdmin):
    prepopulated_fields = {"slug": ("title",)}
    list_display = ('slug', 'published_at')
```

</details>

That was a brief introduction to the Django Admin system, a simple but powerful way to get content into your application. We’ll often use it as it saves time having to build custom forms.

In the next section, we’ll look at the Django generic relations system, and how it can be used.

## Reading Question

Drag the code blocks into the box below. Define the `PostAdmin` class so that it will display `summary` and `content` in the Post list. **Hint** , not all of the blocks will be used, and the blocks must be properly indented.

Here is the solution:

```python
class PostAdmin(admin.ModelAdmin):
    prepopulated_fields = {"slug": ("title",)}
    list_display = ('summary', 'content')
```

* Use `list_display`, not `display_list`
* If you want the summary and the content of the post to appear, use `'summary'` and `'content'`
