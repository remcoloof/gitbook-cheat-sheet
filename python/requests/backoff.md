# Backoff

The [backoff](https://pypi.org/project/backoff/) package allows for retrying certain logic when a certain exception occurs. This is mainly useful for making requests to external API's that can fail once in a while.&#x20;

## Default

```python
@backoff.on_exception(backoff.expo, (RequestException, SalesforceError), max_tries=3)
def perform_request_standard():
    response = requests.get("https://jsonplaceholder.typicode.com/tods/1")
    response.raise_for_status()
    return response.json()
```

Running the function above will retry the code three times with an exponential backoff. This is the easiest way to implement the backoff.

## Try except block

```python
@backoff.on_exception(backoff.expo, (RequestException, SalesforceError), max_tries=3)
def perform_request_try_except_block():
    response = requests.get("https://jsonplaceholder.typicode.com/tods/1")
    print("done")
    try:
        response.raise_for_status()
    except (RequestException, SalesforceError) as exc:
        logging.error(f"An error has occured! Exception: {exc }, Response: {response.json()}")
        raise exc
    return response.json()
```

It is possible that we would like to pefrom some additonal steps when the execption occurs. To do so, we make use of the try-except block. In the except clause we can include additional logic, e.g. logging. Next, we need to re-raise the error to ensure that the backoff is called.
