# getLoadingProgress()

A MilvusClient interface. This method gets loading collection progress.

```java
R<GetLoadingProgressResponse> getLoadingProgress(GetLoadingProgressParam requestParam);
```

## LoadCollectionParam

Use the `GetLoadingProgressParam.Builder` to construct a `GetLoadingProgressParam` object.

```java
import io.milvus.param.GetLoadingProgressParam;
GetLoadingProgressParam.Builder builder = GetLoadingProgressParam.newBuilder();
```

Methods of `GetLoadingProgressParam.Builder`:

<table>
    <tr>
        <th>Method</th>
        <th>Description</th>
        <th>Parameters</th>
    </tr>
    <tr>
        <td>withCollectionName(String collectionName)</td>
        <td>Sets the collection name. Collection name cannot be empty or null.</td>
        <td>collectionName: The name of the collection to load.</td>
    </tr>
    <tr>
        <td>withPartitionNames(List\<String> partitionNames)</td>
        <td>Sets partition names list to specify query scope (Optional).</td>
        <td>partitionNames: <br/>The name list of partitions to be loaded.</td>
    </tr>
    <tr>
        <td>build()</td>
        <td>Constructs a LoadCollectionParam object.</td>
        <td>N/A</td>
    </tr>
    <tr>
        <td><code>withSyncLoadWaitingInterval(Long milliseconds)</code></td>
        <td>Sets the waiting interval for sync mode. In sync mode, the client checks the collection load status at intervals. The value must be greater than zero, and cannot be greater than <code>Constant.MAX_WAITING_LOADING_INTERVAL</code>. The default value is <code>500</code> milliseconds</td>
        <td><code>milliseconds</code>: The time interval in milliseconds for checking the data load status.</td>
    </tr>
    <tr>
        <td><code>withSyncLoadWaitingTimeout(Long seconds)</code></td>
        <td>Sets the timeout period for sync mode. The value must be greater than zero and cannot be greater than <code>Constant.MAX_WAITING_LOADING_TIMEOUT</code>. The default value is <code>60</code> seconds.</td>
        <td><code>seconds</code>: A during of time in seconds to wait till timeout.</td>
    </tr>
    <tr>
        <td><code>withReplicaNumber(Integer replicaNumber)</code></td>
        <td>Specifies the number of replicas to load. The default value is <code>1</code>.</td>
        <td><code>replicaNumber</code>: The number of the replicas to load when loading a collection.</td>
    </tr>
    <tr>
        <td><code>build()</code></td>
        <td>Constructs a <code>LoadCollectionParam</code> object</td>
        <td>N/A</td>
    </tr>
</table>

The `GetLoadingProgressParam.Builder.build()` can throw the following exceptions:

- ParamException: error if the parameter is invalid.

## Returns

This method catches all the exceptions and returns an `R<GetLoadingProgressResponse>` object.

- If the API fails on the server side, it returns the error code and message from the server.

- If the API fails by RPC exception, it returns `R.Status.Unknown` and the error message of the exception.

- If the API succeeds, it returns `R.Status.Success`.

## Example

```java
import io.milvus.param.*;

GetLoadingProgressParam param = GetLoadingProgressParam.newBuilder()
        .withCollectionName(COLLECTION_NAME)
        .build();
R<GetLoadingProgressResponse> response = client.getLoadingProgress(param);
if (response.getStatus() != R.Status.Success.getCode()) {
    System.out.println(response.getMessage());
}
System.out.println(response.getProgress());
```

