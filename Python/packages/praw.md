# Python Reddit API Wrapper(PRAW)

`import praw`

## Code Flow

```python
reddit = praw.Reddit(client_id='SI8pN3DSbt0zor', 		client_secret='xaxkj7HNh8kwg8e5t4m6KvSrbTI',
	redirect_uri='http://localhost:8080',
    user_agent='testscript by /u/fakebot3')

url_for_user_to_go_to = reddit.auth.url(['identity'], '...', 'permanent')
```

`['identity']` is where you put the reddit oauth api scopes for permissions you want

User goes to url and code passed to redirect url as query parameter

```python
refresh_token = reddit.auth.authorize(code)
logged_in = reddit.user.me()
```

##### Using Saved Refresh Token

```python
reddit=praw.Reddit(client_id='SI8pN3DSbt0zor',
 client_secret='xaxkj7HNh8kwg8e5t4m6KvSrbTI',	       
 refresh_token='WeheY7PwgeCZj4S3QgUcLhKE5S2s4eAYdxM',
 user_agent='testscriptby/u/fakebot3')
 
print(reddit.auth.scopes())
```

##### Getting User subreddits

Need `['subreddits']` scope

```python
subs = reddit.user.subreddits(limit=None)`
for sub in subs:
    print(sub)
```



