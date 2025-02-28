## Spark: a tiny web framework for Java, Kotlin and Groovy

----------------------------------------

# About this fork (unofficial build)

[![](https://img.shields.io/github/actions/workflow/status/intellisrc/spark/ci.yml)](https://github.com/Intellisrc/spark/actions/workflows/ci.yml)
[![](https://img.shields.io/github/issues-pr-closed/intellisrc/spark)](./PR-STATUS.md)
[![](https://img.shields.io/github/license/intellisrc/spark.svg)](./LICENSE)
[![](https://img.shields.io/maven-central/v/com.intellisrc/spark-core.svg)](http://mvnrepository.com/artifact/com.intellisrc/spark-core)

The goal of this fork is to update Spark from the community pull requests and update dependencies until the official repository is back to regular maintenance.

You can see the merge progress in [PR-STATUS](PR-STATUS.md)

## Using it

In order to use this fork version, you need to change your spark dependency.

***NOTE:*** As all classes and packages remain in the same location, you don't need to change your code.

### Maven
```xml
<dependency>
  <groupId>com.intellisrc</groupId>
  <artifactId>spark-core</artifactId>
  <version>2.9.4-unofficial-5</version>
</dependency>
```

### Gradle

```groovy
dependencies {
    implementation 'com.intellisrc:spark-core:2.9.4-unofficial-5'
}
```

## Release 1

These are the patches included in `unofficial-1`:

Bug fixes:
* Method not allowed (Error 405) (perwendel/spark#1234)
* have ": " in request params map (perwendel/spark#1232)
* handling the trailing slash (perwendel/spark#1219)
* change HashMap to ConcurrentHashMap (perwendel/spark#1218 , perwendel/spark#1211, perwendel/spark#1210)

Improvements:
* make route parameter optional (perwendel/spark#1229)
* Improved tests (perwendel/spark#1257 , perwendel/spark#1228 , perwendel/spark#1227)

Security:
* Upgrade Dependencies (perwendel/spark#1239 , perwendel/spark#1232 , perwendel/spark#1215 , perwendel/spark#1207)
* Disable server version response header (perwendel/spark#1214)

## Release 2

These are the patches included in `unofficial-2`:

Bug fixes:
* Initiate the servlet instance in exception mapper (perwendel#1137)

Improvements:
* Added extra information to get server parameters (perwendel/spark#1175)
* ResponseTransformer should have access to Request & Response (perwendel/spark#1174)
* Allow to set default content-type (perwendel#1173)
* Set custom session store (perwendel#1173)
* Allow configuring endpointIdentificationAlgorithm for jetty SSL (perwendel#1153)

## Release 3

These are the patches included in `unofficial-3`:

Bug fixes:
* Fixed GZip content-length problem - Issue: perwendel#1157 (also perwendel#459, perwendel#742 and perwendel#937)

Improvements:
* Added additional mime types (like 'video/mp4') - Issue: perwendel#997
* Allow to override or add mime types (perwendel#997)
* Added `brotli` compression support (additionally to GZip) 
* Regex support in paths 
* HTTP/2 support (perwendel#1183)

## Release 4

These are the patches included in `unofficial-4`:

Bug fixes:
* Fixed optional trailing slash when used with params
* Fixed incorrect response based on acceptType (perwendel#1077) (PR: perwendel/spark#1238)
* Fixed incorrect handling when using invalid methods (perwendel/spark#1236) (PR: perwendel#1204)

Improvements:
* Added unicode support in paths (issue perwendel#1026) (PR: perwendel/spark#1222)

## Release 5

These are the patches included in `unofficial-5`:

Bug fixes:
* NullPointerException in response.header (perwendel/spark/issues/1273)
* Make WebSocketServletContextHandlerFactory.create() not static (perwendel/spark/issues/1208)
* ConcurrentModificationException from spark.route.Routes (perwendel/spark/issues/1243)
* Servlet exception mapper cleanup (perwendel/spark/issues/1213)

Improvements:
* Code updated to Java 11
* Jetty updated to 11
* Added support for multiple calls to `staticFileLocation` and `externalStaticFileLocation` (perwendel/spark/issues/568)

More details and examples on the differences between the Official version and this one: [DIFFERENCES.md](DIFFERENCES.md)

----------------------------------------

# About Spark (official build)

[![](https://img.shields.io/travis/perwendel/spark.svg)](https://travis-ci.org/perwendel/spark)
[![](https://img.shields.io/github/license/perwendel/spark.svg)](./LICENSE)
[![](https://img.shields.io/maven-central/v/com.sparkjava/spark-core.svg)](http://mvnrepository.com/artifact/com.sparkjava/spark-core)

**Spark 2.9.4 is out!!**  <a href="https://github.com/perwendel/spark/blob/master/changeset/2.9.4-changeset.md">Changeset</a> 
```xml
<dependency>
    <groupId>com.sparkjava</groupId>
    <artifactId>spark-core</artifactId>
    <version>2.9.4</version>
</dependency>
```

Sponsor the project here https://github.com/sponsors/perwendel

For documentation please go to: http://sparkjava.com/documentation

For usage questions, please use [stack overflow with the “spark-java” tag](http://stackoverflow.com/questions/tagged/spark-java) 

Javadoc: http://javadoc.io/doc/com.sparkjava/spark-core

When committing to the project please use Spark format configured in https://github.com/perwendel/spark/blob/master/config/spark_formatter_intellij.xml

Getting started
---------------

```xml
<dependency>
    <groupId>com.sparkjava</groupId>
    <artifactId>spark-core</artifactId>
    <version>2.9.4</version>
</dependency>
```

```java
import static spark.Spark.*;

public class HelloWorld {
    public static void main(String[] arg){
        get("/hello", (request, response) -> "Hello World!");
    }
}
```

View at: http://localhost:4567/hello


Check out and try the examples in the source code.
You can also check out the javadoc. After getting the source from
[github](https://github.com/perwendel/spark) run: 

    mvn javadoc:javadoc

The result is put in /target/site/apidocs

Examples
---------

Simple example showing some basic functionality

```java
import static spark.Spark.*;

/**
 * A simple example just showing some basic functionality
 */
public class SimpleExample {

    public static void main(String[] args) {

        //  port(5678); <- Uncomment this if you want spark to listen to port 5678 instead of the default 4567

        get("/hello", (request, response) -> "Hello World!");

        post("/hello", (request, response) ->
            "Hello World: " + request.body()
        );

        get("/private", (request, response) -> {
            response.status(401);
            return "Go Away!!!";
        });

        get("/users/:name", (request, response) -> "Selected user: " + request.params(":name"));

        get("/news/:section", (request, response) -> {
            response.type("text/xml");
            return "<?xml version=\"1.0\" encoding=\"UTF-8\"?><news>" + request.params("section") + "</news>";
        });

        get("/protected", (request, response) -> {
            halt(403, "I don't think so!!!");
            return null;
        });

        get("/redirect", (request, response) -> {
            response.redirect("/news/world");
            return null;
        });

        get("/", (request, response) -> "root");
    }
}

```

-------------------------------

A simple CRUD example showing how to create, get, update and delete book resources

```java
import static spark.Spark.*;

import java.util.HashMap;
import java.util.Map;
import java.util.Random;

/**
 * A simple CRUD example showing how to create, get, update and delete book resources.
 */
public class Books {

    /**
     * Map holding the books
     */
    private static Map<String, Book> books = new HashMap<String, Book>();

    public static void main(String[] args) {
        final Random random = new Random();

        // Creates a new book resource, will return the ID to the created resource
        // author and title are sent in the post body as x-www-urlencoded values e.g. author=Foo&title=Bar
        // you get them by using request.queryParams("valuename")
        post("/books", (request, response) -> {
            String author = request.queryParams("author");
            String title = request.queryParams("title");
            Book book = new Book(author, title);

            int id = random.nextInt(Integer.MAX_VALUE);
            books.put(String.valueOf(id), book);

            response.status(201); // 201 Created
            return id;
        });

        // Gets the book resource for the provided id
        get("/books/:id", (request, response) -> {
            Book book = books.get(request.params(":id"));
            if (book != null) {
                return "Title: " + book.getTitle() + ", Author: " + book.getAuthor();
            } else {
                response.status(404); // 404 Not found
                return "Book not found";
            }
        });

        // Updates the book resource for the provided id with new information
        // author and title are sent in the request body as x-www-urlencoded values e.g. author=Foo&title=Bar
        // you get them by using request.queryParams("valuename")
        put("/books/:id", (request, response) -> {
            String id = request.params(":id");
            Book book = books.get(id);
            if (book != null) {
                String newAuthor = request.queryParams("author");
                String newTitle = request.queryParams("title");
                if (newAuthor != null) {
                    book.setAuthor(newAuthor);
                }
                if (newTitle != null) {
                    book.setTitle(newTitle);
                }
                return "Book with id '" + id + "' updated";
            } else {
                response.status(404); // 404 Not found
                return "Book not found";
            }
        });

        // Deletes the book resource for the provided id
        delete("/books/:id", (request, response) -> {
            String id = request.params(":id");
            Book book = books.remove(id);
            if (book != null) {
                return "Book with id '" + id + "' deleted";
            } else {
                response.status(404); // 404 Not found
                return "Book not found";
            }
        });

        // Gets all available book resources (ids)
        get("/books", (request, response) -> {
            String ids = "";
            for (String id : books.keySet()) {
                ids += id + " ";
            }
            return ids;
        });
    }

    public static class Book {

        public String author, title;

        public Book(String author, String title) {
            this.author = author;
            this.title = title;
        }

        public String getAuthor() {
            return author;
        }

        public void setAuthor(String author) {
            this.author = author;
        }

        public String getTitle() {
            return title;
        }

        public void setTitle(String title) {
            this.title = title;
        }
    }
}
```

---------------------------------

Example showing a very simple (and stupid) authentication filter that is executed before all other resources

```java
import static spark.Spark.*;

import java.util.HashMap;
import java.util.Map;

/**
 * Example showing a very simple (and stupid) authentication filter that is
 * executed before all other resources.
 *
 * When requesting the resource with e.g.
 *     http://localhost:4567/hello?user=some&password=guy
 * the filter will stop the execution and the client will get a 401 UNAUTHORIZED with the content 'You are not welcome here'
 *
 * When requesting the resource with e.g.
 *     http://localhost:4567/hello?user=foo&password=bar
 * the filter will accept the request and the request will continue to the /hello route.
 *
 * Note: There is a second "before filter" that adds a header to the response
 * Note: There is also an "after filter" that adds a header to the response
 */
public class FilterExample {

    private static Map<String, String> usernamePasswords = new HashMap<String, String>();

    public static void main(String[] args) {

        usernamePasswords.put("foo", "bar");
        usernamePasswords.put("admin", "admin");

        before((request, response) -> {
            String user = request.queryParams("user");
            String password = request.queryParams("password");

            String dbPassword = usernamePasswords.get(user);
            if (!(password != null && password.equals(dbPassword))) {
                halt(401, "You are not welcome here!!!");
            }
        });

        before("/hello", (request, response) -> response.header("Foo", "Set by second before filter"));

        get("/hello", (request, response) -> "Hello World!");

        after("/hello", (request, response) -> response.header("spark", "added by after-filter"));

        afterAfter("/hello", (request, response) -> response.header("finally", "executed even if exception is throw"));

        afterAfter((request, response) -> response.header("finally", "executed after any route even if exception is throw"));
    }
}
```

---------------------------------

Example showing how to use attributes

```java
import static spark.Spark.after;
import static spark.Spark.get;

/**
 * Example showing the use of attributes
 */
public class FilterExampleAttributes {

    public static void main(String[] args) {
        get("/hi", (request, response) -> {
            request.attribute("foo", "bar");
            return null;
        });

        after("/hi", (request, response) -> {
            for (String attr : request.attributes()) {
                System.out.println("attr: " + attr);
            }
        });

        after("/hi", (request, response) -> {
            Object foo = request.attribute("foo");
            response.body(asXml("foo", foo));
        });
    }

    private static String asXml(String name, Object value) {
        return "<?xml version=\"1.0\" encoding=\"UTF-8\"?><" + name +">" + value + "</"+ name + ">";
    }
}
```


---------------------------------

Example showing how to serve static resources

```java
import static spark.Spark.*;

public class StaticResources {

    public static void main(String[] args) {

        // Will serve all static file are under "/public" in classpath if the route isn't consumed by others routes.
        // When using Maven, the "/public" folder is assumed to be in "/main/resources"
        staticFileLocation("/public");

        get("/hello", (request, response) -> "Hello World!");
    }
}
```
---------------------------------

Example showing how to define content depending on accept type

```java
import static spark.Spark.*;

public class JsonAcceptTypeExample {

    public static void main(String args[]) {

        //Running curl -i -H "Accept: application/json" http://localhost:4567/hello json message is read.
        //Running curl -i -H "Accept: text/html" http://localhost:4567/hello HTTP 404 error is thrown.
        get("/hello", "application/json", (request, response) -> "{\"message\": \"Hello World\"}");
    }
} 
```
---------------------------------

Example showing how to render a view from a template. Note that we are using `ModelAndView` class for setting the object and name/location of template. 

First of all we define a class which handles and renders output depending on template engine used. In this case [FreeMarker](http://freemarker.incubator.apache.org/).


```java
public class FreeMarkerTemplateEngine extends TemplateEngine {

    private Configuration configuration;

    protected FreeMarkerTemplateEngine() {
        this.configuration = createFreemarkerConfiguration();
    }

    @Override
    public String render(ModelAndView modelAndView) {
        try {
            StringWriter stringWriter = new StringWriter();

            Template template = configuration.getTemplate(modelAndView.getViewName());
            template.process(modelAndView.getModel(), stringWriter);

            return stringWriter.toString();
        } catch (IOException e) {
            throw new IllegalArgumentException(e);
        } catch (TemplateException e) {
            throw new IllegalArgumentException(e);
        }
    }

    private Configuration createFreemarkerConfiguration() {
        Configuration retVal = new Configuration();
        retVal.setClassForTemplateLoading(FreeMarkerTemplateEngine.class, "freemarker");
        return retVal;
    }
}
```

Then we can use it to generate our content. Note how we are setting model data and view name. Because we are using FreeMarker, in this case a `Map` and the name of the template is required:

```java
public class FreeMarkerExample {

    public static void main(String args[]) {

        get("/hello", (request, response) -> {
            Map<String, Object> attributes = new HashMap<>();
            attributes.put("message", "Hello FreeMarker World");

            // The hello.ftl file is located in directory:
            // src/test/resources/spark/examples/templateview/freemarker
            return modelAndView(attributes, "hello.ftl");
        }, new FreeMarkerTemplateEngine());
    }
}
```

---------------------------------

Example of using Transformer.

First of all we define the transformer class, in this case a class which transforms an object to JSON format using gson API.

```java
public class JsonTransformer implements ResponseTransformer {

	private Gson gson = new Gson();

	@Override
	public String render(Object model) {
		return gson.toJson(model);
	}
}
```

And then the code which return a simple POJO to be transformed to JSON:

```java
public class TransformerExample {

    public static void main(String args[]) {
        get("/hello", "application/json", (request, response) -> {
            return new MyMessage("Hello World");
        }, new JsonTransformer());
    }
}
```

Debugging
------------------
See [Spark-debug-tools](https://github.com/perwendel/spark-debug-tools) as a separate module.
