# API List

This document provides a detailed list of all the APIs in the application.

## Router APIs

### Get Routers

*   **Description:** Get a list of routers for a service.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/routers`
*   **Input:**
    *   `query:keyword` (string): The search keyword.
    *   `query:service` (string): The service ID.
*   **Output:**
    *   `routers` (array of `router_dto.Item`): A list of routers.
        *   `id` (string): The router ID.
        *   `methods` (array of string): The HTTP methods.
        *   `protocols` (array of string): The protocols.
        *   `request_path` (string): The request path.
        *   `description` (string): The description.
        *   `disabled` (boolean): Whether the router is disabled.
        *   `creator` (string): The creator's ID.
        *   `updater` (string): The updater's ID.
        *   `create_time` (string): The creation time.
        *   `update_time` (string): The update time.
        *   `can_delete` (boolean): Whether the router can be deleted.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/routers?service=<service_id>&keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/routers?service=<service_id>&keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/routers?service=<service_id>&keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Router Detail

*   **Description:** Get the detail of a router.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/router/detail`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `query:router` (string): The router ID.
*   **Output:**
    *   `router` (`router_dto.Detail`): The router detail.
        *   `id` (string): The router ID.
        *   `name` (string): The router name.
        *   `description` (string): The description.
        *   `methods` (array of string): The HTTP methods.
        *   `path` (string): The request path.
        *   `protocols` (array of string): The protocols.
        *   `match` (array of `router_dto.Match`): The match rules.
            *   `position` (string): The position of the match rule.
            *   `match_type` (string): The type of the match rule.
            *   `key` (string): The key of the match rule.
            *   `pattern` (string): The pattern of the match rule.
        *   `proxy` (`router_dto.Proxy`): The proxy configuration.
            *   `path` (string): The proxy path.
            *   `timeout` (integer): The timeout in milliseconds.
            *   `retry` (integer): The number of retries.
            *   `headers` (array of `router_dto.Header`): The headers to add to the request.
                *   `key` (string): The header key.
                *   `value` (string): The header value.
                *   `opt` (string): The operation.
                *   `optType` (string): The operation type.
            *   `extends` (object): The extends configuration.
            *   `plugins` (object): The plugins configuration.
        *   `disabled` (boolean): Whether the router is disabled.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/router/detail?service=<service_id>&router=<router_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/router/detail?service=<service_id>&router=<router_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/router/detail?service=<service_id>&router=<router_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Create Router

*   **Description:** Create a new router for a service.
*   **Method:** `POST`
*   **Path:** `/api/v1/service/router`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `body` (`router_dto.Create`): The router configuration.
        *   `id` (string): The router ID.
        *   `name` (string): The router name.
        *   `path` (string): The request path.
        *   `methods` (array of string): The HTTP methods.
        *   `description` (string): The description.
        *   `protocols` (array of string): The protocols.
        *   `match` (array of `router_dto.Match`): The match rules.
        *   `upstream` (string): The upstream ID.
        *   `proxy` (`router_dto.InputProxy`): The proxy configuration.
        *   `disabled` (boolean): Whether the router is disabled.
*   **Output:**
    *   `router` (`router_dto.SimpleDetail`): The created router detail.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/service/router?service=<service_id>" -d '{...}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{...}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/router?service=<service_id>")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/service/router?service=<service_id>", strings.NewReader("{...}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Edit Router

*   **Description:** Edit an existing router.
*   **Method:** `PUT`
*   **Path:** `/api/v1/service/router`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `query:router` (string): The router ID.
    *   `body` (`router_dto.Edit`): The router configuration to update.
