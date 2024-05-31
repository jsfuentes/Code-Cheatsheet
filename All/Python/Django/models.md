# Models

Unlike Ruby/Phoenix, migrations are entirely derived from the models

## Using Models

### Importing

```python
from polls.models import Choice, Question
```

### Querying

```python
Question.objects.all() #<QuerySet []>
Question.objects.filter(id=1)
Question.objects.filter(question_text__startswith='What')

# Identical
Question.objects.get(pk=1)
Question.objects.get(id=1)

Question.objects.get(pub_date__year=timezone.now().year) #Will throw error if doesn't exist
```

#### Querying through relations

Use two underscores to seperate relationships with unlimited layers

```python
Choice.objects.filter(question__pub_date__year=current_year)
```

### Creation

```python
from django.utils import timezone

q = Question(question_text="What's new?", pub_date=timezone.now())
q.save()
q.id #Q now has an id
```

Updating

```python
q.question_text = "What's up?"
q.save()
```

#### Children

If choice is a child of q

```python
q.choice_set.all() #<QuerySet[]>
q.choice_set.count() #0

c = q.choice_set.create(choice_text='Not much', votes=0)

c.question.question_text #has access to parent
```

### Delete

```
q.delete()
```



## Creating New Model

```python
import datetime
from django.db import models
from django.utils import timezone

class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')
    
    def __str__(self): #For better logging/admin
        return self.question_text
      
    def was_published_recently(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
    
    def __str__(self):
        return self.choice_text
```

- Table names will be app and model in lowercase e.g `polls_question`
- Columns will be field e.g `question_text`

### Migrations

After making changes to the model file, you need to create the migrations with:

```python
poetry run python manage.py makemigrations polls
```

Then actually run the migrations

```bash
poetry run python manage.py migrate
```

