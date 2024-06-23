# UMP API Quickstart

This document describes how to start using the UAS Management Portal (UMP) API, including authorization, authentication,
and accessing API resources. In this section, you'll find a step-by-step guide to quickly start using the API.

## Prerequisites

Before you can start using the API, ensure you have the following in place:

* A valid SIS (Staff Information System) account with appropriate access permissions.
* Your account has to be allowed by your system administrator to use UMP.

## Authentication

To authenticate with the UMP API follow these steps to get your token:

1. Log in to the UMP portal.
2. Navigate to the API settings section.
3. Generate a new API key or token.
4. Copy the token for use in your API requests.

Include the token in your request headers as shown below:

```http
Authorization: Bearer YOUR_ACCESS_TOKEN
```

## Making Your First Request

Here is a simple example of making a GET request to one of the API's endpoints to retrieve UAS data:

```http
GET /api/uas/data HTTP/1.1
Host: api.ump.com
Authorization: Bearer YOUR_ACCESS_TOKEN
```

### Example with cURL

```cURL
curl -X GET "https://api.ump.com/api/uas/data" -H "Authorization: Bearer YOUR_ACCESS_TOKEN"
```

## Response Handling

API responses are returned in JSON format. Here’s an example of handling a response in Python:

```Java
import org.springframework.http.HttpEntity;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpMethod;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

@Service
public class UmpApiService {

    private final String API_URL = "https://api.ump.com/api/uas/data";
    private final String ACCESS_TOKEN = "YOUR_ACCESS_TOKEN";

    public String getUasData() {
        RestTemplate restTemplate = new RestTemplate();

        HttpHeaders headers = new HttpHeaders();
        headers.set("Authorization", "Bearer " + ACCESS_TOKEN);

        HttpEntity<String> entity = new HttpEntity<>(headers);

        ResponseEntity<String> response = restTemplate.exchange(API_URL, HttpMethod.GET, entity, String.class);

        if (response.getStatusCode().is2xxSuccessful()) {
            return response.getBody();
        } else {
            return "Error: " + response.getStatusCodeValue() + ", " + response.getBody();
        }
    }
}

```

## API Usage Tips

- **Rate Limiting**: Be mindful of the rate limits. The standard rate limit is 70 requests per minute.
- **Error Handling**: Always check for error responses and handle them gracefully in your application.
- **Efficient Queries**: Optimize your queries to request only the necessary data to reduce load and improve performance.

## Next Steps

After making your first request, you can:

- Explore additional endpoints in the API documentation.
- Integrate the API into your application to automate UAS data management.
- Use advanced features like filtering and sorting to tailor the data to your needs.

For more detailed information, refer to the full API documentation and explore the various functionalities
offered by the UMP API.