# Replicate

```shell
pip install replicate
```

Next, [copy your API token](https://replicate.com/account) and authenticate by setting it as an environment variable:

```console
export REPLICATE_API_TOKEN=[token]
```

Then, run the model:

```python
import replicate
output = replicate.run(
    "devxpy/cog-wav2lip:8d65e3f4f4298520e079198b493c25adfc43c058ffec924f2aefc8010ed25eef",
    input={"face": open("path/to/file", "rb")}
)
print(output)
```