### Servlet
- A servlet is a Java™ technology-based Web component, that generate dynamic content
- Manged by containers
- platform-independent Java classes 
- Loaded dynamically
- run by a Java technology-enabled Web server.
- Containers are Web server extensions that provide servlet functionality.  

Servlets interact with Web clients via a request/response paradigm implemented by the servlet container. 

### Servlet Container
The servlet container is a part of a Web server or application server that **provides the
network services** over which requests and responses are sent, decodes MIME-based
requests, and formats MIME-based responses

A servlet container also **contains and manages servlets through their lifecycle**.

All servlet containers must support HTTP as a protocol for requests and responses

### The Servlet Interface
The two classes in the Java Servlet API that implement the Servlet interface are GenericServlet and HttpServlet. For most purposes,
Developers will extend HttpServlet to implement their servlets.

The basic Servlet interface defines a service method for handling client requests.This method is called for each request that the servlet container routes to an instance
of a servlet.The handling of concurrent requests to a Web application generally requires that the can deal with multiple threads executing within
the service method at a particular time.Generally the Web container handles concurrent requests to the same servlet by concurrent execution
of the service method on different threads.

The HttpServlet abstract subclass adds additional methods beyond the basic Servlet interface that are automatically called by the service method in the
HttpServlet class to aid in processing HTTP-based requests. These methods are:

- doGet for handling HTTP GET requests
- doPost for handling HTTP POST requests
- doPut for handling HTTP PUT requests
- doDelete for handling HTTP DELETE requests

### Servlet Instances
The servlet declaration which is either via the annotation or part of the deployment descriptor of the Web application controls how the servlet container
provides instances of the servlet.

For a servlet not hosted in a distributed environment (the default), the servlet container must use only one instance per servlet declaration.
However,the servlet container may instantiate multiple instances to handle a heavy request load and serialize requests to a particular instance.

if the servlet in a distributable application implements the SingleThreadModel interface, the container may instantiate multiple instances
of that servlet in each JVM of the container.

####  Single Thread Model
The use of the SingleThreadModel interface guarantees that only one thread at a time will execute in a given servlet instance’s service method
It is important to note that this guarantee only applies to each servlet instance, since the container may choose to pool such objects.
Objects that are accessible to more than one servlet instance at a time, such as instances of HttpSession, may be available at any particular
time to multiple servlets, including those that implement SingleThreadModel. 

### Servlet Life Cycle
A servlet is managed through a well defined life cycle that defines how it is loaded
and instantiated, is initialized, handles requests from clients, and is taken out of
service. This life cycle is expressed in the API by the init, service, and destroy
methods of the javax.servlet.Servlet interface

The servlet container is responsible for loading and instantiating servlets. The
loading and instantiation can occur when the container is started, or delayed until
the container determines the servlet is needed to service a request. 

When the servlet engine is started, needed servlet classes must be located by the
servlet container. The servlet container loads the servlet class using normal Java class
loading facilities.

After loading the Servlet class, the container instantiates it for use. 
After the servlet object is instantiated, the container must initialize the servlet before
it can handle requests from clients.

Initialization is provided so that a servlet can read persistent configuration data, initialize
costly resources (such as JDBC™ APIbased connections), and perform other one-time activities.

The container initializes the servlet instance by calling the init method of the Servlet interface with a
unique (per servlet declaration) object implementing the ServletConfig interface.
This configuration object allows the servlet to access name-value initialization
parameters from the Web application’s configuration information.
The configuration object also gives the servlet access to an object (implementing the ServletContext
interface) that describes the servlet’s runtime environment. 

During initialization, the servlet instance can throw an UnavailableException or a
ServletException. In this case, the servlet must not be placed into active service
and must be released by the servlet container. The destroy method is not called as it
is considered unsuccessful initialization.

The triggering of static initialization methods when a tool loads and introspects a
Web application is to be distinguished from the calling of the init method.
Developers should not assume a servlet is in an active container runtime until the
init method of the Servlet interface is called. For example, a servlet should not try
to establish connections to databases or Enterprise JavaBeans™ containers when
only static (class) initialization methods have been invoked.

### Request Handling
After a servlet is properly initialized, the servlet container may use it to handle client
requests. Requests are represented by request objects of type ServletRequest. The
servlet fills out response to requests by calling methods of a provided object of type
ServletResponse. These objects are passed as parameters to the service method of
the Servlet interface.

#### Multithreading Issues



  



