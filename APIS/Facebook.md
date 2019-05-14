# Facebook Login

Requires Redirect URL to be https, but you can also use localhost

Use the Facebook sdk

Non sdk is oauth flow

Need to have your app domain on you main settings page, and the redirect url and at the bottom of that page url all the SAME

App secret is now on the settings page

All this is to get the holy user access token

## Access Token

Once you acquire an access token you can now use the graph api and append` ?access_token={access_token}` to the query such as 

```
https://graph.facebook.com/me?access_token=EAALuFEXM4agBAB6DDyPpBTlJiDgHzZCJEi0Vjo0DjyyFuwsQOkpgAvrt825ZBdWy7Ihi2I8XL63FZAAG394lheHMS9rDZBtdeIK74QkS8YYOWfL5ZAeuX7qM5ZBFFQbomIC3ba6a3ZB5X5Nb5jDHvbEJGUdzxyZCdmfzfAEk2DbibYXkWtF7s42n
```

*No that isn't a real access token*

#### Friends

WIth the user_friends permissions

```
https://graph.facebook.com/me
   ?fields=friends
   &access_token={your-user-access-token}
```

```python
params = {
  'fields': 'friends, name, id, picture',
  'access_token': access_token
}
r = requests.get('https://graph.facebook.com/me', params=params)
```