*   **Output:**
    *   `router` (`router_dto.SimpleDetail`): The updated router detail.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/service/router?service=<service_id>&router=<router_id>" -d '{...}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{...}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/router?service=<service_id>&router=<router_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/service/router?service=<service_id>&router=<router_id>", strings.NewReader("{...}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Delete Router

*   **Description:** Delete a router.
*   **Method:** `DELETE`
*   **Path:** `/api/v1/service/router`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `query:router` (string): The router ID.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X DELETE "/api/v1/service/router?service=<service_id>&router=<router_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/router?service=<service_id>&router=<router_id>")
          .delete()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("DELETE", "http://localhost:8080/api/v1/service/router?service=<service_id>&router=<router_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Router Prefix

*   **Description:** Get the prefix for a service.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/router/define`
*   **Input:**
    *   `query:service` (string): The service ID.
*   **Output:**
    *   `prefix` (string): The prefix.
    *   `force` (boolean): Whether the prefix is forced.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/router/define?service=<service_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/router/define?service=<service_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/router/define?service=<service_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

## API Documentation APIs

### Update API Documentation

*   **Description:** Update the documentation for an API.
*   **Method:** `PUT`
*   **Path:** `/api/v1/service/api_doc`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `body` (`api_doc_dto.UpdateDoc`): The documentation content.
        *   `content` (string): The documentation content in markdown format.
*   **Output:**
    *   `doc` (`api_doc_dto.ApiDocDetail`): The updated API documentation.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/service/api_doc?service=<service_id>" -d '{"content": "..."}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"content\": \"...\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/api_doc?service=<service_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/service/api_doc?service=<service_id>", strings.NewReader("{\"content\": \"...\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get API Documentation

*   **Description:** Get the documentation for an API.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/api_doc`
*   **Input:**
    *   `query:service` (string): The service ID.
*   **Output:**
    *   `doc` (`api_doc_dto.ApiDocDetail`): The API documentation.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/api_doc?service=<service_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/api_doc?service=<service_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/api_doc?service=<service_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Upload API Documentation

*   **Description:** Upload a documentation file for an API.
*   **Method:** `POST`
*   **Path:** `/api/v1/service/api_doc/upload`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `form-data:doc`: The documentation file.
*   **Output:**
    *   `doc` (`api_doc_dto.ApiDocDetail`): The updated API documentation.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/service/api_doc/upload?service=<service_id>" -F "doc=@/path/to/your/doc.md"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("multipart/form-data");
        RequestBody body = new MultipartBody.Builder()
            .setType(MultipartBody.FORM)
            .addFormDataPart("doc", "doc.md",
                RequestBody.create(MediaType.parse("application/octet-stream"),
                new File("/path/to/your/doc.md")))
            .build();
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/api_doc/upload?service=<service_id>")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        package main

        import (
            "bytes"
            "fmt"
            "io"
            "mime/multipart"
            "net/http"
            "os"
        )

        func main() {
            client := &http.Client{}
            body := &bytes.Buffer{}
            writer := multipart.NewWriter(body)
            fw, err := writer.CreateFormFile("doc", "/path/to/your/doc.md")
            if err != nil {
                fmt.Println(err)
                return
            }
            file, err := os.Open("/path/to/your/doc.md")
            if err != nil {
                fmt.Println(err)
                return
            }
            _, err = io.Copy(fw, file)
            if err != nil {
                fmt.Println(err)
                return
            }
            writer.Close()
            req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/service/api_doc/upload?service=<service_id>", bytes.NewReader(body.Bytes()))
            if err != nil {
                fmt.Println(err)
                return
            }
            req.Header.Set("Content-Type", writer.FormDataContentType())
            res, err := client.Do(req)
            if err != nil {
                fmt.Println(err)
                return
            }
            defer res.Body.Close()

            body, err = ioutil.ReadAll(res.Body)
            if err != nil {
                fmt.Println(err)
                return
            }
            fmt.Println(string(body))
        }
        ```

## AI Router APIs

### Get AI Router

*   **Description:** Get an AI router.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/ai-router`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `query:router` (string): The router ID.
*   **Output:**
    *   `api` (object): The AI router detail.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/ai-router?service=<service_id>&router=<router_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/ai-router?service=<service_id>&router=<router_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/ai-router?service=<service_id>&router=<router_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get AI Routers

*   **Description:** Get a list of AI routers for a service.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/ai-routers`
*   **Input:**
    *   `query:keyword` (string): The search keyword.
    *   `query:service` (string): The service ID.
*   **Output:**
    *   `apis` (array of object): A list of AI routers.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/ai-routers?service=<service_id>&keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/ai-routers?service=<service_id>&keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/ai-routers?service=<service_id>&keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Create AI Router

*   **Description:** Create a new AI router for a service.
*   **Method:** `POST`
*   **Path:** `/api/v1/service/ai-router`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `body` (object): The AI router configuration.
*   **Output:**
    *   `api` (object): The created AI router detail.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/service/ai-router?service=<service_id>" -d '{...}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{...}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/ai-router?service=<service_id>")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/service/ai-router?service=<service_id>", strings.NewReader("{...}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Edit AI Router

*   **Description:** Edit an existing AI router.
*   **Method:** `PUT`
*   **Path:** `/api/v1/service/ai-router`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `query:router` (string): The router ID.
    *   `body` (object): The AI router configuration to update.
*   **Output:**
    *   `api` (object): The updated AI router detail.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/service/ai-router?service=<service_id>&router=<router_id>" -d '{...}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{...}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/ai-router?service=<service_id>&router=<router_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/service/ai-router?service=<service_id>&router=<router_id>", strings.NewReader("{...}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Delete AI Router

*   **Description:** Delete an AI router.
*   **Method:** `DELETE`
*   **Path:** `/api/v1/service/ai-router`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `query:router` (string): The router ID.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X DELETE "/api/v1/service/ai-router?service=<service_id>&router=<router_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/ai-router?service=<service_id>&router=<router_id>")
          .delete()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("DELETE", "http://localhost:8080/api/v1/service/ai-router?service=<service_id>&router=<router_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

## Subscribe APIs

### Get Service Subscribers

*   **Description:** Get a list of subscribers for a service.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/subscribers`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `subscribers` (array of `subscribe_dto.Subscriber`): A list of subscribers.
        *   `id` (string): The subscription ID.
        *   `service` (string): The service ID.
        *   `subscriber` (string): The subscriber's service ID.
        *   `team` (string): The team ID.
        *   `apply_time` (string): The apply time.
        *   `applier` (string): The applier's user ID.
        *   `from` (integer): The source of the subscription.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/subscribers?service=<service_id>&keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/subscribers?service=<service_id>&keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/subscribers?service=<service_id>&keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Add Subscriber

*   **Description:** Add a subscriber to a service.
*   **Method:** `POST`
*   **Path:** `/api/v1/service/subscriber`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `body` (`subscribe_dto.AddSubscriber`): The subscriber information.
        *   `application` (string): The application ID.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/service/subscriber?service=<service_id>" -d '{"application": "<application_id>"}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"application\": \"<application_id>\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/subscriber?service=<service_id>")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/service/subscriber?service=<service_id>", strings.NewReader("{\"application\": \"<application_id>\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Delete Subscriber

*   **Description:** Delete a subscriber from a service.
*   **Method:** `DELETE`
*   **Path:** `/api/v1/service/subscriber`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `query:application` (string): The application ID.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X DELETE "/api/v1/service/subscriber?service=<service_id>&application=<application_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/subscriber?service=<service_id>&application=<application_id>")
          .delete()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("DELETE", "http://localhost:8080/api/v1/service/subscriber?service=<service_id>&application=<application_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Application Subscriptions

*   **Description:** Get a list of subscriptions for an application.
*   **Method:** `GET`
*   **Path:** `/api/v1/application/subscriptions`
*   **Input:**
    *   `query:application` (string): The application ID.
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `subscriptions` (array of `subscribe_dto.SubscriptionItem`): A list of subscriptions.
        *   `id` (string): The subscription ID.
        *   `service` (string): The service ID.
        *   `apply_status` (integer): The apply status.
        *   `team` (string): The team ID.
        *   `from` (integer): The source of the subscription.
        *   `create_time` (string): The creation time.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/application/subscriptions?application=<application_id>&keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/application/subscriptions?application=<application_id>&keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/application/subscriptions?application=<application_id>&keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Cancel Subscription

*   **Description:** Cancel a subscription.
*   **Method:** `POST`
*   **Path:** `/api/v1/application/subscription/cancel`
*   **Input:**
    *   `query:application` (string): The application ID.
    *   `query:subscription` (string): The subscription ID.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/application/subscription/cancel?application=<application_id>&subscription=<subscription_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/application/subscription/cancel?application=<application_id>&subscription=<subscription_id>")
          .post(RequestBody.create(null, new byte[0]))
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/application/subscription/cancel?application=<application_id>&subscription=<subscription_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Cancel Subscription Apply

*   **Description:** Cancel a subscription application.
*   **Method:** `POST`
*   **Path:** `/api/v1/application/subscription/cancel_apply`
*   **Input:**
    *   `query:application` (string): The application ID.
    *   `query:subscription` (string): The subscription ID.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/application/subscription/cancel_apply?application=<application_id>&subscription=<subscription_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/application/subscription/cancel_apply?application=<application_id>&subscription=<subscription_id>")
          .post(RequestBody.create(null, new byte[0]))
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/application/subscription/cancel_apply?application=<application_id>&subscription=<subscription_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Approval List

*   **Description:** Get a list of subscription approvals for a service.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/approval/subscribes`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `query:status` (integer): The status of the approvals.
*   **Output:**
    *   `approvals` (array of `subscribe_dto.ApprovalItem`): A list of approvals.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/approval/subscribes?service=<service_id>&status=<status>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/approval/subscribes?service=<service_id>&status=<status>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/approval/subscribes?service=<service_id>&status=<status>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Approval Detail

*   **Description:** Get the detail of a subscription approval.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/approval/subscribe`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `query:apply` (string): The apply ID.
*   **Output:**
    *   `approval` (`subscribe_dto.Approval`): The approval detail.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/approval/subscribe?service=<service_id>&apply=<apply_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/approval/subscribe?service=<service_id>&apply=<apply_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/approval/subscribe?service=<service_id>&apply=<apply_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Approval

*   **Description:** Approve or reject a subscription application.
*   **Method:** `POST`
*   **Path:** `/api/v1/service/approval/subscribe`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `query:apply` (string): The apply ID.
    *   `body` (`subscribe_dto.Approve`): The approval information.
        *   `opinion` (string): The opinion.
        *   `operate` (string): The operation (`pass` or `refuse`).
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/service/approval/subscribe?service=<service_id>&apply=<apply_id>" -d '{"opinion": "...", "operate": "pass"}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"opinion\": \"...\", \"operate\": \"pass\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/approval/subscribe?service=<service_id>&apply=<apply_id>")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/service/approval/subscribe?service=<service_id>&apply=<apply_id>", strings.NewReader("{\"opinion\": \"...\", \"operate\": \"pass\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```
## Certificate APIs

### Get Certificates

*   **Description:** Get a list of certificates.
*   **Method:** `GET`
*   **Path:** `/api/v1/certificates`
*   **Input:** None
*   **Output:**
    *   `certificates` (array of `certificate_dto.Certificate`): A list of certificates.
        *   `id` (string): The certificate ID.
        *   `name` (string): The certificate name.
        *   `domains` (array of string): The domains covered by the certificate.
        *   `partition` (string): The partition of the certificate.
        *   `not_before` (string): The start date of the certificate.
        *   `not_after` (string): The end date of the certificate.
        *   `updater` (string): The updater's user ID.
        *   `update_time` (string): The update time.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/certificates"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/certificates")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/certificates", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Certificate Detail

