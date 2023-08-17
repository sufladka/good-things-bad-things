# Good Things - Bad Things: A Cookbook for Java Developers

<!-- TOC -->
* [Good Things - Bad Things: A Cookbook for Java Developers](#good-things---bad-things-a-cookbook-for-java-developers)
  * [Introduction](#introduction)
  * [Avoid creating custom frameworks unless you have person-years of free resources](#avoid-creating-custom-frameworks-unless-you-have-person-years-of-free-resources)
  * [Avoid using XML](#avoid-using-xml)
  * [Avoid overusing private methods](#avoid-overusing-private-methods)
  * [Prefer declarative style over imperative one](#prefer-declarative-style-over-imperative-one)
  * [Use static imports for static declarative APIs](#use-static-imports-for-static-declarative-apis)
  * [Test behaviour, not implementation](#test-behaviour-not-implementation)
  * [Write code from left to right, from top to bottom (for sinistrodextral human languages speakers)](#write-code-from-left-to-right-from-top-to-bottom-for-sinistrodextral-human-languages-speakers)
  * [Use named parameters](#use-named-parameters)
<!-- TOC -->

## Introduction
This cookbook is primarily tailored for Java developers while also catering to those from other programming backgrounds, offering a compilation of insights I've acquired throughout my career. Within these pages, you'll find a collection of seemingly straightforward yet incredibly valuable lessons that I've gathered over the course of my journey. As developers, we often immerse ourselves in the complexities of coding, algorithms, and intricate frameworks, sometimes overlooking the power of simplicity.

This guide is a celebration of those simple yet transformative "aha" moments – the lessons that aren't buried within dense technical manuals, but instead arise from real-world experiences, debugging sessions, and collaborative problem-solving. Through this cookbook, I aim to distill these invaluable takeaways and present them in a format that's accessible and applicable for developers of all skill levels.

Whether you're a seasoned Java expert or just embarking on your programming voyage, this collection of insights is meant to serve as a compass, guiding you through the nuanced landscape of software development. Together, we'll navigate through the realms of best practices, coding efficiencies, debugging techniques, and the art of crafting elegant solutions.

As you delve into the pages ahead, I encourage you to approach each entry with an open mind and a willingness to uncover the wisdom that lies within the seemingly ordinary. Just as a skilled chef transforms basic ingredients into a masterpiece, you have the opportunity to elevate your development skills by embracing these foundational principles.

Let's embark on this journey together, as we explore the world of coding wisdom that emerges from both the good and the bad – ultimately shaping us into more adept, insightful, and resourceful developers.

Welcome to the cookbook that celebrates the intricacies of our craft – where good things and bad things converge to form the tapestry of developer wisdom.


## Avoid creating custom frameworks unless you have person-years of free resources
Building a custom framework from scratch can be alluring, promising tailor-made solutions to your development challenges. However, before embarking on this journey, consider the following factors:

1. **Resource intensive and complex**  
Developing a custom framework demands significant investments of time, effort, and resources. Crafting an effective framework requires a deep understanding of software architecture, design patterns, and scalability principles. Additionally, creating a comprehensive solution that addresses various scenarios and edge cases introduces complexity that's often underestimated.

1. **IDE support**   
   When developing custom frameworks, keep in mind that frameworks usually require additional tooling. The less popular a framework is, the more essential the tooling becomes to support developers, given the continuous lack of both individual and community experience.
1. **Maintenance burden and opportunity cost**   
Once the custom framework is in place, ongoing maintenance becomes a substantial commitment. This includes fixing bugs, implementing updates, and ensuring compatibility as technology evolves. The time and resources devoted to maintaining the framework can divert attention from other critical aspects of your project, impacting its core goals.

1. **Bad documentation**   
Thorough documentation is crucial for any successful tool, and custom frameworks are no exception. Crafting clear and comprehensive documentation takes considerable effort. Poor documentation can lead to confusion, frustration, and inefficiencies among your team members, hindering adoption and usability.

1. **Learning curve for the team**  
Introducing a custom framework requires your development team to invest time in learning its intricacies. This learning curve impacts productivity, as developers adapt to new workflows and practices. Not all team members might grasp the new tool at the same pace, potentially leading to skill disparities and resistance to change.

Take a look on any open-source framework. How long it took it to rise into useful product.  
For example, [Spring Framework](https://github.com/spring-projects/spring-framework), a Java framework established in 2004. With 754 contributors and over 27,600 commits, significant resources and community support, a framework is an ongoing endeavor, continually evolving to meet changing needs.

In conclusion, the decision to build a custom framework should be approached cautiously. Unless you have person-years of free resources to invest in development, maintenance, and documentation, leveraging well-established solutions like the Spring Framework is often more pragmatic. The complexities of framework development, coupled with the challenges of documentation and team learning, make opting for existing solutions a wise choice for most projects. Remember that simplicity and efficiency are often found not in building everything from scratch, but in leveraging the wisdom of the broader development community.

**True stories (directed by Robert B. Weide)**  
Actors:  
Framework Supplier (FS): The developer who creates the framework.  
Framework Consumer (FC): The developer who utilizes the framework for daily tasks.  

Story 0:   
FC: This component is useless for our use case. Could you please ensure components work with real-life examples?   
FS: We've tested it in our sandbox. It's your job to use it in real-life scenarios.  
**Moral**: FS is usually out of business. That's why he develops a framework in isolation, ignoring actual business requirements.  

Story 1:   
FS: Due to limited capacity, troubleshooting the framework is now your responsibility, FC.   
FC: Fuuuuu!  
**Moral**: Developing a framework is expensive. FS doesn't have time to maintain a framework. He needs to develop new features.

Story 2:  
FC: (_Glancing at our tiny, chaotic, and poorly organized documentation, often lacking examples and sometimes even absent_) The documentation for our framework feels like fluffware.  
FS: From our perspective, it's comprehensive and valuable. If you find details lacking, create tickets to address them.  
FC: (_Mentally comparing our documentation with mature open-source frameworks_) I meant the documentation as a whole.  
FS: If you believe something is missed, create tickets. Goodbye.  
**Moral**: FS provides pure documentation for a framework and don't want to evaluate it by himself first, because he doesn't consume it. 
But it's like giving code to a team for review without reviewing it by author first, or provide feature to QA for testing without testing by author first, or provide feature to PO for acceptance without testing by QA, etc.   
Of course, in each case the issue will be addressed. The question is in time, cost and reputation.  

## Avoid using XML

I apologize if you've heavily invested in XML, but it's my strong belief that its time has come to an end. Many protocols, tools, and frameworks have moved away from this outdated format, although some still hold onto it, perhaps out of habit or nostalgia. However, the industry's shift toward more modern alternatives is undeniable.

In light of this, let's take a moment to compare how the choice of build tools can reflect this shift. Personally, I lean towards Gradle over Maven, and here's why:

Gradle:  
```groovy
implementation 'org.apache.commons:commons-collections4:4.4'
```

Maven:  
```xml
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-collections4</artifactId>
    <version>4.4</version>
    <scope>runtime</scope>
</dependency>
```

The difference is clear. With Gradle's Groovy-based build scripts, the syntax is concise and expressive. It's a breath of fresh air in comparison to Maven's XML configuration. The example above showcases the elegance and simplicity of Gradle's approach to defining dependencies.

The gradual transition from XML-based configurations to more expressive alternatives, like Groovy scripts in Gradle or YAML in various contexts, has streamlined development and brought about increased readability and maintainability. This change aligns with the industry's movement towards cleaner, more human-friendly syntax.

So, I urge you to consider the benefits of embracing newer, more efficient ways of expressing configurations and dependencies. As the development landscape evolves, it's crucial to adapt and leverage tools that make your work both enjoyable and effective.

## Avoid overusing private methods

There's a common misconception that breaking down a method into many private methods automatically makes it more readable, understandable, and maintainable. However, this belief can lead to a misconception itself.

Private methods encapsulate the vision of their author. Imagine a scenario where a developer divides a method into several private methods, intending to enhance clarity. For instance, consider a method \`processOrder\` that encapsulates the steps of order processing:

```java
private void processOrder(Order order) {
    validateOrder(order);
    updateInventory(order);
    calculateTotal(order);
    generateInvoice(order);
    sendConfirmationEmail(order);
}
```
While this may seem like a logical division, other developers might disagree or find this arrangement less intuitive or even misleading.

Here is why:  
1. **The complexity of understanding**.  
A method split into numerous private methods introduces complexity in understanding the logic. Each private method might lead to other private methods, creating a complex chain that is hard to navigate. This makes comprehending the complete process a daunting task.
1. **Rigidity and implementation mess**.  
Once a set of steps is defined within private methods, developers might hesitate to alter them, even if the steps no longer fit the evolving requirements. Instead, they might attempt to fit new requirements into existing methods, leading to methods that lose their original meaning and introducing confusion.
1. **The paradox of change**.  
Ironically, the correct usage of private methods might involve inlining and redefining them each time the process evolves. This approach aims to ensure that private methods accurately reflect any changes. However, this practice leads to significant modifications every time a change is made, resulting in a cumbersome process.


**Guidelines to consider**
- **Clarity over quantity**: Prioritize the clarity of your code over creating numerous private methods. Ensure that your code's structure aids understanding. 
- **Maintainable abstractions**: If you decide to use private methods, ensure they are meaningful abstractions that enhance the overall logic. 
- [**Declarative style**](#prefer-declarative-style-over-imperative-one): Keep on eyes **what** to do, hide behind **how** to do.
- **Code review**: Encourage code reviews and discussions to determine if the division into private methods is truly enhancing clarity.

So, embrace private methods thoughtfully, with the goal of improving code understanding. 
Remember that while private methods can simplify logic, excessive use can complicate comprehension. 
Strive for a balance that contributes to code that is both maintainable and easily understandable.


## Prefer declarative style over imperative one

Imperative APIs tell you **how** to do something, while declarative APIs tell you **what** to do. This distinction is fundamental and carries significant implications for writing efficient and maintainable code.  
The typical declarative API in Java is the java.util.Stream API.

An imperative API provides explicit step-by-step instructions on how to achieve a certain outcome. For example, consider sorting a collection of strings in an imperative style:
```java
var strings = List.of("Hello", "World", "!");
var sortedStrings = new ArrayList<>(strings);
Collections.sort(sortedStrings, (s1, s2) -> Integer.compare(s1.length(), s2.length()));
var result = List.copyOf(sortedStrings);
```
In contrast, a declarative API focuses on expressing the desired outcome without specifying the step-by-step process.   
Here's the same sorting task in a declarative style using the Stream API:
```java
Stream.of("Hello", "World", "!")
    .sorted(comparing(String::length))
    .collect(toUnmodifiableList());
```

Here is another example:
```java
CompositeValidator.builder()
    // @formatter:off
    //------- attribute ---------|----------------- rule --------------|------------- error -----------------------|
    .with(cart::items            , isNotEmpty()                        ,   CART_IS_EMPTY                           ,
                                   hasSufficientStock()                ,   INSUFFICIENT_STOCK                      )
    //---------------------------|-------------------------------------|-------------------------------------------|
    .with(cart:totalPrice        , isGreaterThan(BigDecimal.ZERO)      ,   TOTAL_PRICE_IS_ZERO_OR_NEGATIVE         )
    //---------------------------|-------------------------------------|-------------------------------------------|
    .with(cart:shippingAddress   , isNotNull()                         ,   SHIPPING_ADDRESS_IS_MISSING             )
    //---------------------------|-------------------------------------|-------------------------------------------|
    // @formatter:on
    .validate();
```
In imperative style, you would find something like:  
```java
private void validateCart() {
    validateItems();
    validateTotalPrice();
    validateShippingAddress();
}
``` 
Declarative code answers the question **how** we validate a cart: we ensure that cart is not empty, stock is sufficient, price is positive, etc. All validation rules are on your eyes.   
Meanwhile, imperative code answers the question **what** we do in order to validate a cart: we validate items, validate price, etc. All validation rules are hidden behind private methods, while this is the only essential part of validation.
 
The declarative approach is often preferred for several reasons:  
* **Readability**: Declarative code reads like a description of the task, making it easier to understand without getting lost in implementation details.
* **Conciseness**: Declarative code is usually shorter and more concise, reducing the chances of errors and making the codebase easier to maintain.
* **Abstraction**: Declarative APIs abstract the underlying complexity, allowing you to focus on what needs to be done, rather than how to do it.

When working with complex systems or large codebases, the declarative approach simplifies comprehension, promotes code reuse, and facilitates debugging. It helps in avoiding low-level management of resources and streamlines code into a more intuitive and natural representation of the problem.

In your programming journey, strive to embrace the declarative style whenever possible. By doing so, you'll produce code that communicates intent effectively and fosters a more maintainable and collaborative development process.

## Use static imports for static declarative APIs

I've emphasized the importance of using declarative APIs. To make them even more elegant, consider employing static imports for static methods where appropriate. 
Let's compare these two code snippets:

```java
Stream.of("1", "2", "3")
    .sorted(Comparator.comparing(String::length))
    .collect(Collectors.toList());
```
```java
Stream.of("1", "2", "3")
    .sorted(comparing(String::length))
    .collect(toList());
```
At first glance, they might seem the same, right? But actually, they aren't. The first version is notably less pleasant, squandering the tokens of your innate intelligence.  
To see the difference clearer, let's attempt to translate both examples into plain English:  
* Stream of 1, 2, 3, sorted Comparator comparing String length, collect Collectors to list.
* Stream of 1, 2, 3, sorted comparing String length, collect to list.   

The first sentence doesn't make much sense, while the second one is a proper English sentence, isn't it?  

By using static imports for static methods, you're not only writing cleaner code but also crafting code that speaks a language closer to everyday conversation. 

## Test behaviour, not implementation
A prevalent misconception exists that unit tests should mock virtually all dependencies and scrutinize each class and method in isolation. While this approach is appropriate for testing library or utility functions, it can have detrimental effects when applied to testing business logic.  

The purpose of unit tests is to guarantee that your code retains functionality throughout refactoring or the introduction of new features. However, if you find yourself modifying code and needing to adjust tests to accommodate the new implementation, these tests become counterproductive. In simpler terms, rather than facilitating refactoring and code evolution, such tests impede it.   

Additionally, when unit tests are too granular and focus on individual methods or classes, they fail to provide insights into the behavior of the system as a whole. If a granular test fails, it only tells you which line of code doesn't work, which is much less important than understanding which business scenario doesn't work. It may happen that your imagined well-tested corner case is not reachable for business scenarios at all.  

To address these issues, it is important to test the behavior of the system rather than its implementation details. Instead of testing individual methods or classes in isolation, focus on testing the behavior of components or the entire business layer. This approach ensures that your tests are more resilient to changes in the implementation and provide valuable insights into the overall functionality of the system.

Wrong unit test example:
```java
public class OrderServiceTest {

    @Mock
    private InventoryService inventoryService;
    @Mock
    private EmailService emailService;
    
    @InjectMocks
    private OrderService orderService; 
    
    @Test
    void testPlaceOrder() {
        // given
        Order order = new Order(/* ... */);
        when(inventoryService.checkAvailability(order)).thenReturn(true);

        // when
        orderService.placeOrder(order);

        // then (verifies implementation details)
        verify(inventoryService).checkAvailability(order);
        verify(emailService).sendConfirmationEmail(order);
    }
}
```
Better unit test:

```java
public class OrderScenariosTest {

    private InMemoryInventoryRepository inventoryRepository = new InMemoryInventoryRepository();
    private InMemoryOrderRepository orderRepository = new InMemoryOrderRepository();
    private InMemoryEmpailService emailService = new InMemoryEmpailService();
    private OrderService orderService;
    
    @BeforeEach
    void init() {
      orderService = 
          new DefaultOrderService(
              new DefaultInventoryService(inventoryRepository),
              emailService,
              orderRepository
          );
    }
    
    @Test
    void testPlaceNewOrderWhenInventoryExists() {
      // given
      
      // setup inventory inventoryRepository.save(...)
      // setup other necessary state of a system
      // prepare input data
      Order order = new Order(/* ... */);
    
      // when
      orderService.placeOrder(order);
    
      // then (verifies behavior, i.e. that some state changed, some notifications sent, etc. )
      assertTnat(orderRepository.findById(order.getId())).isNotNull();
      assertThat(emailService.getNotifications())
              .satisfiesExactlyInAnyOrder(
                      email -> isEmailToOwner(email), 
                      email -> isEmailToBuyer(email)
              );
      // other verifications for the desired behavior
    }
}
```
However, JUnit framework is not the best choice for good unit tests. 
There are better alternatives like [Cucumber](https://cucumber.io/) or [Spock](https://spockframework.org/). 

## Write code from left to right, from top to bottom (for sinistrodextral human languages speakers)

Consistently writing code in a left-to-right, top-to-bottom manner enhances code readability and makes it easier to follow the logic of your program. It mirrors the natural way we read and understand languages, ensuring a seamless flow of comprehension.

Example of bad, right-to-left formatting:
```java
1 Stream.of("Hello", "World", "!")
2    .flatMapToInt(word -> word.chars()
3        .filter(ch -> ch == 'H')
4        .map(ch -> ch + 1)
5    )
```
In this example, operations on the characters (lines 3-4) are on the left side relative to the source of these characters (line 2). 
This can create a false impression that these operations are performed on the **word** itself, rather than **word.chars()**. 
When additional levels of enclosing functions are added, the complexity grows, potentially leading to confusion.

To avoid potential confusion and improve code readability, use a left-to-right, top-to-bottom formatting approach. 
Enclose operations consistently to align with their context and logical structure.
Good example:
```java
Stream.of("Hello", "World", "!")
    .flatMapToInt(word ->
        word.chars()
            .filter(ch -> ch == 'H')
            .map(ch -> ch + 1)
    )
```

In the example above, each operation is enclosed in a clear, nested structure, making it easier to comprehend the sequence of actions and their relationship to the source data.  
You might wonder why the word in `.flatMapToInt(word ->` is not moved to a new line. The reason is that when you call methods like `map`, `flatMap`, `fold`, `compose`, and others, you can usually deduce from the context that your first line of a multiline lambda works with a variable from your Stream or other source which you use. Therefore, adding one more level of indentation can be a bit excessive.

By adhering to the practice of writing code from left to right and from top to bottom, you enhance not only the readability of your code but also its understandability. The consistency in formatting guides developers through the logical flow of your code, leading to more effective collaboration and maintenance.

## Use named parameters

Surprised to hear this? Yes, you can indeed implement named parameters in Java! However, there are limitations to where you can apply them.

One excellent use case for named parameters is the builder pattern. Let's explore this with an example:

```java
Transaction.builder()
    // @formatter:off
    .with(tx -> {
        tx.transactionId = generateUniqueId();
        tx.sender = new User("Alice");
        tx.receiver = new User("Bob");
        tx.amount = calculateTransactionAmount();
    })
    // @formatter:on
    .build();
```
In this example, the named parameters in the builder pattern make the code much more readable and intuitive. Each property assignment is clearly labeled, allowing you to easily understand the intent of each line.

Now, compare the named parameter approach with the traditional constructor initialization:
```java
new Transaction(
    generateUniqueId(),
    new User("Alice"),
    new User("Bob"),
    calculateTransactionAmount()
)
```

In the constructor initialization example, it's less clear at a glance who is the sender and who is the receiver. The order of arguments might lead to confusion, especially when dealing with constructors that have multiple parameters.

Though named parameters may not be a universal feature in Java, they can be a powerful tool in certain contexts, such as the builder pattern. By employing named parameters, you improve code readability, reduce errors stemming from parameter order confusion, and enhance the overall clarity of your codebase.