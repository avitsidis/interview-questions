# Web

## Http verbs

* Get
* POST
* PUT
* DELETE
* OPTIONS
* HEAD

## Http status codes

* 1xx: Informational-It means the request has been received and the process is continuing.
* 2xx: Success-It means the action was successfully received, understood, and accepted.
* 3xx: Redirection-It means further action must be taken in order to complete the request.
* 4xx: Client Error-It means the request contains incorrect syntax or cannot be fulfilled
* 5xx: Server Error-It means the server failed to fulfill an apparently valid request.

401 'Unauthorized' should be 401 'Unauthenticated' = please authenticate first
If the request already included Authorization credentials, then the 401 response indicates that authorization has been refused for those credentials.

403 Forbidden = know who you are–I believe who you say you are–but you just don’t have permission to access this resource. Maybe if you ask the system administrator nicely, you’ll get permission. But please don’t bother me again until your predicament changes.

## XSS Cross site scripting

type de faille de sécurité des sites web permettant d'injecter du contenu dans une page, provoquant ainsi des actions sur les navigateurs web visitant la page. Il est par exemple possible de rediriger vers un autre site pour de l'hameçonnage ou encore de voler la session en récupérant les cookies.
Le principe est d'injecter des données arbitraires dans un site web, par exemple en déposant un message dans un forum, ou par des paramètres d'URL. Si ces données arrivent telles quelles dans la page web transmise au navigateur (par les paramètres d'URL, un message posté…) sans avoir été vérifiées, alors il existe une faille : on peut s'en servir pour faire exécuter du code malveillant en langage de script (du JavaScript le plus souvent) par le navigateur web qui consulte cette page.

source: wikipedia

## Long Polling vs SSE vs WebSocket

## JSONP

used to request data from a server residing in a different domain than the client
html:

```html
<script type="application/javascript"
        src="http://server.example.com/Users/1234?callback=parseResponse">
</script>
```

Response:
parseResponse({"Name": "Foo", "Id": 1234, "Rank": 7});

JSONP enables sharing of data bypassing same-origin policy. The policy disallows running JavaScript to read media DOM elements or XHR data fetched from outside the page's origin. The aggregation of the site's scheme, port number and host name identifies as its origin. JSONP is being replaced by CORS.

## CORS : Cross-Origin Resource Sharing

CORS is a mechanism that allows restricted resources (e.g. fonts) on a web page to be requested from another domain outside the domain from which the first resource was served.
CORS can be used as a modern alternative to the JSONP pattern. While JSONP supports only the GET request method, CORS also supports other types of HTTP requests.

### Example

#### Request

HTTP OPTION
Header : `Origin: http://www.example.com`

#### Response

`Access-Control-Allow-Origin : *` : for public resources
Ou
`Access-Control-Allow-Origin: http://www.example.com`
OU
`Error`

## Local storage vs session storage vs cookie

## REST

REST is architectural style.

### Rest level

* Use of verbs
* RESTful URI
* HTTP
* HateOAS
* GraphQL/OData
