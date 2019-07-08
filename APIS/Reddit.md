# Reddit API

Python => Praw(Python Reddit API Wrapper)

1) https://www.reddit.com/prefs/apps - And add an app to get secret

2) Send the user to the auth url: 

```
https://www.reddit.com/api/v1/authorize?client_id=CLIENT_ID&response_type=TYPE&
state=RANDOM_STRING&redirect_uri=URI&duration=DURATION&scope=SCOPE_STRING
```

3) If authed, the user redirected to redirect_uri with code and state in query string

4) Post to the `https://www.reddit.com/api/v1/access_token`  with `grant_type=authorization_code&code=CODE&redirect_uri=URI`

....

## Dealing With Stuff

### Determine Available Attributes of an Object

If you have a PRAW object, e.g., [`Comment`](https://praw.readthedocs.io/en/latest/code_overview/models/comment.html#praw.models.Comment), [`Message`](https://praw.readthedocs.io/en/latest/code_overview/models/message.html#praw.models.Message), [`Redditor`](https://praw.readthedocs.io/en/latest/code_overview/models/redditor.html#praw.models.Redditor), or [`Submission`](https://praw.readthedocs.io/en/latest/code_overview/models/submission.html#praw.models.Submission), and you want to see what attributes are available along with their values, use the built-in [`vars()`](https://docs.python.org/3.6/library/functions.html#vars) function of python. For example:

```
import pprint

# assume you have a Reddit instance bound to variable `reddit`
submission = reddit.submission(id='39zje0')
print(submission.title) # to make it non-lazy
pprint.pprint(vars(submission))
```

Note the line where we print the title. PRAW uses lazy objects so that network requests to Reddit’s API are only issued when information is needed. Here, before the print line, `submission` points to a lazy [`Submission`](https://praw.readthedocs.io/en/latest/code_overview/models/submission.html#praw.models.Submission) object. When we try to print its title, additional information is needed, thus a network request is made, and the instances ceases to be lazy. Outputting all the attributes of a lazy object will result in fewer attributes than expected.