*   **Description:** Get the detail of a certificate.
*   **Method:** `GET`
*   **Path:** `/api/v1/certificate`
*   **Input:**
    *   `query:id` (string): The certificate ID.
*   **Output:**
    *   `certificate` (`certificate_dto.Certificate`): The certificate detail.
    *   `cert` (`certificate_dto.File`): The certificate file.
        *   `key` (string): The private key.
        *   `pem` (string): The certificate in PEM format.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/certificate?id=<certificate_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/certificate?id=<certificate_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/certificate?id=<certificate_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Create Certificate

*   **Description:** Create a new certificate.
*   **Method:** `POST`
*   **Path:** `/api/v1/certificate`
*   **Input:**
    *   `body` (`certificate_dto.FileInput`): The certificate file.
        *   `key` (string): The private key.
        *   `pem` (string): The certificate in PEM format.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/certificate" -d '{"key": "...", "pem": "..."}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"key\": \"...\", \"pem\": \"...\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/certificate")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/certificate", strings.NewReader("{\"key\": \"...\", \"pem\": \"...\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Update Certificate

*   **Description:** Update an existing certificate.
*   **Method:** `PUT`
*   **Path:** `/api/v1/certificate`
*   **Input:**
    *   `query:id` (string): The certificate ID.
    *   `body` (`certificate_dto.FileInput`): The certificate file.
        *   `key` (string): The private key.
        *   `pem` (string): The certificate in PEM format.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/certificate?id=<certificate_id>" -d '{"key": "...", "pem": "..."}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"key\": \"...\", \"pem\": \"...\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/certificate?id=<certificate_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/certificate?id=<certificate_id>", strings.NewReader("{\"key\": \"...\", \"pem\": \"...\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Delete Certificate

*   **Description:** Delete a certificate.
*   **Method:** `DELETE`
*   **Path:** `/api/v1/certificate`
*   **Input:**
    *   `query:id` (string): The certificate ID.
*   **Output:**
    *   `id` (string): The ID of the deleted certificate.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X DELETE "/api/v1/certificate?id=<certificate_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/certificate?id=<certificate_id>")
          .delete()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("DELETE", "http://localhost:8080/api/v1/certificate?id=<certificate_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```
## Cluster APIs

### Get Cluster Nodes

*   **Description:** Get a list of nodes in a cluster.
*   **Method:** `GET`
*   **Path:** `/api/v1/cluster/nodes`
*   **Input:**
    *   `query:partition` (string): The partition ID.
*   **Output:**
    *   `nodes` (array of `cluster_dto.Node`): A list of nodes.
        *   `id` (string): The node ID.
        *   `name` (string): The node name.
        *   `manager_address` (array of string): The manager addresses.
        *   `peer_address` (array of string): The peer addresses.
        *   `service_address` (array of string): The service addresses.
        *   `status` (integer): The node status.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/cluster/nodes?partition=<partition_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/cluster/nodes?partition=<partition_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/cluster/nodes?partition=<partition_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Reset Cluster

*   **Description:** Reset a cluster.
*   **Method:** `PUT`
*   **Path:** `/api/v1/cluster/reset`
*   **Input:**
    *   `query:partition` (string): The partition ID.
    *   `body` (`cluster_dto.ResetCluster`): The reset information.
        *   `manager_address` (string): The new manager address.
*   **Output:**
    *   `nodes` (array of `cluster_dto.Node`): A list of nodes in the reset cluster.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/cluster/reset?partition=<partition_id>" -d '{"manager_address": "..."}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"manager_address\": \"...\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/cluster/reset?partition=<partition_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/cluster/reset?partition=<partition_id>", strings.NewReader("{\"manager_address\": \"...\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Check Cluster

*   **Description:** Check the status of a cluster.
*   **Method:** `POST`
*   **Path:** `/api/v1/cluster/check`
*   **Input:**
    *   `body` (`cluster_dto.CheckCluster`): The check information.
        *   `address` (string): The address of the cluster to check.
*   **Output:**
    *   `nodes` (array of `cluster_dto.Node`): A list of nodes in the cluster.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/cluster/check" -d '{"address": "..."}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"address\": \"...\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/cluster/check")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/cluster/check", strings.NewReader("{\"address\": \"...\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```
## Team Manager APIs

### Get Team

*   **Description:** Get a team's information.
*   **Method:** `GET`
*   **Path:** `/api/v1/manager/team`
*   **Input:**
    *   `query:id` (string): The team ID.
*   **Output:**
    *   `team` (`team_dto.Team`): The team's information.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/manager/team?id=<team_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/manager/team?id=<team_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/manager/team?id=<team_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Search Teams

*   **Description:** Search for teams.
*   **Method:** `GET`
*   **Path:** `/api/v1/manager/teams`
*   **Input:**
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `teams` (array of `team_dto.Item`): A list of teams.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/manager/teams?keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/manager/teams?keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/manager/teams?keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Create Team

*   **Description:** Create a new team.
*   **Method:** `POST`
*   **Path:** `/api/v1/manager/team`
*   **Input:**
    *   `body` (`team_dto.CreateTeam`): The team's information.
*   **Output:**
    *   `team` (`team_dto.Team`): The created team's information.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/manager/team" -d '{"name": "...", "description": "..."}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"name\": \"...\", \"description\": \"...\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/manager/team")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/manager/team", strings.NewReader("{\"name\": \"...\", \"description\": \"...\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Edit Team

*   **Description:** Edit an existing team.
*   **Method:** `PUT`
*   **Path:** `/api/v1/manager/team`
*   **Input:**
    *   `query:id` (string): The team ID.
    *   `body` (`team_dto.EditTeam`): The team's information to update.
*   **Output:**
    *   `team` (`team_dto.Team`): The updated team's information.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/manager/team?id=<team_id>" -d '{"name": "...", "description": "..."}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"name\": \"...\", \"description\": \"...\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/manager/team?id=<team_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/manager/team?id=<team_id>", strings.NewReader("{\"name\": \"...\", \"description\": \"...\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Delete Team

*   **Description:** Delete a team.
*   **Method:** `DELETE`
*   **Path:** `/api/v1/manager/team`
*   **Input:**
    *   `query:id` (string): The team ID.
*   **Output:**
    *   `id` (string): The ID of the deleted team.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X DELETE "/api/v1/manager/team?id=<team_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/manager/team?id=<team_id>")
          .delete()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("DELETE", "http://localhost:8080/api/v1/manager/team?id=<team_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```
## My Team APIs

### Get Team

*   **Description:** Get a team's information.
*   **Method:** `GET`
*   **Path:** `/api/v1/team`
*   **Input:**
    *   `query:team` (string): The team ID.
*   **Output:**
    *   `team` (`team_dto.Team`): The team's information.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/team?team=<team_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/team?team=<team_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/team?team=<team_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Search Teams

*   **Description:** Search for teams.
*   **Method:** `GET`
*   **Path:** `/api/v1/teams`
*   **Input:**
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `teams` (array of `team_dto.Item`): A list of teams.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/teams?keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/teams?keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/teams?keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get My Simple Teams

*   **Description:** Get a simplified list of my teams.
*   **Method:** `GET`
*   **Path:** `/api/v1/simple/teams/mine`
*   **Input:**
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `teams` (array of `team_dto.SimpleTeam`): A list of simple teams.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/simple/teams/mine?keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/simple/teams/mine?keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/simple/teams/mine?keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Simple Teams

*   **Description:** Get a simplified list of all teams.
*   **Method:** `GET`
*   **Path:** `/api/v1/simple/teams`
*   **Input:**
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `teams` (array of `team_dto.SimpleTeam`): A list of simple teams.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/simple/teams?keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/simple/teams?keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/simple/teams?keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Simple Members

*   **Description:** Get a simplified list of team members.
*   **Method:** `GET`
*   **Path:** `/api/v1/team/members/simple`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `teams` (array of `team_dto.SimpleMember`): A list of simple members.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/team/members/simple?team=<team_id>&keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/team/members/simple?team=<team_id>&keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/team/members/simple?team=<team_id>&keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Edit Team

*   **Description:** Edit an existing team.
*   **Method:** `PUT`
*   **Path:** `/api/v1/team`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `body` (`team_dto.EditTeam`): The team's information to update.
*   **Output:**
    *   `team` (`team_dto.Team`): The updated team's information.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/team?team=<team_id>" -d '{"name": "...", "description": "..."}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"name\": \"...\", \"description\": \"...\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/team?team=<team_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/team?team=<team_id>", strings.NewReader("{\"name\": \"...\", \"description\": \"...\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Add Member

*   **Description:** Add a member to a team.
*   **Method:** `POST`
*   **Path:** `/api/v1/team/member`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `body` (`team_dto.UserIDs`): The user IDs to add.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/team/member?team=<team_id>" -d '{"users": ["..."]}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"users\": [\"...\"]}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/team/member?team=<team_id>")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/team/member?team=<team_id>", strings.NewReader("{\"users\": [\"...\"]}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Remove Member

*   **Description:** Remove a member from a team.
*   **Method:** `DELETE`
*   **Path:** `/api/v1/team/member`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `query:user` (string): The user ID to remove.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X DELETE "/api/v1/team/member?team=<team_id>&user=<user_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/team/member?team=<team_id>&user=<user_id>")
          .delete()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("DELETE", "http://localhost:8080/api/v1/team/member?team=<team_id>&user=<user_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Members

*   **Description:** Get a list of team members.
*   **Method:** `GET`
*   **Path:** `/api/v1/team/members`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `members` (array of `team_dto.Member`): A list of members.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/team/members?team=<team_id>&keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/team/members?team=<team_id>&keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/team/members?team=<team_id>&keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Update Member Role

*   **Description:** Update the role of a team member.
*   **Method:** `PUT`
*   **Path:** `/api/v1/team/member/role`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `body` (`team_dto.UpdateMemberRole`): The user IDs and roles to update.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/team/member/role?team=<team_id>" -d '{"users": ["..."], "roles": ["..."]}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"users\": [\"...\"], \"roles\": [\"...\"]}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/team/member/role?team=<team_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/team/member/role?team=<team_id>", strings.NewReader("{\"users\": [\"...\"], \"roles\": [\"...\"]}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Team Services

*   **Description:** Get a list of services for a team.
*   **Method:** `GET`
*   **Path:** `/api/v1/team/services`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `services` (array of object): A list of services.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/team/services?team=<team_id>&keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/team/services?team=<team_id>&keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/team/services?team=<team_id>&keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Create Team Service

*   **Description:** Create a new service for a team.
*   **Method:** `POST`
*   **Path:** `/api/v1/team/service`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `body` (object): The service information.
*   **Output:**
    *   `service` (object): The created service information.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/team/service?team=<team_id>" -d '{...}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{...}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/team/service?team=<team_id>")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/team/service?team=<team_id>", strings.NewReader("{...}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Create Team App

*   **Description:** Create a new app for a team.
*   **Method:** `POST`
*   **Path:** `/api/v1/team/app`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `body` (object): The app information.
*   **Output:**
    *   `app` (object): The created app information.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/team/app?team=<team_id>" -d '{...}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{...}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/team/app?team=<team_id>")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/team/app?team=<team_id>", strings.NewReader("{...}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Delete Team Service

*   **Description:** Delete a service from a team.
*   **Method:** `DELETE`
*   **Path:** `/api/v1/team/service`
*   **Input:**
    *   `query:service` (string): The service ID.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X DELETE "/api/v1/team/service?service=<service_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/team/service?service=<service_id>")
          .delete()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("DELETE", "http://localhost:8080/api/v1/team/service?service=<service_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```
## Service APIs

### Get Service Info

*   **Description:** Get a service's information.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/info`
*   **Input:**
    *   `query:service` (string): The service ID.
*   **Output:**
    *   `service` (`service_dto.Service`): The service's information.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/info?service=<service_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/info?service=<service_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/info?service=<service_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Edit Service

*   **Description:** Edit an existing service.
*   **Method:** `PUT`
*   **Path:** `/api/v1/service/info`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `body` (`service_dto.EditService`): The service's information to update.
*   **Output:**
    *   `service` (`service_dto.Service`): The updated service's information.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/service/info?service=<service_id>" -d '{...}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{...}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/info?service=<service_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/service/info?service=<service_id>", strings.NewReader("{...}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Delete Service

*   **Description:** Delete a service.
*   **Method:** `DELETE`
*   **Path:** `/api/v1/service/info`
*   **Input:**
    *   `query:service` (string): The service ID.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X DELETE "/api/v1/service/info?service=<service_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/info?service=<service_id>")
          .delete()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("DELETE", "http://localhost:8080/api/v1/service/info?service=<service_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get My Services

*   **Description:** Get a list of my services.
*   **Method:** `GET`
*   **Path:** `/api/v1/my_services`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `services` (array of `service_dto.ServiceItem`): A list of services.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/my_services?team=<team_id>&keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/my_services?team=<team_id>&keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/my_services?team=<team_id>&keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Search Services

*   **Description:** Search for services.
*   **Method:** `GET`
*   **Path:** `/api/v1/services`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `services` (array of `service_dto.ServiceItem`): A list of services.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/services?team=<team_id>&keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/services?team=<team_id>&keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/services?team=<team_id>&keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Simple Services

*   **Description:** Get a simplified list of all services.
*   **Method:** `GET`
*   **Path:** `/api/v1/simple/services`
*   **Input:** None
*   **Output:**
    *   `services` (array of `service_dto.SimpleServiceItem`): A list of simple services.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/simple/services"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/simple/services")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/simple/services", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get My Simple Services

*   **Description:** Get a simplified list of my services.
*   **Method:** `GET`
*   **Path:** `/api/v1/simple/services/mine`
*   **Input:** None
*   **Output:**
    *   `services` (array of `service_dto.SimpleServiceItem`): A list of simple services.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/simple/services/mine"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/simple/services/mine")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/simple/services/mine", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Quick Create RESTful Service

*   **Description:** Quickly create a new RESTful service.
*   **Method:** `POST`
*   **Path:** `/api/v1/quick/service/rest`
*   **Input:** None
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/quick/service/rest"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/quick/service/rest")
          .post(RequestBody.create(null, new byte[0]))
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/quick/service/rest", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Quick Create AI Service

*   **Description:** Quickly create a new AI service.
*   **Method:** `POST`
*   **Path:** `/api/v1/quick/service/ai`
*   **Input:**
    *   `body` (`service_dto.QuickCreateAIService`): The AI service's information.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/quick/service/ai" -d '{...}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{...}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/quick/service/ai")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/quick/service/ai", strings.NewReader("{...}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get App Info

*   **Description:** Get an app's information.
*   **Method:** `GET`
*   **Path:** `/api/v1/app/info`
*   **Input:**
    *   `query:app` (string): The app ID.
*   **Output:**
    *   `app` (`service_dto.App`): The app's information.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/app/info?app=<app_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/app/info?app=<app_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/app/info?app=<app_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Delete App

*   **Description:** Delete an app.
*   **Method:** `DELETE`
*   **Path:** `/api/v1/app`
*   **Input:**
    *   `query:app` (string): The app ID.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X DELETE "/api/v1/app?app=<app_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/app?app=<app_id>")
          .delete()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("DELETE", "http://localhost:8080/api/v1/app?app=<app_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Simple Apps

*   **Description:** Get a simplified list of all apps.
*   **Method:** `GET`
*   **Path:** `/api/v1/simple/apps`
*   **Input:**
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `apps` (array of `service_dto.SimpleAppItem`): A list of simple apps.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/simple/apps?keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/simple/apps?keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/simple/apps?keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get My Simple Apps

*   **Description:** Get a simplified list of my apps.
*   **Method:** `GET`
*   **Path:** `/api/v1/simple/apps/mine`
*   **Input:**
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `apps` (array of `service_dto.SimpleAppItem`): A list of simple apps.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/simple/apps/mine?keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/simple/apps/mine?keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/simple/apps/mine?keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get My Apps

*   **Description:** Get a list of my apps.
*   **Method:** `GET`
*   **Path:** `/api/v1/my_apps`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `apps` (array of `service_dto.AppItem`): A list of apps.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/my_apps?team=<team_id>&keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/my_apps?team=<team_id>&keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/my_apps?team=<team_id>&keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Search Apps

*   **Description:** Search for apps.
*   **Method:** `GET`
*   **Path:** `/api/v1/apps`
*   **Input:**
    *   `query:team` (string): The team ID.
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `apps` (array of `service_dto.AppItem`): A list of apps.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/apps?team=<team_id>&keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/apps?team=<team_id>&keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/apps?team=<team_id>&keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Search Can Subscribe Apps

*   **Description:** Search for apps that can subscribe to a service.
*   **Method:** `GET`
*   **Path:** `/api/v1/apps/can_subscribe`
*   **Input:**
    *   `query:service` (string): The service ID.
*   **Output:**
    *   `app` (array of `service_dto.SubscribeAppItem`): A list of apps.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/apps/can_subscribe?service=<service_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/apps/can_subscribe?service=<service_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/apps/can_subscribe?service=<service_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Update App Info

*   **Description:** Update an app's information.
*   **Method:** `PUT`
*   **Path:** `/api/v1/app/info`
*   **Input:**
    *   `query:app` (string): The app ID.
    *   `body` (`service_dto.UpdateApp`): The app's information to update.
*   **Output:**
    *   `app` (`service_dto.App`): The updated app's information.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/app/info?app=<app_id>" -d '{...}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{...}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/app/info?app=<app_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/app/info?app=<app_id>", strings.NewReader("{...}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Service Doc

*   **Description:** Get a service's documentation.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/doc`
*   **Input:**
    *   `query:service` (string): The service ID.
*   **Output:**
    *   `doc` (`service_dto.ServiceDoc`): The service's documentation.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/doc?service=<service_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/doc?service=<service_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/doc?service=<service_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Save Service Doc

*   **Description:** Save a service's documentation.
*   **Method:** `PUT`
*   **Path:** `/api/v1/service/doc`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `body` (`service_dto.SaveServiceDoc`): The service's documentation to save.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/service/doc?service=<service_id>" -d '{"doc": "..."}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"doc\": \"...\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/doc?service=<service_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/service/doc?service=<service_id>", strings.NewReader("{\"doc\": \"...\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```
## Catalogue APIs

### Search Catalogues

*   **Description:** Search for catalogues and tags.
*   **Method:** `GET`
*   **Path:** `/api/v1/catalogues`
*   **Input:**
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `catalogues` (array of `catalogue_dto.Item`): A list of catalogues.
    *   `tags` (array of `tag_dto.Item`): A list of tags.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/catalogues?keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/catalogues?keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/catalogues?keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Create Catalogue

*   **Description:** Create a new catalogue.
*   **Method:** `POST`
*   **Path:** `/api/v1/catalogue`
*   **Input:**
    *   `body` (`catalogue_dto.CreateCatalogue`): The catalogue's information.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/catalogue" -d '{"name": "...", "parent": "..."}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"name\": \"...\", \"parent\": \"...\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/catalogue")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/catalogue", strings.NewReader("{\"name\": \"...\", \"parent\": \"...\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Edit Catalogue

*   **Description:** Edit an existing catalogue.
*   **Method:** `PUT`
*   **Path:** `/api/v1/catalogue`
*   **Input:**
    *   `query:catalogue` (string): The catalogue ID.
    *   `body` (`catalogue_dto.EditCatalogue`): The catalogue's information to update.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/catalogue?catalogue=<catalogue_id>" -d '{"name": "...", "parent": "..."}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"name\": \"...\", \"parent\": \"...\"}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/catalogue?catalogue=<catalogue_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/catalogue?catalogue=<catalogue_id>", strings.NewReader("{\"name\": \"...\", \"parent\": \"...\"}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Delete Catalogue

*   **Description:** Delete a catalogue.
*   **Method:** `DELETE`
*   **Path:** `/api/v1/catalogue`
*   **Input:**
    *   `query:catalogue` (string): The catalogue ID.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X DELETE "/api/v1/catalogue?catalogue=<catalogue_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/catalogue?catalogue=<catalogue_id>")
          .delete()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("DELETE", "http://localhost:8080/api/v1/catalogue?catalogue=<catalogue_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Sort Catalogue

*   **Description:** Sort the catalogues.
*   **Method:** `PUT`
*   **Path:** `/api/v1/catalogue/sort`
*   **Input:**
    *   `body` (array of `catalogue_dto.SortItem`): The sort information.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/catalogue/sort" -d '[{"id": "...", "children": [...]}]'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "[{\"id\": \"...\", \"children\": [...]}]");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/catalogue/sort")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/catalogue/sort", strings.NewReader("[{\"id\": \"...\", \"children\": [...]}]"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Catalogue Services

*   **Description:** Get a list of services in a catalogue.
*   **Method:** `GET`
*   **Path:** `/api/v1/catalogue/services`
*   **Input:**
    *   `query:keyword` (string): The search keyword.
*   **Output:**
    *   `services` (array of `catalogue_dto.ServiceItem`): A list of services.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/catalogue/services?keyword=<keyword>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/catalogue/services?keyword=<keyword>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/catalogue/services?keyword=<keyword>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Get Catalogue Service Detail

*   **Description:** Get the detail of a service in a catalogue.
*   **Method:** `GET`
*   **Path:** `/api/v1/catalogue/service`
*   **Input:**
    *   `query:service` (string): The service ID.
*   **Output:**
    *   `service` (`catalogue_dto.ServiceDetail`): The service's detail.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/catalogue/service?service=<service_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/catalogue/service?service=<service_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/catalogue/service?service=<service_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Subscribe Service

*   **Description:** Subscribe to a service.
*   **Method:** `POST`
*   **Path:** `/api/v1/catalogue/service/subscribe`
*   **Input:**
    *   `body` (`catalogue_dto.SubscribeService`): The subscription information.
*   **Output:** None
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X POST "/api/v1/catalogue/service/subscribe" -d '{"service": "...", "applications": ["..."]}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{\"service\": \"...\", \"applications\": [\"...\"]}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/catalogue/service/subscribe")
          .post(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("POST", "http://localhost:8080/api/v1/catalogue/service/subscribe", strings.NewReader("{\"service\": \"...\", \"applications\": [\"...\"]}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```
## Upstream APIs

### Get Upstream

*   **Description:** Get the upstream configuration for a service.
*   **Method:** `GET`
*   **Path:** `/api/v1/service/upstream`
*   **Input:**
    *   `query:service` (string): The service ID.
*   **Output:**
    *   `upstream` (`upstream_dto.UpstreamConfig`): The upstream configuration.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X GET "/api/v1/service/upstream?service=<service_id>"
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();

        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/upstream?service=<service_id>")
          .get()
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("GET", "http://localhost:8080/api/v1/service/upstream?service=<service_id>", nil)
        if err != nil {
            fmt.Println(err)
            return
        }
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```

### Save Upstream

*   **Description:** Save the upstream configuration for a service.
*   **Method:** `PUT`
*   **Path:** `/api/v1/service/upstream`
*   **Input:**
    *   `query:service` (string): The service ID.
    *   `body` (`upstream_dto.Upstream`): The upstream configuration to save.
*   **Output:**
    *   `upstream` (`upstream_dto.UpstreamConfig`): The saved upstream configuration.
*   **Sample Call:**
    *   **cURL**
        ```bash
        curl -X PUT "/api/v1/service/upstream?service=<service_id>" -d '{...}'
        ```
    *   **Java**
        ```java
        OkHttpClient client = new OkHttpClient();
        MediaType mediaType = MediaType.parse("application/json");
        RequestBody body = RequestBody.create(mediaType, "{...}");
        Request request = new Request.Builder()
          .url("http://localhost:8080/api/v1/service/upstream?service=<service_id>")
          .put(body)
          .build();

        Response response = client.newCall(request).execute();
        ```
    *   **Go**
        ```go
        client := &http.Client{}
        req, err := http.NewRequest("PUT", "http://localhost:8080/api/v1/service/upstream?service=<service_id>", strings.NewReader("{...}"))
        if err != nil {
            fmt.Println(err)
            return
        }
        req.Header.Add("Content-Type", "application/json")
        res, err := client.Do(req)
        if err != nil {
            fmt.Println(err)
            return
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            fmt.Println(err)
            return
        }
        fmt.Println(string(body))
        ```
I have now documented all the APIs. I will mark this step as complete.
