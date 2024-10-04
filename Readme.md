
## `postReq(url, data, options)`

### Description

The `postReq` function is a custom AJAX utility that provides a standardized way to send asynchronous HTTP requests to the BotsApp server. It simplifies data communication and offers advanced features like progress tracking and request cancellation.

When i was creating my [Botsapp - web chat application](https://github.com/darshitlimbad/botsapp/) project which i wanted to make fully native ( okay fine you win... as much as my brain can.. ) i came accross a problem the problem was i had to code whole XML HTTP request code again and again for my backend ( php api's ) requests, That's why decided to create a function which works similer ways like Fetch API does.. and that's how postReq was born :).

It works similer ways to Fetch API at some points but both are fully different and fetch API is more enhanced and advanced in all ways. 

I also learned one thing from this which we all knew but some of us were so busy that we didn't even try to look at it and it was using parameters as a function i mean just think about it we all knew that parameters are not only made for variables right ( atleast in js ) we can use the paramters to initialize a function which we can define while calling the function, If you are familiar with the OOP's concept and Interfaces concepts then you will easily understand what i just did here.

Okay not gonna bore you here is whole Documentation :).

### Parameters

- **`url`:** (String) The URL of the target server-side endpoint. For example, `/functionality/lib/_chat.php`.
- **`data`:** (Object or String) Data to be sent with the request. This is usually JSON-encoded data for POST requests.
- **`options`:** (Object)  An optional object for customizing the request behavior. See table below for available options.

### Options Table

| Option                 | Type        | Description                                                                                        |
|--------------------------|--------------|-----------------------------------------------------------------------------------------------------|
| `method`               | String      | The HTTP method to use (e.g., "POST" by default can accept any other requests also like "GET").          |
| `async`                | Boolean     | Whether the request should be asynchronous (true by default).                                            |
| `Content_Type`          | String      | The content type of the request data (e.g., 'application/json' by default).                              |
| `onUploadProgress`     | Function    | Callback function for progress updates during file uploads. It receives a `Progress` object.        |
| `onDownloadProgress`    | Function    | Callback function for progress updates during file downloads. It receives a `Progress` object.       |
| `onDOwnloadAbortXMLOrNot` | Function    | Callback function to determine if the download should be aborted.                                   |
| `onUploadAbortXMLOrNot`               | Function    | Callback function to determine if the upload should be aborted.                                   |


### Return Value

- **Promise:**  The `postReq` function returns a Promise that resolves with an object containing:
    - **`status`:** (String) "success" for a successful request, "error" for an error, or "abort" for an aborted request.
    - **`responseText`:** (String)  The server's response text. If the response is in JSON format, it is parsed into a JavaScript object.

### Example Usage

```javascript
// Send a POST request to the chat endpoint
postReq('/functionality/lib/_chat.php', JSON.stringify({ req: 'sendMsg', msg: 'Hello!' }))
    .then(response => {
        if (response.status === 'success') {
            console.log('Message sent successfully:', response.responseText);
        } else {
            console.error('Error sending message:', response.error);
        }
    })
    .catch(error => {
        console.error('Error:', error);
    });
```

#### `Progress` Class

### Description

The `Progress` class provides a convenient structure for accessing progress information during file uploads and downloads. It contains information about the amount of data loaded, the total size, and whether the operation is complete.

### Properties

- **`done`:** (Boolean)  Indicates whether the operation is complete (`true`) or not (`false`).
- **`loaded`:** (Number) The amount of data that has been loaded so far.
- **`total`:** (Number) The total size of the data being transferred.
- **`timeStamp`:** (Number) The timestamp of the progress event.

### Example Usage

```javascript
postReq('/functionality/lib/_chat.php', JSON.stringify({ <some action related to file> }) ,
    onUploadProgress = (progress) => {
        let progressPR = document.querySelector(".progressPR");
        progressPR.textContent = Math.ceil(progress.loaded * 100 / progress.total) + "%";
        
        if (progress.done) {
            progressPR.remove();
        }
    }
)
```