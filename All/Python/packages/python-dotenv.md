# Environment Variables

`python-dotenv` package can handle environment variables that you put in a `.env` file 

```
CONFIG_PATH=${HOME}/.config/foo
DOMAIN=example.org
EMAIL=admin@${DOMAIN}
```

gitignore this .env 

```python
from dotenv import load_dotenv
load_dotenv()

import os
SECRET_KEY = os.getenv("EMAIL")
DATABASE_PASSWORD = os.getenv("DATABASE_PASSWORD")
```

flask run auto does this