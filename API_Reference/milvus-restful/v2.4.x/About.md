# Get Started

Milvus offers RESTful API for you to manipulate your collections and data stored in them. Before you dive in, there are several things that are worth noting:

## Understanding the API endpoints

These API endpoints involve manipulating collections in a specified cluster as well as the data in a specific collection.

The prefix of an API endpoint should always be the URI of your Milvus instance, such as `localhost:19530`.

The following is the API endpoint used to list collections in a Milvus cluster.

```shell
export MILVUS_URI="http://localhost:19530"

curl --request GET \
    --url '${MILVUS_URI}/v1/vector/collections' \
    --header 'accept: application/json' \
    --header 'content-type: application/json'
```

## Authentication credentials

With default settings, you do not need to provide any authentication credentials to access the API endpoints. However, if you have enabled authentication in your Milvus instance, you need to provide the correct credentials in the request header. You can use a token as the authentication method when you access the API endpoints. To obtain a token, you should use a colon (:) to concatenate the username and password that you use to access your Milvus instance. For example, `root:milvus`.

```shell
export MILVUS_URI="http://localhost:19530"
export TOKEN="root:milvus"

curl --request GET \
    --url '${MILVUS_URI}/v1/vector/collections' \
    --header "Authorization: Bearer ${TOKEN}" \
    --header 'accept: application/json' \
    --header 'content-type: application/json'
```

## API endpoint versioning

Since v2.3.13, Milvus starts to offer two sets of API endpoints, namely v1 and v2. The v1 endpoints only covers collection and vector operations, while the v2 endpoints cover more operations such as index management, partition management, and role-based access control (RBAC) operations. The v2 endpoints are the latest and recommended set of endpoints.
