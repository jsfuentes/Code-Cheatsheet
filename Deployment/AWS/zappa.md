# Zappa

Zappa is for deploying serverless python apps to AWS Lambda,

-  Use **Python 3.9.16**, currently only supports 3.6-3.9

```bash
pip install zappa
zappa init
zappa deploy
```

To update prod later

```bash
zappa update production
```

To check fails and logs

```
zappa tail production
```

*If deploy fails cuz no psycopg2 and its in the requirements.txt try `pip install psycopg2-binary`

## Guides

[Flask](https://medium.com/hacktive-devs/deploy-flask-applications-as-aws-lambda-with-zappa-962409687240)

![Screenshot 2023-03-24 at 10.20.59 AM](/Users/jfuentes/Library/Containers/at.EternalStorms.Yoink/Data/Documents/YoinkPromisedFiles/yoinkFilePromiseCreationFolder85557727-3A1F-4D88-B72C-5D66903503C6/add85557727-3A1F-4D88-B72C-5D66903503C6/Screenshot 2023-03-24 at 10.20.59 AM.png)

