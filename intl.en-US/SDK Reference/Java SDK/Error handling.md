# Error handling {#concept_43022_zh .concept}

## Method {#section_mlb_dl2_2fb .section}

Currently, the Table Store Java SDK adopts the `Exception` method to handle errors. The operation is successful if the called interface does not throw an exception. If an exception is thrown, the operation fails.

**Note:** Batch operation interfaces such as BatchGetRow and BatchWriteRow are successfully called only when the system checks that no exception is thrown and the status of each row is successful.

## Exceptions { .section}

The Table Store Java SDK has two types of exceptions: ClientException and TableStoreException, inherited from RuntimeException.

-   ClientException: Indicates an internal SDK exception, for example, an incorrect parameter value.

-   TableStoreException: Indicates a server error generated by parsing a server error message. TableStoreException has the following components:

    -   getHttpStatus\(\): Returned HTTP code, for example, 200 or 404.

    -   getErrorCode\(\): Error type string returned by Table Store.

    -   getRequestId\(\): The UUID used as a unique identifier for this request. If you cannot solve a problem, save the RequestId and [open a ticket](https://selfservice.console.aliyun.com/ticket/createIndex).


