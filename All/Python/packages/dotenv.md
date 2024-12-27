# Environment Variables

```bash
pip install python-dotenv
```

`python-dotenv` reads key-value pairs from a `.env` file and sets them as environment variables

.env (git ignore this)

```
CONFIG_PATH=${HOME}/.config/foo
DOMAIN=example.org
EMAIL=admin@${DOMAIN}
```

script.py

```python
from dotenv import load_dotenv
import os

load_dotenv()

SECRET_KEY = os.getenv("EMAIL")
DATABASE_PASSWORD = os.getenv("DATABASE_PASSWORD")
```

flask run auto does this