# TRPC

### [Error handling](https://trpc.io/docs/server/error-handling)

```typescript
//server
import { TRPCError } from "@trpc/server";

export async function getTuftsPaSummary(
  priorAuth: PriorAuth,
  practitioner: Practitioner,
) {
  if (!condition) {
    throw new TRPCError({
      code: "BAD_REQUEST",
      message: "Prior auth form source not found",
    });
  }
}

//client
    try {
      const htmlContent = await frontendClient.priorAuth.getSummaryInfo.query({
        priorAuthId,
      })
    } catch (err) {
      if (err instanceof TRPCClientError) {
        toast.error(`Failed to copy to clipboard: ${err.message}`);
      } else {
        toast.error("Failed to copy to clipboard");
      }
    }
```

| BAD_REQUEST            | The server cannot or will not process the request due to something that is perceived to be a client error. | 400  |
| ---------------------- | ------------------------------------------------------------ | ---- |
| UNAUTHORIZED           | The client request has not been completed because it lacks valid authentication credentials for the requested resource. | 401  |
| FORBIDDEN              | The server was unauthorized to access a required data source, such as a REST API. | 403  |
| NOT_FOUND              | The server cannot find the requested resource.               | 404  |
| METHOD_NOT_SUPPORTED   | The server knows the request method, but the target resource doesn't support this method. | 405  |
| TIMEOUT                | The server would like to shut down this unused connection.   | 408  |
| CONFLICT               | The server request resource conflict with the current state of the target resource. | 409  |
| PRECONDITION_FAILED    | Access to the target resource has been denied.               | 412  |
| PAYLOAD_TOO_LARGE      | Request entity is larger than limits defined by server.      | 413  |
| UNSUPPORTED_MEDIA_TYPE | The server refuses to accept the request because the payload format is in an unsupported format. | 415  |
| UNPROCESSABLE_CONTENT  | The server understands the request method, and the request entity is correct, but the server was unable to process it. | 422  |
| TOO_MANY_REQUESTS      | The rate limit has been exceeded or too many requests are being sent to the server. | 429  |
| CLIENT_CLOSED_REQUEST  | Access to the resource has been denied.                      | 499  |
| INTERNAL_SERVER_ERROR  | An unspecified error occurred.                               | 500  |
| NOT_IMPLEMENTED        | The server does not support the functionality required to fulfill the request. | 501  |
| BAD_GATEWAY            | The server received an invalid response from the upstream server. | 502  |
| SERVICE_UNAVAILABLE    | The server is not ready to handle the request.               | 503  |
| GATEWAY_TIMEOUT        | The server did not get a response in time from the upstream server that it needed in order to complete the request. | 504  |

