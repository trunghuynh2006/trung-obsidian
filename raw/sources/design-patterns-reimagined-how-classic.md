[![](https://blogger.googleusercontent.com/img/a/AVvXsEjoT5lUQolvjcdjjAR1oiiEn7-O68thr3JFh7Pf5CAkKwGKnkbYG7u3HhdOGDP_WryVUKuo3RRklJK9OHO0BFcfw3zJJoUmZ6ZoPF-QrbZ-Xn5DsUH-MNIzMHC9PwBzWmR7Y5GdHyew79hQHZs7T10bl-nE-Eg6lnrqJHIfwjOkfrD2dV7nPM3lVw=w267-h400)](https://blogger.googleusercontent.com/img/a/AVvXsEjoT5lUQolvjcdjjAR1oiiEn7-O68thr3JFh7Pf5CAkKwGKnkbYG7u3HhdOGDP_WryVUKuo3RRklJK9OHO0BFcfw3zJJoUmZ6ZoPF-QrbZ-Xn5DsUH-MNIzMHC9PwBzWmR7Y5GdHyew79hQHZs7T10bl-nE-Eg6lnrqJHIfwjOkfrD2dV7nPM3lVw)

## INTRODUCTION

When the Gang of Four published their seminal work "Design Patterns: Elements of Reusable Object-Oriented Software" in 1994, they crystallized decades of object-oriented programming wisdom into twenty-three patterns that would influence software development for generations. Shortly thereafter, the Pattern-Oriented Software Architecture series began with its first volume in 1996, expanding the pattern catalog to include architectural and concurrent system patterns. These books were written in an era when C++ and Smalltalk dominated, when desktop applications were the norm, and when distributed computing meant CORBA and RPC calls over local networks. The computing landscape of that time bore little resemblance to the world we inhabit today.

The intervening three decades have witnessed a transformation in software development that the original pattern authors could scarcely have imagined. Cloud computing has moved from a novel concept to the default deployment model. Microservices architectures have replaced monolithic applications. Functional programming concepts have permeated mainstream languages. Containerization and orchestration platforms manage applications at scales that would have seemed impossible in the 1990s. Modern languages like Rust, Go, Kotlin, and TypeScript incorporate features that make certain patterns obsolete while demanding entirely new patterns for problems that did not exist thirty years ago. Concurrency has moved from a specialized concern to a fundamental requirement, with multi-core processors in every device and distributed systems as the architectural norm rather than the exception.

If we were to rewrite these classic pattern books today, the catalog would look dramatically different. Some patterns would disappear entirely, recognized now as solutions to problems that no longer exist or as anti-patterns that create more problems than they solve. Other patterns would undergo significant transformation, their core intent preserved but their implementation and structure adapted to modern paradigms. Most significantly, a host of new patterns would emerge, addressing the challenges of distributed systems, reactive programming, cloud-native architectures, and the demands of building resilient systems at scale. This article explores how the pattern catalog would evolve, examining which patterns would be removed, which would be transformed, and which new patterns would take their place in a modern treatment of software design.

## PATTERNS THAT WOULD DISAPPEAR

The **Singleton pattern** was perhaps the most widely used pattern from the original Gang of Four catalog, and it would be one of the first to be removed from a modern edition. The Singleton ensures that a class has only one instance and provides a global point of access to it. In the 1990s, this seemed like an elegant solution for managing shared resources like configuration objects, logging facilities, or connection pools. However, modern software development has recognized the Singleton as an anti-pattern that introduces global state, makes testing difficult, violates the single responsibility principle, and creates hidden dependencies between components.

The fundamental problem with Singleton is that it combines two responsibilities that should be separate. First, it enforces that only one instance exists. Second, it provides global access to that instance. The global access creates tight coupling throughout the codebase, making it nearly impossible to substitute alternative implementations for testing. The enforcement of a single instance is often unnecessary or can be better handled by dependency injection frameworks. Consider a typical Singleton implementation from the classic pattern:

public class DatabaseConnection {

private static DatabaseConnection instance;

private Connection connection;

private DatabaseConnection() {

// Private constructor prevents instantiation

this.connection = createConnection();

}

public static DatabaseConnection getInstance() {

if (instance == null) {

instance = new DatabaseConnection();

}

return instance;

}

public void executeQuery(String query) {

// Execute query using the connection

}

}

This implementation creates numerous problems. Any code that calls DatabaseConnection.getInstance() has a hidden dependency that is not visible in its constructor or method signatures. Testing becomes difficult because you cannot easily substitute a mock implementation. The lazy initialization shown here is not thread-safe, and making it thread-safe adds complexity. The global state makes it difficult to reason about the program's behavior, especially in concurrent scenarios.

Modern applications handle this scenario through dependency injection and inversion of control containers. Instead of classes obtaining their dependencies through static methods, dependencies are explicitly declared and injected. This makes dependencies visible, enables easy substitution for testing, and allows the container to manage the lifecycle and scope of objects. Here is how the same scenario would be handled in a modern application:

public class DatabaseConnection {

private final Connection connection;

// Dependencies are injected through the constructor

public DatabaseConnection(ConnectionConfig config) {

this.connection = createConnection(config);

}

public void executeQuery(String query) {

// Execute query using the connection

}

}

public class OrderService {

private final DatabaseConnection database;

// The service receives its dependency explicitly

public OrderService(DatabaseConnection database) {

this.database = database;

}

public void processOrder(Order order) {

database.executeQuery("INSERT INTO orders...");

}

}

The dependency injection container manages the lifecycle and ensures that only one instance of DatabaseConnection exists if that is the desired scope. The key difference is that this is a configuration concern handled by the container, not a structural concern baked into the class itself. Testing becomes straightforward because you can pass a mock DatabaseConnection to OrderService. The dependencies are explicit and visible in the constructor signature.

The **Abstract Factory pattern** would also be removed from a modern pattern catalog. This pattern provides an interface for creating families of related objects without specifying their concrete classes. In the original formulation, Abstract Factory addressed the problem of creating objects that must work together and ensuring that the created objects are compatible. A classic example involved creating UI components that must all belong to the same look-and-feel family, such as Windows or Macintosh widgets.

The pattern involved multiple levels of abstraction with abstract factory interfaces, concrete factory implementations, abstract product interfaces, and concrete product implementations. This created a complex hierarchy that was difficult to understand and maintain. Modern approaches handle this problem more elegantly through dependency injection, configuration, and simpler factory methods. The full Abstract Factory machinery is rarely justified in contemporary codebases.

Consider a simplified version of the classic Abstract Factory for creating UI components:

public interface GUIFactory {

Button createButton();

Checkbox createCheckbox();

}

public class WindowsFactory implements GUIFactory {

public Button createButton() {

return new WindowsButton();

}

public Checkbox createCheckbox() {

return new WindowsCheckbox();

}

}

public class MacFactory implements GUIFactory {

public Button createButton() {

return new MacButton();

}

public Checkbox createCheckbox() {

return new MacCheckbox();

}

}

Modern applications would handle this through configuration and dependency injection without the elaborate factory hierarchy. The framework or container would be configured to use the appropriate implementations, and components would receive their dependencies through injection. The complexity of maintaining parallel factory hierarchies is avoided.

The **Flyweight pattern** would be significantly de-emphasized or removed from a modern catalog. Flyweight was designed to minimize memory usage by sharing data among similar objects. In an era when memory was measured in megabytes and every byte counted, this pattern made sense for applications that needed to create large numbers of similar objects, such as characters in a text editor or trees in a graphical scene.

Modern computing environments have abundant memory, and premature optimization is recognized as a significant source of unnecessary complexity. The Flyweight pattern adds considerable complexity to the codebase by requiring careful separation of intrinsic and extrinsic state, managing shared object pools, and coordinating access to shared objects. In most modern applications, this complexity is not justified by the memory savings. When memory optimization is truly necessary, modern languages and frameworks provide better mechanisms such as string interning, object pooling libraries, and memory-efficient data structures.

The **Interpreter pattern** would also be removed or drastically reduced in scope. This pattern defines a representation for a grammar and an interpreter for sentences in that language. The classic implementation involved creating a class hierarchy representing grammar rules and implementing an interpret method on each class. While this worked for very simple languages, it quickly became unwieldy for anything more complex.

Modern software development has much better tools for language implementation. Parser generators like ANTLR can automatically generate efficient parsers from grammar specifications. Domain-specific language frameworks provide sophisticated tools for creating and interpreting languages. For simple expression evaluation, libraries and built-in language features handle the task more efficiently than hand-coded interpreter patterns. The complexity and maintenance burden of the classic Interpreter pattern is rarely justified when superior alternatives exist.

## PATTERNS THAT WOULD TRANSFORM

The **Observer pattern** would undergo significant transformation in a modern pattern catalog, evolving from its original form into event-driven architectures, reactive streams, and publish-subscribe systems. The original Observer pattern defined a one-to-many dependency between objects so that when one object changed state, all its dependents were notified automatically. This was typically implemented with subjects maintaining lists of observers and calling their update methods when changes occurred.

The fundamental concept remains valuable, but the implementation and scope have expanded dramatically. Modern applications deal with asynchronous events, backpressure, error handling, and distributed event streams. The simple synchronous notification mechanism of the original pattern is insufficient for these requirements. Contemporary implementations use reactive programming libraries, event buses, message queues, and publish-subscribe systems that provide much richer functionality.

Here is a classic Observer implementation showing the traditional approach:

public interface Observer {

void update(String message);

}

public class Subject {

private List<Observer> observers = new ArrayList<>();

private String state;

public void attach(Observer observer) {

observers.add(observer);

}

public void detach(Observer observer) {

observers.remove(observer);

}

public void setState(String state) {

this.state = state;

notifyObservers();

}

private void notifyObservers() {

for (Observer observer: observers) {

observer.update(state);

}

}

}

public class ConcreteObserver implements Observer {

private String name;

public ConcreteObserver(String name) {

this.name = name;

}

public void update(String message) {

System.out.println(name + " received: " + message);

}

}

This implementation has several limitations. Notifications are synchronous, blocking the subject until all observers complete. There is no error handling if an observer throws an exception. There is no mechanism for backpressure if observers cannot keep up with notifications. Memory leaks can occur if observers are not properly detached. The pattern does not scale to distributed systems where observers might be in different processes or on different machines.

Modern implementations use reactive streams that address these limitations. Reactive streams provide asynchronous, non-blocking event handling with backpressure support. They include sophisticated operators for transforming, filtering, and combining event streams. Error handling is built into the stream semantics. Here is how the same scenario would be implemented using reactive streams:

import io.reactivex.rxjava3.core.Observable;

import io.reactivex.rxjava3.subjects.PublishSubject;

public class ReactiveSubject {

// PublishSubject acts as both Observable and Observer

private PublishSubject<String> subject = PublishSubject.create();

// Expose the observable interface for subscribers

public Observable<String> getObservable() {

return subject;

}

// Publish events to all subscribers

public void setState(String state) {

subject.onNext(state);

}

// Signal completion

public void complete() {

subject.onComplete();

}

// Signal error

public void error(Throwable throwable) {

subject.onError(throwable);

}

}

public class ReactiveExample {

public void demonstrateReactiveObserver() {

ReactiveSubject subject = new ReactiveSubject();

// Subscribe with automatic resource management

subject.getObservable()

.filter(msg -> msg.length() > 5) // Only long messages

.map(String::toUpperCase) // Transform to uppercase

.subscribe(

message -> System.out.println("Observer 1: " + message),

error -> System.err.println("Error: " + error),

() -> System.out.println("Completed")

);

// Second subscriber with different processing

subject.getObservable()

.debounce(100, TimeUnit.MILLISECONDS) // Rate limiting

.subscribe(message -> System.out.println("Observer 2: " + message));

// Publish events asynchronously

subject.setState("hello");

subject.setState("world");

subject.setState("reactive programming");

}

}

This reactive implementation provides asynchronous event delivery, built-in error handling, completion semantics, and powerful operators for stream transformation. Subscribers can apply backpressure if they cannot keep up with events. The framework handles thread safety and resource management. This represents a significant evolution from the simple Observer pattern while preserving its core intent of decoupling event sources from event consumers.

In distributed systems, the Observer pattern transforms further into publish-subscribe messaging systems. Events are published to message brokers like Apache Kafka, RabbitMQ, or cloud-based services like AWS SNS/SQS. Subscribers can be in different processes, different machines, or different data centers. The message broker handles delivery guarantees, persistence, and scaling. This distributed form of the Observer pattern is fundamental to modern microservices architectures.

The **Command pattern** would transform into **Command Query Responsibility Segregation**, commonly known as CQRS. The original **Command pattern** encapsulated a request as an object, allowing you to parameterize clients with different requests, queue requests, log requests, and support undoable operations. The pattern involved creating command objects with an execute method, and often included support for undo through an additional method.

CQRS takes the core concept of representing operations as objects and extends it to separate the read and write models of an application. In modern systems, the requirements for reading data are often very different from the requirements for writing data. Reads need to be fast, may require denormalized views, and often have different scaling characteristics. Writes need to ensure consistency, may involve complex business logic, and often occur less frequently than reads.

The classic Command pattern looked like this:

public interface Command {

void execute();

void undo();

}

public class TransferMoneyCommand implements Command {

private Account source;

private Account destination;

private double amount;

private boolean executed = false;

public TransferMoneyCommand(Account source, Account destination, double amount) {

this.source = source;

this.destination = destination;

this.amount = amount;

}

public void execute() {

source.withdraw(amount);

destination.deposit(amount);

executed = true;

}

public void undo() {

if (executed) {

destination.withdraw(amount);

source.deposit(amount);

executed = false;

}

}

}

Modern CQRS implementations separate commands that modify state from queries that read state. Commands are processed through a command handler that validates the command, applies business rules, and updates the write model. Queries are processed through a separate query handler that reads from optimized read models. The read and write models may use different data stores, different schemas, and different scaling strategies.

Here is a modern CQRS implementation showing the separation of commands and queries:

// Command side - represents an intent to change state

public class TransferMoneyCommand {

private final String sourceAccountId;

private final String destinationAccountId;

private final BigDecimal amount;

private final String transactionId;

public TransferMoneyCommand(String sourceAccountId,

String destinationAccountId,

BigDecimal amount) {

this.sourceAccountId = sourceAccountId;

this.destinationAccountId = destinationAccountId;

this.amount = amount;

this.transactionId = UUID.randomUUID().toString();

}

// Getters omitted for brevity

}

// Command handler - processes commands and updates write model

public class TransferMoneyCommandHandler {

private final AccountRepository accountRepository;

private final EventPublisher eventPublisher;

public TransferMoneyCommandHandler(AccountRepository accountRepository,

EventPublisher eventPublisher) {

this.accountRepository = accountRepository;

this.eventPublisher = eventPublisher;

}

public CommandResult handle(TransferMoneyCommand command) {

// Load aggregates from write model

Account source = accountRepository.findById(command.getSourceAccountId());

Account destination = accountRepository.findById(command.getDestinationAccountId());

// Validate business rules

if (source.getBalance().compareTo(command.getAmount()) < 0) {

return CommandResult.failure("Insufficient funds");

}

// Execute the transfer

source.withdraw(command.getAmount());

destination.deposit(command.getAmount());

// Persist changes

accountRepository.save(source);

accountRepository.save(destination);

// Publish event for read model updates

eventPublisher.publish(new MoneyTransferredEvent(

command.getTransactionId(),

command.getSourceAccountId(),

command.getDestinationAccountId(),

command.getAmount(),

Instant.now()

));

return CommandResult.success(command.getTransactionId());

}

}

// Query side - represents a request for data

public class GetAccountBalanceQuery {

private final String accountId;

public GetAccountBalanceQuery(String accountId) {

this.accountId = accountId;

}

public String getAccountId() {

return accountId;

}

}

// Query handler - reads from optimized read model

public class GetAccountBalanceQueryHandler {

private final AccountReadModelRepository readRepository;

public GetAccountBalanceQueryHandler(AccountReadModelRepository readRepository) {

this.readRepository = readRepository;

}

public AccountBalanceDTO handle(GetAccountBalanceQuery query) {

// Read from denormalized, optimized read model

AccountReadModel account = readRepository.findById(query.getAccountId());

return new AccountBalanceDTO(

account.getAccountId(),

account.getBalance(),

account.getCurrency(),

account.getLastTransactionDate()

);

}

}

This CQRS implementation separates the concerns of writing and reading data. The command handler focuses on validating business rules and maintaining consistency in the write model. The query handler focuses on efficiently retrieving data from a read model that may be denormalized and optimized for specific query patterns. Events published by the command side update the read models asynchronously, allowing the read and write sides to scale independently.

The **Strategy pattern** would transform significantly in modern implementations, moving away from class hierarchies toward functional approaches using higher-order functions and lambda expressions. The original Strategy pattern defined a family of algorithms, encapsulated each one, and made them interchangeable. This allowed the algorithm to vary independently from clients that use it. The classic implementation involved creating a strategy interface and multiple concrete strategy classes.

Modern languages with first-class functions make the Strategy pattern much simpler. Instead of creating separate classes for each strategy, you can pass functions directly. This reduces boilerplate code and makes the intent clearer. The pattern becomes less about object-oriented design and more about functional composition.

Here is the classic Strategy pattern implementation:

public interface PaymentStrategy {

void pay(double amount);

}

public class CreditCardStrategy implements PaymentStrategy {

private String cardNumber;

private String cvv;

public CreditCardStrategy(String cardNumber, String cvv) {

this.cardNumber = cardNumber;

this.cvv = cvv;

}

public void pay(double amount) {

System.out.println("Paid " + amount + " using credit card " + cardNumber);

}

}

public class PayPalStrategy implements PaymentStrategy {

private String email;

public PayPalStrategy(String email) {

this.email = email;

}

public void pay(double amount) {

System.out.println("Paid " + amount + " using PayPal account " + email);

}

}

public class ShoppingCart {

private PaymentStrategy paymentStrategy;

public void setPaymentStrategy(PaymentStrategy strategy) {

this.paymentStrategy = strategy;

}

public void checkout(double amount) {

paymentStrategy.pay(amount);

}

}

Modern implementations use functional interfaces and lambda expressions to eliminate the need for separate strategy classes:

import java.util.function.BiConsumer;

public class ModernShoppingCart {

// Strategy is now a function type

private BiConsumer<PaymentDetails, Double> paymentStrategy;

public void setPaymentStrategy(BiConsumer<PaymentDetails, Double> strategy) {

this.paymentStrategy = strategy;

}

public void checkout(PaymentDetails details, double amount) {

paymentStrategy.accept(details, amount);

}

}

public class PaymentDetails {

private String identifier;

private String credential;

public PaymentDetails(String identifier, String credential) {

this.identifier = identifier;

this.credential = credential;

}

public String getIdentifier() { return identifier; }

public String getCredential() { return credential; }

}

public class PaymentStrategies {

// Strategies are now static methods that can be passed as method references

public static void payCreditCard(PaymentDetails details, double amount) {

System.out.println("Paid " + amount + " using credit card " +

details.getIdentifier());

}

public static void payPayPal(PaymentDetails details, double amount) {

System.out.println("Paid " + amount + " using PayPal account " +

details.getIdentifier());

}

public static void payCryptocurrency(PaymentDetails details, double amount) {

System.out.println("Paid " + amount + " using crypto wallet " +

details.getIdentifier());

}

}

public class PaymentExample {

public void demonstrateModernStrategy() {

ModernShoppingCart cart = new ModernShoppingCart();

// Use method reference as strategy

cart.setPaymentStrategy(PaymentStrategies::payCreditCard);

cart.checkout(new PaymentDetails("1234-5678", "123"), 99.99);

// Use lambda expression as strategy

cart.setPaymentStrategy((details, amount) -> {

System.out.println("Paid " + amount + " using bank transfer to " +

details.getIdentifier());

});

cart.checkout(new PaymentDetails("IBAN123", ""), 150.00);

// Compose strategies

BiConsumer<PaymentDetails, Double> loggingStrategy =

(details, amount) -> System.out.println("Processing payment of " + amount);

BiConsumer<PaymentDetails, Double> actualPayment =

PaymentStrategies::payPayPal;

cart.setPaymentStrategy(loggingStrategy.andThen(actualPayment));

cart.checkout(new PaymentDetails("user@example.com", ""), 75.50);

}

}

This modern approach eliminates the need for separate strategy classes while preserving the ability to vary algorithms independently. Strategies can be defined inline as lambdas, passed as method references, or composed from multiple functions. The code is more concise and the intent is clearer. This represents a fundamental shift from object-oriented to functional approaches for this pattern.

The **Proxy pattern** would transform into multiple specialized patterns for modern distributed systems. The original Proxy pattern provided a surrogate or placeholder for another object to control access to it. The classic pattern had several variants including remote proxies for objects in different address spaces, virtual proxies for lazy initialization, and protection proxies for access control.

In modern systems, the Proxy pattern has evolved into **API gateways**, **service meshes**, and **distributed proxy patterns**. These modern incarnations handle concerns like service discovery, load balancing, circuit breaking, authentication, rate limiting, and observability. The simple forwarding proxy of the original pattern has grown into sophisticated infrastructure components.

An API gateway acts as a proxy for microservices, providing a single entry point for clients and handling cross-cutting concerns. Here is a simplified example of a modern API gateway proxy:

public class APIGatewayProxy {

private final ServiceRegistry serviceRegistry;

private final CircuitBreakerRegistry circuitBreakerRegistry;

private final RateLimiter rateLimiter;

private final AuthenticationService authService;

private final MetricsCollector metrics;

public APIGatewayProxy(ServiceRegistry serviceRegistry,

CircuitBreakerRegistry circuitBreakerRegistry,

RateLimiter rateLimiter,

AuthenticationService authService,

MetricsCollector metrics) {

this.serviceRegistry = serviceRegistry;

this.circuitBreakerRegistry = circuitBreakerRegistry;

this.rateLimiter = rateLimiter;

this.authService = authService;

this.metrics = metrics;

}

public Response handleRequest(Request request) {

long startTime = System.currentTimeMillis();

try {

// Authentication and authorization

User user = authService.authenticate(request.getAuthToken());

if (!authService.authorize(user, request.getPath())) {

return Response.forbidden("Access denied");

}

// Rate limiting

if (!rateLimiter.allowRequest(user.getId())) {

return Response.tooManyRequests("Rate limit exceeded");

}

// Service discovery

String serviceName = extractServiceName(request.getPath());

ServiceInstance service = serviceRegistry.getInstance(serviceName);

if (service == null) {

return Response.serviceUnavailable("Service not found");

}

// Circuit breaker protection

CircuitBreaker circuitBreaker =

circuitBreakerRegistry.getCircuitBreaker(serviceName);

if (circuitBreaker.isOpen()) {

return Response.serviceUnavailable("Service temporarily unavailable");

}

// Forward request to actual service

Response response = forwardRequest(service, request);

// Record success

circuitBreaker.recordSuccess();

metrics.recordRequest(serviceName, response.getStatusCode(),

System.currentTimeMillis() - startTime);

return response;

} catch (Exception e) {

// Record failure

String serviceName = extractServiceName(request.getPath());

circuitBreakerRegistry.getCircuitBreaker(serviceName).recordFailure();

metrics.recordError(serviceName, e);

return Response.internalServerError("Request failed");

}

}

private Response forwardRequest(ServiceInstance service, Request request) {

// Transform request, add headers, forward to service

HttpClient client = HttpClient.newHttpClient();

HttpRequest httpRequest = HttpRequest.newBuilder()

.uri(URI.create(service.getUrl() + request.getPath()))

.header("X-Forwarded-For", request.getClientIp())

.header("X-Request-ID", UUID.randomUUID().toString())

.method(request.getMethod(), request.getBodyPublisher())

.build();

try {

HttpResponse<String> httpResponse =

client.send(httpRequest, HttpResponse.BodyHandlers.ofString());

return new Response(httpResponse.statusCode(), httpResponse.body());

} catch (Exception e) {

throw new RuntimeException("Failed to forward request", e);

}

}

private String extractServiceName(String path) {

// Extract service name from path like /api/users/123

String\[\] parts = path.split("/");

return parts.length > 2? parts\[2\]: null;

}

}

This modern proxy implementation handles authentication, rate limiting, service discovery, circuit breaking, and metrics collection. It acts as a sophisticated intermediary that provides much more functionality than simple forwarding. The pattern has evolved from a structural design pattern into an architectural component that is essential for managing distributed systems.

## NEW PATTERNS FOR DISTRIBUTED SYSTEMS

The **Circuit Breaker pattern** would be a prominent addition to a modern pattern catalog. This pattern prevents an application from repeatedly trying to execute an operation that is likely to fail, allowing it to continue without waiting for the fault to be fixed or wasting resources on operations that are doomed to fail. The pattern is essential for building resilient distributed systems where remote calls can fail due to network issues, service overload, or service failures.

The Circuit Breaker pattern operates like an electrical circuit breaker. It has three states: closed, open, and half-open. In the closed state, requests pass through normally and failures are counted. When failures exceed a threshold, the circuit breaker trips to the open state, immediately failing all requests without attempting the operation. After a timeout period, the circuit breaker enters the half-open state, allowing a limited number of test requests through. If these succeed, the circuit breaker resets to closed. If they fail, it returns to open.

The constituents of the Circuit Breaker pattern include the circuit breaker itself, which maintains state and makes decisions about whether to allow operations; the protected operation, which is the potentially failing operation being guarded; failure detection logic, which determines what constitutes a failure; and state transition logic, which manages movement between states based on success and failure counts.

Here is a comprehensive implementation of the Circuit Breaker pattern:

import java.time.Duration;

import java.time.Instant;

import java.util.concurrent.atomic.AtomicInteger;

import java.util.concurrent.atomic.AtomicReference;

import java.util.function.Supplier;

public class CircuitBreaker {

private enum State {

CLOSED, // Normal operation, requests pass through

OPEN, // Failing fast, requests immediately rejected

HALF\_OPEN // Testing if service recovered

}

private final int failureThreshold;

private final int successThreshold;

private final Duration timeout;

private final AtomicInteger failureCount;

private final AtomicInteger successCount;

private final AtomicReference<State> state;

private final AtomicReference<Instant> lastFailureTime;

public CircuitBreaker(int failureThreshold,

int successThreshold,

Duration timeout) {

this.failureThreshold = failureThreshold;

this.successThreshold = successThreshold;

this.timeout = timeout;

this.failureCount = new AtomicInteger(0);

this.successCount = new AtomicInteger(0);

this.state = new AtomicReference<>(State.CLOSED);

this.lastFailureTime = new AtomicReference<>(Instant.now());

}

public <T> T execute(Supplier<T> operation) throws CircuitBreakerOpenException {

State currentState = state.get();

// Check if we should transition from OPEN to HALF\_OPEN

if (currentState == State.OPEN) {

if (Duration.between(lastFailureTime.get(), Instant.now())

.compareTo(timeout) > 0) {

// Timeout elapsed, try half-open

state.compareAndSet(State.OPEN, State.HALF\_OPEN);

successCount.set(0);

currentState = State.HALF\_OPEN;

} else {

// Still in timeout period, fail fast

throw new CircuitBreakerOpenException(

"Circuit breaker is OPEN, failing fast");

}

}

try {

// Attempt the operation

T result = operation.get();

// Operation succeeded

onSuccess(currentState);

return result;

} catch (Exception e) {

// Operation failed

onFailure(currentState);

throw e;

}

}

private void onSuccess(State currentState) {

if (currentState == State.HALF\_OPEN) {

// Count successes in half-open state

int successes = successCount.incrementAndGet();

if (successes >= successThreshold) {

// Enough successes, close the circuit

state.set(State.CLOSED);

failureCount.set(0);

successCount.set(0);

}

} else if (currentState == State.CLOSED) {

// Reset failure count on success in closed state

failureCount.set(0);

}

}

private void onFailure(State currentState) {

lastFailureTime.set(Instant.now());

if (currentState == State.HALF\_OPEN) {

// Any failure in half-open state reopens the circuit

state.set(State.OPEN);

successCount.set(0);

} else if (currentState == State.CLOSED) {

// Count failures in closed state

int failures = failureCount.incrementAndGet();

if (failures >= failureThreshold) {

// Too many failures, open the circuit

state.set(State.OPEN);

}

}

}

public boolean isOpen() {

return state.get() == State.OPEN;

}

public State getState() {

return state.get();

}

public void reset() {

state.set(State.CLOSED);

failureCount.set(0);

successCount.set(0);

}

}

public class CircuitBreakerOpenException extends RuntimeException {

public CircuitBreakerOpenException(String message) {

super(message);

}

}

// Example usage with a remote service call

public class PaymentService {

private final CircuitBreaker circuitBreaker;

private final HttpClient httpClient;

public PaymentService() {

// Open circuit after 5 failures, require 2 successes to close,

// wait 30 seconds before trying again

this.circuitBreaker = new CircuitBreaker(5, 2, Duration.ofSeconds(30));

this.httpClient = HttpClient.newHttpClient();

}

public PaymentResult processPayment(PaymentRequest request) {

try {

return circuitBreaker.execute(() -> {

// This is the protected operation that might fail

return callPaymentGateway(request);

});

} catch (CircuitBreakerOpenException e) {

// Circuit is open, return cached response or error

return PaymentResult.temporarilyUnavailable(

"Payment service is temporarily unavailable");

} catch (Exception e) {

// Actual failure from the operation

return PaymentResult.failed("Payment processing failed: " +

e.getMessage());

}

}

private PaymentResult callPaymentGateway(PaymentRequest request) {

// Simulate calling external payment gateway

HttpRequest httpRequest = HttpRequest.newBuilder()

.uri(URI.create("https://payment-gateway.example.com/process"))

.header("Content-Type", "application/json")

.POST(HttpRequest.BodyPublishers.ofString(request.toJson()))

.timeout(Duration.ofSeconds(5))

.build();

try {

HttpResponse<String> response =

httpClient.send(httpRequest, HttpResponse.BodyHandlers.ofString());

if (response.statusCode() == 200) {

return PaymentResult.success(response.body());

} else {

throw new RuntimeException("Payment gateway returned status " +

response.statusCode());

}

} catch (Exception e) {

throw new RuntimeException("Failed to call payment gateway", e);

}

}

}

This Circuit Breaker implementation provides automatic failure detection and recovery. When the payment gateway starts failing, the circuit breaker opens after five failures, preventing further attempts and allowing the system to fail fast. After thirty seconds, it enters half-open state to test if the service has recovered. If two consecutive requests succeed, the circuit closes and normal operation resumes. This prevents cascading failures and allows the system to recover gracefully from transient issues.

The **Saga pattern** would be another essential addition to a modern pattern catalog. This pattern manages distributed transactions across multiple services in a microservices architecture. Traditional ACID transactions do not work well in distributed systems because they require locking resources across services, which reduces availability and creates tight coupling. The Saga pattern breaks a distributed transaction into a series of local transactions, each updating a single service. If one transaction fails, the saga executes compensating transactions to undo the changes made by previous steps.

There are two main coordination approaches for sagas: choreography and orchestration. In choreography, each service produces and listens to events, and services coordinate themselves without a central controller. In orchestration, a central saga orchestrator tells services what operations to perform. Orchestration is generally easier to understand and monitor, while choreography provides better decoupling.

The constituents of the Saga pattern include the saga coordinator, which manages the overall transaction flow; local transactions, which are the individual steps that modify a single service; compensating transactions, which undo the effects of completed steps when the saga fails; and a saga log, which records the progress of the saga to enable recovery from failures.

Here is an implementation of the Saga pattern using orchestration for an order processing scenario:

import java.util.ArrayList;

import java.util.List;

import java.util.UUID;

// Saga step interface

public interface SagaStep {

String getName();

void execute(SagaContext context) throws Exception;

void compensate(SagaContext context);

}

// Context shared across saga steps

public class SagaContext {

private final String sagaId;

private final Map<String, Object> data;

public SagaContext() {

this.sagaId = UUID.randomUUID().toString();

this.data = new ConcurrentHashMap<>();

}

public String getSagaId() {

return sagaId;

}

public void put(String key, Object value) {

data.put(key, value);

}

public Object get(String key) {

return data.get(key);

}

}

// Saga orchestrator

public class SagaOrchestrator {

private final List<SagaStep> steps;

private final SagaLog sagaLog;

public SagaOrchestrator(SagaLog sagaLog) {

this.steps = new ArrayList<>();

this.sagaLog = sagaLog;

}

public void addStep(SagaStep step) {

steps.add(step);

}

public SagaResult execute(SagaContext context) {

List<SagaStep> completedSteps = new ArrayList<>();

sagaLog.logSagaStarted(context.getSagaId());

try {

// Execute each step in sequence

for (SagaStep step: steps) {

sagaLog.logStepStarted(context.getSagaId(), step.getName());

try {

step.execute(context);

completedSteps.add(step);

sagaLog.logStepCompleted(context.getSagaId(), step.getName());

} catch (Exception e) {

sagaLog.logStepFailed(context.getSagaId(), step.getName(), e);

// Step failed, compensate all completed steps

compensate(context, completedSteps);

return SagaResult.failed(

"Saga failed at step " + step.getName() + ": " + e.getMessage());

}

}

sagaLog.logSagaCompleted(context.getSagaId());

return SagaResult.success();

} catch (Exception e) {

sagaLog.logSagaFailed(context.getSagaId(), e);

return SagaResult.failed("Saga failed: " + e.getMessage());

}

}

private void compensate(SagaContext context, List<SagaStep> completedSteps) {

// Execute compensating transactions in reverse order

for (int i = completedSteps.size() - 1; i >= 0; i--) {

SagaStep step = completedSteps.get(i);

sagaLog.logCompensationStarted(context.getSagaId(), step.getName());

try {

step.compensate(context);

sagaLog.logCompensationCompleted(context.getSagaId(), step.getName());

} catch (Exception e) {

// Compensation failed, log and continue with other compensations

sagaLog.logCompensationFailed(context.getSagaId(), step.getName(), e);

}

}

}

}

// Example saga steps for order processing

public class ReserveInventoryStep implements SagaStep {

private final InventoryService inventoryService;

public ReserveInventoryStep(InventoryService inventoryService) {

this.inventoryService = inventoryService;

}

public String getName() {

return "ReserveInventory";

}

public void execute(SagaContext context) throws Exception {

String orderId = (String) context.get("orderId");

List<OrderItem> items = (List<OrderItem>) context.get("items");

// Reserve inventory for the order

String reservationId = inventoryService.reserveItems(items);

context.put("reservationId", reservationId);

}

public void compensate(SagaContext context) {

String reservationId = (String) context.get("reservationId");

if (reservationId!= null) {

// Release the reserved inventory

inventoryService.releaseReservation(reservationId);

}

}

}

public class ProcessPaymentStep implements SagaStep {

private final PaymentService paymentService;

public ProcessPaymentStep(PaymentService paymentService) {

this.paymentService = paymentService;

}

public String getName() {

return "ProcessPayment";

}

public void execute(SagaContext context) throws Exception {

String orderId = (String) context.get("orderId");

BigDecimal amount = (BigDecimal) context.get("amount");

String customerId = (String) context.get("customerId");

// Process payment

String paymentId = paymentService.processPayment(customerId, amount);

context.put("paymentId", paymentId);

}

public void compensate(SagaContext context) {

String paymentId = (String) context.get("paymentId");

if (paymentId!= null) {

// Refund the payment

paymentService.refundPayment(paymentId);

}

}

}

public class CreateShipmentStep implements SagaStep {

private final ShippingService shippingService;

public CreateShipmentStep(ShippingService shippingService) {

this.shippingService = shippingService;

}

public String getName() {

return "CreateShipment";

}

public void execute(SagaContext context) throws Exception {

String orderId = (String) context.get("orderId");

Address address = (Address) context.get("shippingAddress");

List<OrderItem> items = (List<OrderItem>) context.get("items");

// Create shipment

String shipmentId = shippingService.createShipment(orderId, address, items);

context.put("shipmentId", shipmentId);

}

public void compensate(SagaContext context) {

String shipmentId = (String) context.get("shipmentId");

if (shipmentId!= null) {

// Cancel the shipment

shippingService.cancelShipment(shipmentId);

}

}

}

// Usage example

public class OrderProcessingSaga {

private final SagaOrchestrator orchestrator;

public OrderProcessingSaga(InventoryService inventoryService,

PaymentService paymentService,

ShippingService shippingService,

SagaLog sagaLog) {

this.orchestrator = new SagaOrchestrator(sagaLog);

// Define the saga steps in order

orchestrator.addStep(new ReserveInventoryStep(inventoryService));

orchestrator.addStep(new ProcessPaymentStep(paymentService));

orchestrator.addStep(new CreateShipmentStep(shippingService));

}

public SagaResult processOrder(Order order) {

SagaContext context = new SagaContext();

context.put("orderId", order.getId());

context.put("customerId", order.getCustomerId());

context.put("items", order.getItems());

context.put("amount", order.getTotalAmount());

context.put("shippingAddress", order.getShippingAddress());

return orchestrator.execute(context);

}

}

This Saga implementation coordinates a distributed transaction across three services: inventory, payment, and shipping. If any step fails, the orchestrator automatically executes compensating transactions to undo the completed steps. For example, if payment processing fails after inventory has been reserved, the saga releases the inventory reservation. This ensures consistency across services without requiring distributed locks or two-phase commit protocols.

The **Event Sourcing pattern** would be another critical addition to a modern pattern catalog. Instead of storing just the current state of entities, Event Sourcing stores the sequence of events that led to the current state. Every change to application state is captured as an event object, and these events are stored in an append-only log. The current state can be reconstructed by replaying the events from the beginning.

Event Sourcing provides several benefits. It creates a complete audit trail of all changes, enabling temporal queries to see what the state was at any point in time. It enables event replay for debugging and testing. It naturally supports event-driven architectures where other components can subscribe to events. It can improve performance by avoiding complex joins and allowing optimized read models.

The constituents of Event Sourcing include events, which are immutable records of state changes; the event store, which persists events in append-only fashion; aggregates, which are entities that produce events in response to commands; event handlers, which update read models in response to events; and projections, which are read models built from event streams.

Here is an implementation of Event Sourcing for a bank account:

import java.math.BigDecimal;

import java.time.Instant;

import java.util.ArrayList;

import java.util.List;

import java.util.UUID;

// Base event class

public abstract class Event {

private final String eventId;

private final String aggregateId;

private final Instant timestamp;

private final long version;

public Event(String aggregateId, long version) {

this.eventId = UUID.randomUUID().toString();

this.aggregateId = aggregateId;

this.timestamp = Instant.now();

this.version = version;

}

public String getEventId() { return eventId; }

public String getAggregateId() { return aggregateId; }

public Instant getTimestamp() { return timestamp; }

public long getVersion() { return version; }

}

// Domain events

public class AccountOpenedEvent extends Event {

private final String accountNumber;

private final String customerId;

private final BigDecimal initialBalance;

public AccountOpenedEvent(String aggregateId, long version,

String accountNumber, String customerId,

BigDecimal initialBalance) {

super(aggregateId, version);

this.accountNumber = accountNumber;

this.customerId = customerId;

this.initialBalance = initialBalance;

}

public String getAccountNumber() { return accountNumber; }

public String getCustomerId() { return customerId; }

public BigDecimal getInitialBalance() { return initialBalance; }

}

public class MoneyDepositedEvent extends Event {

private final BigDecimal amount;

private final String description;

public MoneyDepositedEvent(String aggregateId, long version,

BigDecimal amount, String description) {

super(aggregateId, version);

this.amount = amount;

this.description = description;

}

public BigDecimal getAmount() { return amount; }

public String getDescription() { return description; }

}

public class MoneyWithdrawnEvent extends Event {

private final BigDecimal amount;

private final String description;

public MoneyWithdrawnEvent(String aggregateId, long version,

BigDecimal amount, String description) {

super(aggregateId, version);

this.amount = amount;

this.description = description;

}

public BigDecimal getAmount() { return amount; }

public String getDescription() { return description; }

}

// Aggregate that produces events

public class BankAccount {

private String accountId;

private String accountNumber;

private String customerId;

private BigDecimal balance;

private long version;

private List<Event> uncommittedEvents;

public BankAccount() {

this.uncommittedEvents = new ArrayList<>();

this.version = 0;

}

// Command: Open a new account

public static BankAccount openAccount(String accountNumber,

String customerId,

BigDecimal initialBalance) {

if (initialBalance.compareTo(BigDecimal.ZERO) < 0) {

throw new IllegalArgumentException("Initial balance cannot be negative");

}

BankAccount account = new BankAccount();

account.applyEvent(new AccountOpenedEvent(

UUID.randomUUID().toString(),

0,

accountNumber,

customerId,

initialBalance

));

return account;

}

// Command: Deposit money

public void deposit(BigDecimal amount, String description) {

if (amount.compareTo(BigDecimal.ZERO) <= 0) {

throw new IllegalArgumentException("Deposit amount must be positive");

}

applyEvent(new MoneyDepositedEvent(

accountId,

version + 1,

amount,

description

));

}

// Command: Withdraw money

public void withdraw(BigDecimal amount, String description) {

if (amount.compareTo(BigDecimal.ZERO) <= 0) {

throw new IllegalArgumentException("Withdrawal amount must be positive");

}

if (balance.compareTo(amount) < 0) {

throw new IllegalArgumentException("Insufficient funds");

}

applyEvent(new MoneyWithdrawnEvent(

accountId,

version + 1,

amount,

description

));

}

// Apply event and update state

private void applyEvent(Event event) {

// Update state based on event

if (event instanceof AccountOpenedEvent) {

AccountOpenedEvent e = (AccountOpenedEvent) event;

this.accountId = e.getAggregateId();

this.accountNumber = e.getAccountNumber();

this.customerId = e.getCustomerId();

this.balance = e.getInitialBalance();

} else if (event instanceof MoneyDepositedEvent) {

MoneyDepositedEvent e = (MoneyDepositedEvent) event;

this.balance = this.balance.add(e.getAmount());

} else if (event instanceof MoneyWithdrawnEvent) {

MoneyWithdrawnEvent e = (MoneyWithdrawnEvent) event;

this.balance = this.balance.subtract(e.getAmount());

}

this.version = event.getVersion();

this.uncommittedEvents.add(event);

}

// Reconstruct state from events

public static BankAccount fromEvents(List<Event> events) {

BankAccount account = new BankAccount();

for (Event event: events) {

account.applyEventFromHistory(event);

}

return account;

}

private void applyEventFromHistory(Event event) {

// Same as applyEvent but doesn't add to uncommittedEvents

if (event instanceof AccountOpenedEvent) {

AccountOpenedEvent e = (AccountOpenedEvent) event;

this.accountId = e.getAggregateId();

this.accountNumber = e.getAccountNumber();

this.customerId = e.getCustomerId();

this.balance = e.getInitialBalance();

} else if (event instanceof MoneyDepositedEvent) {

MoneyDepositedEvent e = (MoneyDepositedEvent) event;

this.balance = this.balance.add(e.getAmount());

} else if (event instanceof MoneyWithdrawnEvent) {

MoneyWithdrawnEvent e = (MoneyWithdrawnEvent) event;

this.balance = this.balance.subtract(e.getAmount());

}

this.version = event.getVersion();

}

public List<Event> getUncommittedEvents() {

return new ArrayList<>(uncommittedEvents);

}

public void markEventsAsCommitted() {

uncommittedEvents.clear();

}

public BigDecimal getBalance() { return balance; }

public String getAccountId() { return accountId; }

public long getVersion() { return version; }

}

// Event store interface

public interface EventStore {

void saveEvents(String aggregateId, List<Event> events, long expectedVersion);

List<Event> getEvents(String aggregateId);

List<Event> getEventsSince(String aggregateId, long version);

}

// Repository using event sourcing

public class BankAccountRepository {

private final EventStore eventStore;

public BankAccountRepository(EventStore eventStore) {

this.eventStore = eventStore;

}

public void save(BankAccount account) {

List<Event> uncommittedEvents = account.getUncommittedEvents();

if (!uncommittedEvents.isEmpty()) {

eventStore.saveEvents(

account.getAccountId(),

uncommittedEvents,

account.getVersion() - uncommittedEvents.size()

);

account.markEventsAsCommitted();

}

}

public BankAccount findById(String accountId) {

List<Event> events = eventStore.getEvents(accountId);

if (events.isEmpty()) {

return null;

}

return BankAccount.fromEvents(events);

}

// Temporal query: get account state at specific time

public BankAccount findByIdAtTime(String accountId, Instant timestamp) {

List<Event> allEvents = eventStore.getEvents(accountId);

List<Event> eventsUntilTime = allEvents.stream()

.filter(e -> e.getTimestamp().isBefore(timestamp) ||

e.getTimestamp().equals(timestamp))

.collect(Collectors.toList());

if (eventsUntilTime.isEmpty()) {

return null;

}

return BankAccount.fromEvents(eventsUntilTime);

}

}

// Usage example

public class EventSourcingExample {

public void demonstrateEventSourcing() {

EventStore eventStore = new InMemoryEventStore();

BankAccountRepository repository = new BankAccountRepository(eventStore);

// Create new account

BankAccount account = BankAccount.openAccount(

"ACC-12345",

"CUST-001",

new BigDecimal("1000.00")

);

repository.save(account);

String accountId = account.getAccountId();

// Perform operations

BankAccount loadedAccount = repository.findById(accountId);

loadedAccount.deposit(new BigDecimal("500.00"), "Salary deposit");

loadedAccount.withdraw(new BigDecimal("200.00"), "ATM withdrawal");

repository.save(loadedAccount);

// Reload and verify

BankAccount reloadedAccount = repository.findById(accountId);

System.out.println("Current balance: " + reloadedAccount.getBalance());

// Output: Current balance: 1300.00

// Temporal query: what was the balance after the first deposit?

List<Event> events = eventStore.getEvents(accountId);

Instant afterFirstDeposit = events.get(1).getTimestamp();

BankAccount historicalAccount =

repository.findByIdAtTime(accountId, afterFirstDeposit);

System.out.println("Balance after first deposit: " +

historicalAccount.getBalance());

// Output: Balance after first deposit: 1500.00

}

}

This Event Sourcing implementation stores all changes as events rather than just the current state. The BankAccount aggregate produces events in response to commands like deposit and withdraw. The current state is reconstructed by replaying events. This enables temporal queries to see what the balance was at any point in time, provides a complete audit trail, and allows the system to rebuild state if the read model becomes corrupted.

## NEW CONCURRENCY AND REACTIVE PATTERNS

The **Async-Await pattern** would be fundamental in a modern pattern catalog. This pattern provides a way to write asynchronous code that looks and behaves like synchronous code, making it much easier to reason about and maintain. Before async-await, asynchronous programming required callbacks or complex promise chains that led to difficult-to-read code. The async-await pattern allows developers to write asynchronous operations in a sequential style while still getting the benefits of non-blocking execution.

The pattern works by marking functions as asynchronous with an async keyword and using an await keyword to wait for asynchronous operations to complete. When an await is encountered, the function yields control back to the caller, allowing other work to proceed. When the awaited operation completes, execution resumes from where it left off. This provides the performance benefits of asynchronous execution without the complexity of callback-based code.

The constituents of the Async-Await pattern include async functions, which are functions that can contain await expressions and return promises or futures; await expressions, which pause execution until an asynchronous operation completes; the event loop or task scheduler, which manages the execution of asynchronous operations; and the underlying promise or future mechanism that represents the eventual result of an asynchronous operation.

Here is an example showing the evolution from callback-based to async-await style:

// Old callback-based approach - difficult to read and maintain

public class CallbackExample {

public void processOrder(String orderId, Callback<OrderResult> callback) {

// Fetch order details

orderService.getOrder(orderId, new Callback<Order>() {

public void onSuccess(Order order) {

// Validate inventory

inventoryService.checkInventory(order.getItems(),

new Callback<InventoryResult>() {

public void onSuccess(InventoryResult inventory) {

if (inventory.isAvailable()) {

// Process payment

paymentService.processPayment(order.getPayment(),

new Callback<PaymentResult>() {

public void onSuccess(PaymentResult payment) {

// Create shipment

shippingService.createShipment(order,

new Callback<ShipmentResult>() {

public void onSuccess(ShipmentResult shipment) {

callback.onSuccess(

new OrderResult(order, shipment));

}

public void onError(Exception e) {

callback.onError(e);

}

});

}

public void onError(Exception e) {

callback.onError(e);

}

});

} else {

callback.onError(

new Exception("Inventory not available"));

}

}

public void onError(Exception e) {

callback.onError(e);

}

});

}

public void onError(Exception e) {

callback.onError(e);

}

});

}

}

// Modern async-await approach - clear and maintainable

public class AsyncAwaitExample {

// Mark method as async and return CompletableFuture

public CompletableFuture<OrderResult> processOrderAsync(String orderId) {

return CompletableFuture.supplyAsync(() -> {

try {

// Fetch order details - await the result

Order order = orderService.getOrderAsync(orderId).join();

// Validate inventory - await the result

InventoryResult inventory =

inventoryService.checkInventoryAsync(order.getItems()).join();

if (!inventory.isAvailable()) {

throw new RuntimeException("Inventory not available");

}

// Process payment - await the result

PaymentResult payment =

paymentService.processPaymentAsync(order.getPayment()).join();

// Create shipment - await the result

ShipmentResult shipment =

shippingService.createShipmentAsync(order).join();

return new OrderResult(order, shipment);

} catch (Exception e) {

throw new RuntimeException("Order processing failed", e);

}

});

}

// Even better with proper async composition

public CompletableFuture<OrderResult> processOrderAsyncComposed(String orderId) {

return orderService.getOrderAsync(orderId)

.thenCompose(order ->

inventoryService.checkInventoryAsync(order.getItems())

.thenApply(inventory -> {

if (!inventory.isAvailable()) {

throw new RuntimeException("Inventory not available");

}

return order;

})

)

.thenCompose(order ->

paymentService.processPaymentAsync(order.getPayment())

.thenApply(payment -> order)

)

.thenCompose(order ->

shippingService.createShipmentAsync(order)

.thenApply(shipment -> new OrderResult(order, shipment))

);

}

}

In languages with native async-await support like Python, JavaScript, or C#, the code becomes even cleaner:

\# Python example with native async-await

async def process\_order(order\_id):

\# Fetch order details

order = await order\_service.get\_order(order\_id)

\# Validate inventory

inventory = await inventory\_service.check\_inventory(order.items)

if not inventory.is\_available():

raise Exception("Inventory not available")

\# Process payment

payment = await payment\_service.process\_payment(order.payment)

\# Create shipment

shipment = await shipping\_service.create\_shipment(order)

return OrderResult(order, shipment)

\# Error handling with try-except

async def process\_order\_with\_error\_handling(order\_id):

try:

order = await order\_service.get\_order(order\_id)

inventory = await inventory\_service.check\_inventory(order.items)

if not inventory.is\_available():

return OrderResult.failed("Inventory not available")

payment = await payment\_service.process\_payment(order.payment)

shipment = await shipping\_service.create\_shipment(order)

return OrderResult.success(order, shipment)

except PaymentException as e:

\# Handle payment-specific errors

return OrderResult.failed(f"Payment failed: {e}")

except Exception as e:

\# Handle general errors

return OrderResult.failed(f"Order processing failed: {e}")

\# Concurrent execution of independent operations

async def process\_order\_concurrent(order\_id):

order = await order\_service.get\_order(order\_id)

\# Execute inventory check and credit check concurrently

inventory\_task = inventory\_service.check\_inventory(order.items)

credit\_task = credit\_service.check\_credit(order.customer\_id, order.total)

\# Wait for both to complete

inventory, credit = await asyncio.gather(inventory\_task, credit\_task)

if not inventory.is\_available():

raise Exception("Inventory not available")

if not credit.is\_approved():

raise Exception("Credit check failed")

payment = await payment\_service.process\_payment(order.payment)

shipment = await shipping\_service.create\_shipment(order)

return OrderResult(order, shipment)

The async-await pattern transforms asynchronous programming from a complex callback-based approach into a straightforward sequential style. The code reads naturally from top to bottom, error handling uses standard try-catch mechanisms, and the execution is still non-blocking and efficient. This pattern has become essential for modern applications that need to handle many concurrent operations without blocking threads.

The **Backpressure pattern** would be another critical addition for reactive systems. Backpressure addresses the problem of a fast producer overwhelming a slow consumer. In traditional push-based systems, if a producer generates data faster than a consumer can process it, the consumer's queue grows unbounded, eventually leading to memory exhaustion or system failure. Backpressure provides a mechanism for consumers to signal to producers that they need to slow down.

The pattern involves several strategies for handling backpressure. The consumer can request a specific number of items from the producer, implementing pull-based flow control. The producer can buffer items up to a limit and then apply a strategy like dropping old items, dropping new items, or blocking until space is available. The consumer can dynamically adjust its request rate based on its processing capacity.

The constituents of the Backpressure pattern include the publisher, which produces items and respects backpressure signals; the subscriber, which consumes items and signals demand; the subscription, which represents the connection between publisher and subscriber and carries backpressure signals; and buffering strategies, which determine how to handle items when the consumer cannot keep up.

Here is an implementation of the Backpressure pattern using reactive streams:

import java.util.concurrent.Flow.\*;

import java.util.concurrent.SubmissionPublisher;

import java.util.concurrent.TimeUnit;

// Publisher that respects backpressure

public class BackpressureAwarePublisher {

private final SubmissionPublisher<DataItem> publisher;

public BackpressureAwarePublisher() {

// Configure publisher with buffer and overflow strategy

this.publisher = new SubmissionPublisher<>(

ForkJoinPool.commonPool(),

Flow.defaultBufferSize()

);

}

public void subscribe(Subscriber<DataItem> subscriber) {

publisher.subscribe(subscriber);

}

public void publishData() {

// Simulate data production

for (int i = 0; i < 1000; i++) {

DataItem item = new DataItem(i, "Data " + i);

// submit() respects backpressure

// It will block if subscriber cannot keep up and buffer is full

int lag = publisher.submit(item);

if (lag > 10) {

// Subscriber is falling behind, slow down production

System.out.println("Backpressure detected, lag: " + lag);

try {

Thread.sleep(100);

} catch (InterruptedException e) {

Thread.currentThread().interrupt();

break;

}

}

}

publisher.close();

}

}

// Subscriber that controls its consumption rate

public class BackpressureAwareSubscriber implements Subscriber<DataItem> {

private Subscription subscription;

private final int requestSize;

private int processedCount = 0;

public BackpressureAwareSubscriber(int requestSize) {

this.requestSize = requestSize;

}

public void onSubscribe(Subscription subscription) {

this.subscription = subscription;

// Request initial batch of items

subscription.request(requestSize);

}

public void onNext(DataItem item) {

// Process the item

processItem(item);

processedCount++;

// Request more items when we have processed a batch

if (processedCount % requestSize == 0) {

subscription.request(requestSize);

}

}

public void onError(Throwable throwable) {

System.err.println("Error in subscriber: " + throwable.getMessage());

}

public void onComplete() {

System.out.println("Subscriber completed, processed " +

processedCount + " items");

}

private void processItem(DataItem item) {

// Simulate slow processing

try {

Thread.sleep(50);

System.out.println("Processed: " + item.getId());

} catch (InterruptedException e) {

Thread.currentThread().interrupt();

}

}

}

// Adaptive subscriber that adjusts request rate based on processing time

public class AdaptiveBackpressureSubscriber implements Subscriber<DataItem> {

private Subscription subscription;

private int currentRequestSize;

private final int minRequestSize;

private final int maxRequestSize;

private long lastRequestTime;

private int processedSinceLastRequest;

public AdaptiveBackpressureSubscriber(int minRequestSize, int maxRequestSize) {

this.minRequestSize = minRequestSize;

this.maxRequestSize = maxRequestSize;

this.currentRequestSize = minRequestSize;

}

public void onSubscribe(Subscription subscription) {

this.subscription = subscription;

this.lastRequestTime = System.currentTimeMillis();

subscription.request(currentRequestSize);

}

public void onNext(DataItem item) {

processItem(item);

processedSinceLastRequest++;

// Check if we should request more items

if (processedSinceLastRequest >= currentRequestSize) {

adjustRequestSize();

subscription.request(currentRequestSize);

processedSinceLastRequest = 0;

lastRequestTime = System.currentTimeMillis();

}

}

private void adjustRequestSize() {

long timeTaken = System.currentTimeMillis() - lastRequestTime;

long averageTimePerItem = timeTaken / currentRequestSize;

// If processing is fast, increase request size

if (averageTimePerItem < 10 && currentRequestSize < maxRequestSize) {

currentRequestSize = Math.min(currentRequestSize \* 2, maxRequestSize);

System.out.println("Increased request size to " + currentRequestSize);

}

// If processing is slow, decrease request size

else if (averageTimePerItem > 100 && currentRequestSize > minRequestSize) {

currentRequestSize = Math.max(currentRequestSize / 2, minRequestSize);

System.out.println("Decreased request size to " + currentRequestSize);

}

}

public void onError(Throwable throwable) {

System.err.println("Error: " + throwable.getMessage());

}

public void onComplete() {

System.out.println("Completed");

}

private void processItem(DataItem item) {

// Processing logic

try {

Thread.sleep(20);

} catch (InterruptedException e) {

Thread.currentThread().interrupt();

}

}

}

// Example with different buffering strategies

public class BufferingStrategies {

// Drop oldest items when buffer is full

public static class DropOldestBuffer<T> {

private final Queue<T> buffer;

private final int maxSize;

public DropOldestBuffer(int maxSize) {

this.buffer = new LinkedList<>();

this.maxSize = maxSize;

}

public synchronized boolean offer(T item) {

if (buffer.size() >= maxSize) {

buffer.poll(); // Remove oldest

}

return buffer.offer(item);

}

public synchronized T poll() {

return buffer.poll();

}

public synchronized int size() {

return buffer.size();

}

}

// Drop newest items when buffer is full

public static class DropNewestBuffer<T> {

private final Queue<T> buffer;

private final int maxSize;

public DropNewestBuffer(int maxSize) {

this.buffer = new LinkedList<>();

this.maxSize = maxSize;

}

public synchronized boolean offer(T item) {

if (buffer.size() >= maxSize) {

return false; // Drop the new item

}

return buffer.offer(item);

}

public synchronized T poll() {

return buffer.poll();

}

}

// Sample items when buffer is full

public static class SamplingBuffer<T> {

private final Queue<T> buffer;

private final int maxSize;

private int skipCounter = 0;

private int skipRate = 1;

public SamplingBuffer(int maxSize) {

this.buffer = new LinkedList<>();

this.maxSize = maxSize;

}

public synchronized boolean offer(T item) {

if (buffer.size() >= maxSize) {

// Increase skip rate when buffer is full

skipRate = Math.min(skipRate \* 2, 100);

}

skipCounter++;

if (skipCounter % skipRate == 0) {

if (buffer.size() >= maxSize) {

buffer.poll();

}

buffer.offer(item);

return true;

}

return false;

}

public synchronized T poll() {

T item = buffer.poll();

if (buffer.size() < maxSize / 2) {

// Decrease skip rate when buffer has space

skipRate = Math.max(skipRate / 2, 1);

}

return item;

}

}

}

This Backpressure implementation allows consumers to control the rate at which they receive items from producers. The adaptive subscriber dynamically adjusts its request size based on processing speed, preventing overwhelming the consumer while maximizing throughput. The different buffering strategies provide options for handling situations where the consumer temporarily falls behind. This pattern is essential for building reactive systems that remain stable under varying load conditions.

The **Actor Model pattern** would be prominently featured in a modern concurrency patterns section. The Actor Model provides a higher-level abstraction for concurrent programming than traditional threads and locks. In this model, actors are independent entities that communicate exclusively through asynchronous message passing. Each actor has its own private state that cannot be accessed directly by other actors, eliminating the need for locks and avoiding many concurrency problems.

The constituents of the Actor Model include actors, which are independent computational entities with private state; mailboxes, which are queues that hold messages sent to an actor; messages, which are immutable data structures sent between actors; and the actor system, which manages actor lifecycle and message delivery. Each actor processes messages sequentially from its mailbox, ensuring that its state is never accessed concurrently.

Here is an implementation of the Actor Model for a banking system:

import java.util.concurrent.\*;

import java.util.HashMap;

import java.util.Map;

// Base message class

public abstract class Message {

private final String senderId;

public Message(String senderId) {

this.senderId = senderId;

}

public String getSenderId() {

return senderId;

}

}

// Specific message types

public class DepositMessage extends Message {

private final BigDecimal amount;

public DepositMessage(String senderId, BigDecimal amount) {

super(senderId);

this.amount = amount;

}

public BigDecimal getAmount() {

return amount;

}

}

public class WithdrawMessage extends Message {

private final BigDecimal amount;

public WithdrawMessage(String senderId, BigDecimal amount) {

super(senderId);

this.amount = amount;

}

public BigDecimal getAmount() {

return amount;

}

}

public class GetBalanceMessage extends Message {

private final CompletableFuture<BigDecimal> responseFuture;

public GetBalanceMessage(String senderId,

CompletableFuture<BigDecimal> responseFuture) {

super(senderId);

this.responseFuture = responseFuture;

}

public CompletableFuture<BigDecimal> getResponseFuture() {

return responseFuture;

}

}

public class TransferMessage extends Message {

private final String targetAccountId;

private final BigDecimal amount;

public TransferMessage(String senderId, String targetAccountId,

BigDecimal amount) {

super(senderId);

this.targetAccountId = targetAccountId;

this.amount = amount;

}

public String getTargetAccountId() {

return targetAccountId;

}

public BigDecimal getAmount() {

return amount;

}

}

// Actor base class

public abstract class Actor {

private final String actorId;

private final BlockingQueue<Message> mailbox;

private final ExecutorService executor;

private volatile boolean running;

public Actor(String actorId, ExecutorService executor) {

this.actorId = actorId;

this.mailbox = new LinkedBlockingQueue<>();

this.executor = executor;

this.running = false;

}

public void start() {

if (!running) {

running = true;

executor.submit(this::processMessages);

}

}

public void stop() {

running = false;

}

public void send(Message message) {

mailbox.offer(message);

}

private void processMessages() {

while (running) {

try {

Message message = mailbox.poll(100, TimeUnit.MILLISECONDS);

if (message!= null) {

receive(message);

}

} catch (InterruptedException e) {

Thread.currentThread().interrupt();

break;

}

}

}

protected abstract void receive(Message message);

public String getActorId() {

return actorId;

}

}

// Bank account actor

public class BankAccountActor extends Actor {

private BigDecimal balance;

private final Map<String, Actor> actorRegistry;

public BankAccountActor(String accountId, BigDecimal initialBalance,

ExecutorService executor,

Map<String, Actor> actorRegistry) {

super(accountId, executor);

this.balance = initialBalance;

this.actorRegistry = actorRegistry;

}

protected void receive(Message message) {

// Process messages sequentially, no concurrent access to balance

if (message instanceof DepositMessage) {

handleDeposit((DepositMessage) message);

} else if (message instanceof WithdrawMessage) {

handleWithdraw((WithdrawMessage) message);

} else if (message instanceof GetBalanceMessage) {

handleGetBalance((GetBalanceMessage) message);

} else if (message instanceof TransferMessage) {

handleTransfer((TransferMessage) message);

}

}

private void handleDeposit(DepositMessage message) {

balance = balance.add(message.getAmount());

System.out.println("Account " + getActorId() +

" deposited " + message.getAmount() +

", new balance: " + balance);

}

private void handleWithdraw(WithdrawMessage message) {

if (balance.compareTo(message.getAmount()) >= 0) {

balance = balance.subtract(message.getAmount());

System.out.println("Account " + getActorId() +

" withdrew " + message.getAmount() +

", new balance: " + balance);

} else {

System.out.println("Account " + getActorId() +

" insufficient funds for withdrawal of " +

message.getAmount());

}

}

private void handleGetBalance(GetBalanceMessage message) {

message.getResponseFuture().complete(balance);

}

private void handleTransfer(TransferMessage message) {

if (balance.compareTo(message.getAmount()) >= 0) {

balance = balance.subtract(message.getAmount());

// Send deposit message to target account

Actor targetActor = actorRegistry.get(message.getTargetAccountId());

if (targetActor!= null) {

targetActor.send(new DepositMessage(

getActorId(),

message.getAmount()

));

System.out.println("Account " + getActorId() +

" transferred " + message.getAmount() +

" to " + message.getTargetAccountId());

} else {

// Target account not found, refund

balance = balance.add(message.getAmount());

System.out.println("Transfer failed, target account not found");

}

} else {

System.out.println("Account " + getActorId() +

" insufficient funds for transfer");

}

}

}

// Actor system that manages actors

public class ActorSystem {

private final ExecutorService executor;

private final Map<String, Actor> actors;

public ActorSystem(int threadPoolSize) {

this.executor = Executors.newFixedThreadPool(threadPoolSize);

this.actors = new ConcurrentHashMap<>();

}

public BankAccountActor createBankAccount(String accountId,

BigDecimal initialBalance) {

BankAccountActor actor = new BankAccountActor(

accountId,

initialBalance,

executor,

actors

);

actors.put(accountId, actor);

actor.start();

return actor;

}

public Actor getActor(String actorId) {

return actors.get(actorId);

}

public void shutdown() {

actors.values().forEach(Actor::stop);

executor.shutdown();

try {

executor.awaitTermination(5, TimeUnit.SECONDS);

} catch (InterruptedException e) {

executor.shutdownNow();

}

}

}

// Usage example

public class ActorModelExample {

public void demonstrateActorModel() throws Exception {

ActorSystem system = new ActorSystem(4);

// Create account actors

BankAccountActor account1 = system.createBankAccount(

"ACC-001",

new BigDecimal("1000.00")

);

BankAccountActor account2 = system.createBankAccount(

"ACC-002",

new BigDecimal("500.00")

);

// Send messages to actors

account1.send(new DepositMessage("external", new BigDecimal("200.00")));

account1.send(new WithdrawMessage("external", new BigDecimal("150.00")));

// Transfer between accounts

account1.send(new TransferMessage(

"external",

"ACC-002",

new BigDecimal("300.00")

));

// Query balance asynchronously

CompletableFuture<BigDecimal> balanceFuture = new CompletableFuture<>();

account1.send(new GetBalanceMessage("external", balanceFuture));

BigDecimal balance = balanceFuture.get(1, TimeUnit.SECONDS);

System.out.println("Account 1 balance: " + balance);

// Allow time for message processing

Thread.sleep(1000);

system.shutdown();

}

}

The Actor Model eliminates the need for explicit locking because each actor processes messages sequentially. Multiple actors can run concurrently, but each actor's state is accessed by only one thread at a time. This makes concurrent programming much simpler and less error-prone. The pattern is particularly well-suited for systems with many independent entities that need to coordinate through message passing, such as distributed systems, game servers, and real-time data processing pipelines.

## NEW DATA PATTERNS FOR MODERN APPLICATIONS

The **Repository pattern** would be significantly expanded in a modern pattern catalog. While the basic concept of abstracting data access existed in earlier patterns, the modern Repository pattern has evolved to handle much more complex scenarios including multiple data sources, caching strategies, query optimization, and integration with domain-driven design principles. The pattern provides a collection-like interface for accessing domain objects while encapsulating the details of data access and persistence.

The modern Repository pattern separates the domain model from data access concerns, allowing the domain logic to remain independent of the persistence mechanism. This enables changing the underlying data store without affecting business logic, facilitates testing by allowing mock repositories, and provides a centralized place for data access logic and caching strategies.

The constituents of the modern Repository pattern include the repository interface, which defines the contract for data access operations; the concrete repository implementation, which handles the actual data access; the domain model, which represents business entities; the data mapper, which translates between domain objects and data store representations; and the unit of work, which coordinates changes across multiple repositories.

Here is a comprehensive implementation of the modern Repository pattern:

import java.util.\*;

import java.util.concurrent.ConcurrentHashMap;

import java.util.stream.Collectors;

// Domain model

public class Customer {

private final String customerId;

private String name;

private String email;

private CustomerStatus status;

private List<Order> orders;

public Customer(String customerId, String name, String email) {

this.customerId = customerId;

this.name = name;

this.email = email;

this.status = CustomerStatus.ACTIVE;

this.orders = new ArrayList<>();

}

// Getters and setters

public String getCustomerId() { return customerId; }

public String getName() { return name; }

public void setName(String name) { this.name = name; }

public String getEmail() { return email; }

public void setEmail(String email) { this.email = email; }

public CustomerStatus getStatus() { return status; }

public void setStatus(CustomerStatus status) { this.status = status; }

public List<Order> getOrders() { return new ArrayList<>(orders); }

public void addOrder(Order order) { orders.add(order); }

}

public enum CustomerStatus {

ACTIVE, INACTIVE, SUSPENDED

}

// Specification pattern for complex queries

public interface Specification<T> {

boolean isSatisfiedBy(T item);

default Specification<T> and(Specification<T> other) {

return item -> this.isSatisfiedBy(item) && other.isSatisfiedBy(item);

}

default Specification<T> or(Specification<T> other) {

return item -> this.isSatisfiedBy(item) || other.isSatisfiedBy(item);

}

default Specification<T> not() {

return item ->!this.isSatisfiedBy(item);

}

}

// Example specifications

public class CustomerByStatusSpecification implements Specification<Customer> {

private final CustomerStatus status;

public CustomerByStatusSpecification(CustomerStatus status) {

this.status = status;

}

public boolean isSatisfiedBy(Customer customer) {

return customer.getStatus() == status;

}

}

public class CustomerByEmailDomainSpecification implements Specification<Customer> {

private final String domain;

public CustomerByEmailDomainSpecification(String domain) {

this.domain = domain;

}

public boolean isSatisfiedBy(Customer customer) {

return customer.getEmail().endsWith("@" + domain);

}

}

// Repository interface

public interface CustomerRepository {

void save(Customer customer);

void delete(String customerId);

Optional<Customer> findById(String customerId);

List<Customer> findAll();

List<Customer> findBySpecification(Specification<Customer> spec);

List<Customer> findByStatus(CustomerStatus status);

Optional<Customer> findByEmail(String email);

long count();

}

// Concrete repository implementation with caching

public class CachedCustomerRepository implements CustomerRepository {

private final Map<String, Customer> dataStore;

private final Map<String, Customer> cache;

private final int cacheMaxSize;

private final long cacheTTLMillis;

private final Map<String, Long> cacheTimestamps;

public CachedCustomerRepository(int cacheMaxSize, long cacheTTLMillis) {

this.dataStore = new ConcurrentHashMap<>();

this.cache = new ConcurrentHashMap<>();

this.cacheTimestamps = new ConcurrentHashMap<>();

this.cacheMaxSize = cacheMaxSize;

this.cacheTTLMillis = cacheTTLMillis;

}

public void save(Customer customer) {

// Save to data store

dataStore.put(customer.getCustomerId(), cloneCustomer(customer));

// Update cache

cache.put(customer.getCustomerId(), cloneCustomer(customer));

cacheTimestamps.put(customer.getCustomerId(), System.currentTimeMillis());

// Evict old cache entries if cache is too large

if (cache.size() > cacheMaxSize) {

evictOldestCacheEntry();

}

}

public void delete(String customerId) {

dataStore.remove(customerId);

cache.remove(customerId);

cacheTimestamps.remove(customerId);

}

public Optional<Customer> findById(String customerId) {

// Check cache first

Customer cached = cache.get(customerId);

if (cached!= null && isCacheValid(customerId)) {

return Optional.of(cloneCustomer(cached));

}

// Cache miss or expired, load from data store

Customer customer = dataStore.get(customerId);

if (customer!= null) {

// Update cache

cache.put(customerId, cloneCustomer(customer));

cacheTimestamps.put(customerId, System.currentTimeMillis());

return Optional.of(cloneCustomer(customer));

}

return Optional.empty();

}

public List<Customer> findAll() {

return dataStore.values().stream()

.map(this::cloneCustomer)

.collect(Collectors.toList());

}

public List<Customer> findBySpecification(Specification<Customer> spec) {

return dataStore.values().stream()

.filter(spec::isSatisfiedBy)

.map(this::cloneCustomer)

.collect(Collectors.toList());

}

public List<Customer> findByStatus(CustomerStatus status) {

return findBySpecification(new CustomerByStatusSpecification(status));

}

public Optional<Customer> findByEmail(String email) {

return dataStore.values().stream()

.filter(c -> c.getEmail().equals(email))

.findFirst()

.map(this::cloneCustomer);

}

public long count() {

return dataStore.size();

}

private boolean isCacheValid(String customerId) {

Long timestamp = cacheTimestamps.get(customerId);

if (timestamp == null) {

return false;

}

return System.currentTimeMillis() - timestamp < cacheTTLMillis;

}

private void evictOldestCacheEntry() {

String oldestKey = cacheTimestamps.entrySet().stream()

.min(Map.Entry.comparingByValue())

.map(Map.Entry::getKey)

.orElse(null);

if (oldestKey!= null) {

cache.remove(oldestKey);

cacheTimestamps.remove(oldestKey);

}

}

private Customer cloneCustomer(Customer customer) {

// Create a defensive copy to prevent external modification

Customer clone = new Customer(

customer.getCustomerId(),

customer.getName(),

customer.getEmail()

);

clone.setStatus(customer.getStatus());

return clone;

}

}

// Unit of Work pattern for coordinating changes

public class UnitOfWork {

private final Map<String, Customer> newCustomers;

private final Map<String, Customer> modifiedCustomers;

private final Set<String> deletedCustomerIds;

private final CustomerRepository repository;

public UnitOfWork(CustomerRepository repository) {

this.repository = repository;

this.newCustomers = new HashMap<>();

this.modifiedCustomers = new HashMap<>();

this.deletedCustomerIds = new HashSet<>();

}

public void registerNew(Customer customer) {

newCustomers.put(customer.getCustomerId(), customer);

}

public void registerModified(Customer customer) {

if (!newCustomers.containsKey(customer.getCustomerId())) {

modifiedCustomers.put(customer.getCustomerId(), customer);

}

}

public void registerDeleted(String customerId) {

newCustomers.remove(customerId);

modifiedCustomers.remove(customerId);

deletedCustomerIds.add(customerId);

}

public void commit() {

// Save new customers

for (Customer customer: newCustomers.values()) {

repository.save(customer);

}

// Save modified customers

for (Customer customer: modifiedCustomers.values()) {

repository.save(customer);

}

// Delete customers

for (String customerId: deletedCustomerIds) {

repository.delete(customerId);

}

// Clear tracking collections

newCustomers.clear();

modifiedCustomers.clear();

deletedCustomerIds.clear();

}

public void rollback() {

newCustomers.clear();

modifiedCustomers.clear();

deletedCustomerIds.clear();

}

}

// Usage example

public class RepositoryExample {

public void demonstrateRepository() {

CustomerRepository repository = new CachedCustomerRepository(100, 60000);

UnitOfWork unitOfWork = new UnitOfWork(repository);

// Create new customers

Customer customer1 = new Customer("CUST-001", "John Doe", "john@example.com");

Customer customer2 = new Customer("CUST-002", "Jane Smith", "jane@company.com");

Customer customer3 = new Customer("CUST-003", "Bob Johnson", "bob@example.com");

unitOfWork.registerNew(customer1);

unitOfWork.registerNew(customer2);

unitOfWork.registerNew(customer3);

unitOfWork.commit();

// Find by ID

Optional<Customer> found = repository.findById("CUST-001");

found.ifPresent(c -> System.out.println("Found customer: " + c.getName()));

// Find by specification

Specification<Customer> exampleDomainSpec =

new CustomerByEmailDomainSpecification("example.com");

Specification<Customer> activeSpec =

new CustomerByStatusSpecification(CustomerStatus.ACTIVE);

List<Customer> activeExampleCustomers =

repository.findBySpecification(exampleDomainSpec.and(activeSpec));

System.out.println("Found " + activeExampleCustomers.size() +

" active customers with example.com email");

// Modify customer

found.ifPresent(customer -> {

customer.setStatus(CustomerStatus.SUSPENDED);

unitOfWork.registerModified(customer);

});

unitOfWork.commit();

// Complex query with combined specifications

Specification<Customer> complexSpec =

new CustomerByStatusSpecification(CustomerStatus.ACTIVE)

.or(new CustomerByStatusSpecification(CustomerStatus.SUSPENDED))

.and(new CustomerByEmailDomainSpecification("example.com"));

List<Customer> complexResult = repository.findBySpecification(complexSpec);

System.out.println("Complex query found " + complexResult.size() + " customers");

}

}

This modern Repository implementation provides a clean abstraction over data access with caching, specification-based queries, and unit of work coordination. The specification pattern allows building complex queries through composition without polluting the repository interface with numerous query methods. The caching layer improves performance while remaining transparent to clients. The unit of work pattern coordinates changes across multiple entities and provides transaction-like semantics.

The **CQRS with Event Sourcing pattern** represents a powerful combination that would be prominently featured in a modern data patterns section. This pattern combines Command Query Responsibility Segregation with Event Sourcing to create systems that separate write and read concerns while maintaining a complete audit trail. The write side uses event sourcing to store all changes as events, while the read side builds optimized projections from those events.

This combination provides several advantages. The write model can focus on enforcing business rules and maintaining consistency. The read model can be optimized for specific query patterns without compromising the write model. Multiple read models can be built from the same event stream for different purposes. The event log provides a complete audit trail and enables temporal queries. The system can scale reads and writes independently.

Here is an implementation combining CQRS and Event Sourcing:

// Events from earlier Event Sourcing example

// AccountOpenedEvent, MoneyDepositedEvent, MoneyWithdrawnEvent

// Read model for account balance queries

public class AccountBalanceReadModel {

private final String accountId;

private final String accountNumber;

private final String customerId;

private BigDecimal balance;

private Instant lastUpdated;

private int transactionCount;

public AccountBalanceReadModel(String accountId, String accountNumber,

String customerId, BigDecimal initialBalance) {

this.accountId = accountId;

this.accountNumber = accountNumber;

this.customerId = customerId;

this.balance = initialBalance;

this.lastUpdated = Instant.now();

this.transactionCount = 0;

}

public void applyDeposit(BigDecimal amount, Instant timestamp) {

this.balance = this.balance.add(amount);

this.lastUpdated = timestamp;

this.transactionCount++;

}

public void applyWithdrawal(BigDecimal amount, Instant timestamp) {

this.balance = this.balance.subtract(amount);

this.lastUpdated = timestamp;

this.transactionCount++;

}

// Getters

public String getAccountId() { return accountId; }

public String getAccountNumber() { return accountNumber; }

public String getCustomerId() { return customerId; }

public BigDecimal getBalance() { return balance; }

public Instant getLastUpdated() { return lastUpdated; }

public int getTransactionCount() { return transactionCount; }

}

// Read model for transaction history queries

public class TransactionHistoryReadModel {

private final String accountId;

private final List<TransactionEntry> transactions;

public TransactionHistoryReadModel(String accountId) {

this.accountId = accountId;

this.transactions = new ArrayList<>();

}

public void addTransaction(String type, BigDecimal amount,

String description, Instant timestamp) {

transactions.add(new TransactionEntry(type, amount, description, timestamp));

}

public List<TransactionEntry> getTransactions() {

return new ArrayList<>(transactions);

}

public List<TransactionEntry> getTransactionsSince(Instant since) {

return transactions.stream()

.filter(t -> t.getTimestamp().isAfter(since))

.collect(Collectors.toList());

}

public BigDecimal getTotalDeposits() {

return transactions.stream()

.filter(t -> t.getType().equals("DEPOSIT"))

.map(TransactionEntry::getAmount)

.reduce(BigDecimal.ZERO, BigDecimal::add);

}

public BigDecimal getTotalWithdrawals() {

return transactions.stream()

.filter(t -> t.getType().equals("WITHDRAWAL"))

.map(TransactionEntry::getAmount)

.reduce(BigDecimal.ZERO, BigDecimal::add);

}

}

public class TransactionEntry {

private final String type;

private final BigDecimal amount;

private final String description;

private final Instant timestamp;

public TransactionEntry(String type, BigDecimal amount,

String description, Instant timestamp) {

this.type = type;

this.amount = amount;

this.description = description;

this.timestamp = timestamp;

}

public String getType() { return type; }

public BigDecimal getAmount() { return amount; }

public String getDescription() { return description; }

public Instant getTimestamp() { return timestamp; }

}

// Event handler that updates read models

public class AccountReadModelUpdater {

private final Map<String, AccountBalanceReadModel> balanceModels;

private final Map<String, TransactionHistoryReadModel> historyModels;

public AccountReadModelUpdater() {

this.balanceModels = new ConcurrentHashMap<>();

this.historyModels = new ConcurrentHashMap<>();

}

public void handleEvent(Event event) {

if (event instanceof AccountOpenedEvent) {

handleAccountOpened((AccountOpenedEvent) event);

} else if (event instanceof MoneyDepositedEvent) {

handleMoneyDeposited((MoneyDepositedEvent) event);

} else if (event instanceof MoneyWithdrawnEvent) {

handleMoneyWithdrawn((MoneyWithdrawnEvent) event);

}

}

private void handleAccountOpened(AccountOpenedEvent event) {

AccountBalanceReadModel balanceModel = new AccountBalanceReadModel(

event.getAggregateId(),

event.getAccountNumber(),

event.getCustomerId(),

event.getInitialBalance()

);

balanceModels.put(event.getAggregateId(), balanceModel);

TransactionHistoryReadModel historyModel =

new TransactionHistoryReadModel(event.getAggregateId());

historyModel.addTransaction(

"OPENING",

event.getInitialBalance(),

"Account opened",

event.getTimestamp()

);

historyModels.put(event.getAggregateId(), historyModel);

}

private void handleMoneyDeposited(MoneyDepositedEvent event) {

AccountBalanceReadModel balanceModel =

balanceModels.get(event.getAggregateId());

if (balanceModel!= null) {

balanceModel.applyDeposit(event.getAmount(), event.getTimestamp());

}

TransactionHistoryReadModel historyModel =

historyModels.get(event.getAggregateId());

if (historyModel!= null) {

historyModel.addTransaction(

"DEPOSIT",

event.getAmount(),

event.getDescription(),

event.getTimestamp()

);

}

}

private void handleMoneyWithdrawn(MoneyWithdrawnEvent event) {

AccountBalanceReadModel balanceModel =

balanceModels.get(event.getAggregateId());

if (balanceModel!= null) {

balanceModel.applyWithdrawal(event.getAmount(), event.getTimestamp());

}

TransactionHistoryReadModel historyModel =

historyModels.get(event.getAggregateId());

if (historyModel!= null) {

historyModel.addTransaction(

"WITHDRAWAL",

event.getAmount(),

event.getDescription(),

event.getTimestamp()

);

}

}

public Optional<AccountBalanceReadModel> getBalanceModel(String accountId) {

return Optional.ofNullable(balanceModels.get(accountId));

}

public Optional<TransactionHistoryReadModel> getHistoryModel(String accountId) {

return Optional.ofNullable(historyModels.get(accountId));

}

}

// Query service for read operations

public class AccountQueryService {

private final AccountReadModelUpdater readModelUpdater;

public AccountQueryService(AccountReadModelUpdater readModelUpdater) {

this.readModelUpdater = readModelUpdater;

}

public Optional<BigDecimal> getAccountBalance(String accountId) {

return readModelUpdater.getBalanceModel(accountId)

.map(AccountBalanceReadModel::getBalance);

}

public Optional<AccountBalanceReadModel> getAccountSummary(String accountId) {

return readModelUpdater.getBalanceModel(accountId);

}

public List<TransactionEntry> getTransactionHistory(String accountId) {

return readModelUpdater.getHistoryModel(accountId)

.map(TransactionHistoryReadModel::getTransactions)

.orElse(Collections.emptyList());

}

public List<TransactionEntry> getRecentTransactions(String accountId,

Duration duration) {

Instant since = Instant.now().minus(duration);

return readModelUpdater.getHistoryModel(accountId)

.map(model -> model.getTransactionsSince(since))

.orElse(Collections.emptyList());

}

public Optional<BigDecimal> getTotalDeposits(String accountId) {

return readModelUpdater.getHistoryModel(accountId)

.map(TransactionHistoryReadModel::getTotalDeposits);

}

}

// Complete CQRS system

public class CQRSBankingSystem {

private final EventStore eventStore;

private final BankAccountRepository writeRepository;

private final AccountReadModelUpdater readModelUpdater;

private final AccountQueryService queryService;

public CQRSBankingSystem(EventStore eventStore) {

this.eventStore = eventStore;

this.writeRepository = new BankAccountRepository(eventStore);

this.readModelUpdater = new AccountReadModelUpdater();

this.queryService = new AccountQueryService(readModelUpdater);

// Subscribe to events to update read models

subscribeToEvents();

}

private void subscribeToEvents() {

// In a real system, this would subscribe to an event bus

// For this example, we will manually update read models after writes

}

// Command side - write operations

public String openAccount(String accountNumber, String customerId,

BigDecimal initialBalance) {

BankAccount account = BankAccount.openAccount(

accountNumber,

customerId,

initialBalance

);

writeRepository.save(account);

// Update read models

for (Event event: account.getUncommittedEvents()) {

readModelUpdater.handleEvent(event);

}

return account.getAccountId();

}

public void deposit(String accountId, BigDecimal amount, String description) {

BankAccount account = writeRepository.findById(accountId)

.orElseThrow(() -> new IllegalArgumentException("Account not found"));

account.deposit(amount, description);

writeRepository.save(account);

// Update read models

for (Event event: account.getUncommittedEvents()) {

readModelUpdater.handleEvent(event);

}

}

public void withdraw(String accountId, BigDecimal amount, String description) {

BankAccount account = writeRepository.findById(accountId)

.orElseThrow(() -> new IllegalArgumentException("Account not found"));

account.withdraw(amount, description);

writeRepository.save(account);

// Update read models

for (Event event: account.getUncommittedEvents()) {

readModelUpdater.handleEvent(event);

}

}

// Query side - read operations

public Optional<BigDecimal> getBalance(String accountId) {

return queryService.getAccountBalance(accountId);

}

public Optional<AccountBalanceReadModel> getAccountSummary(String accountId) {

return queryService.getAccountSummary(accountId);

}

public List<TransactionEntry> getTransactionHistory(String accountId) {

return queryService.getTransactionHistory(accountId);

}

public List<TransactionEntry> getRecentTransactions(String accountId,

Duration duration) {

return queryService.getRecentTransactions(accountId, duration);

}

}

This CQRS with Event Sourcing implementation separates write operations that modify state from read operations that query state. The write side uses event sourcing to maintain a complete history of changes. The read side builds optimized projections for different query patterns. This separation allows independent scaling and optimization of reads and writes, provides a complete audit trail, and enables building multiple specialized read models from the same event stream.

## CONCLUSION

The evolution of design patterns from the classic Gang of Four and POSA books to a modern treatment reflects the profound changes in software development over the past three decades. The shift from monolithic desktop applications to distributed cloud-native systems has rendered some patterns obsolete while demanding entirely new patterns for problems that did not exist in the 1990s. Patterns like Singleton and Abstract Factory that once seemed essential are now recognized as adding unnecessary complexity or creating problems that modern frameworks solve more elegantly. Meanwhile, patterns like Circuit Breaker, Saga, and Event Sourcing have become fundamental for building resilient distributed systems.

The transformation of existing patterns is equally significant. Observer has evolved into sophisticated reactive streams with backpressure support. Command has grown into CQRS with separate read and write models. Strategy has been simplified through functional programming constructs. Proxy has expanded into API gateways and service meshes that handle cross-cutting concerns for entire microservices architectures. These transformations preserve the core intent of the original patterns while adapting their structure and implementation to modern requirements and paradigms.

Perhaps most importantly, the principles underlying design patterns remain as relevant today as they were thirty years ago. The goals of loose coupling, high cohesion, separation of concerns, and designing for change continue to guide software architecture. What has changed is how we achieve these goals. Modern languages provide features like first-class functions, async-await, and pattern matching that make certain patterns simpler or unnecessary. Cloud platforms and container orchestration systems provide infrastructure-level solutions to problems that once required application-level patterns. Functional programming concepts have influenced mainstream languages, leading to more declarative and composable designs. The pattern catalog continues to evolve as new challenges emerge and new solutions are discovered, ensuring that the pattern-oriented approach to software design remains vital and relevant for future generations of developers.