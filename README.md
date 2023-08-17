# Good Things - Bad Things: A Cookbook for Java Developers

<!-- TOC -->
* [Good Things - Bad Things: A Cookbook for Java Developers](#good-things---bad-things-a-cookbook-for-java-developers)
  * [Introduction](#introduction)
  * [Avoid creating custom frameworks unless you have person-years of free resources](#avoid-creating-custom-frameworks-unless-you-have-person-years-of-free-resources)
  * [Avoid Using XML](#avoid-using-xml)
  * [Avoid overusing private methods](#avoid-overusing-private-methods)
  * [Prefer declarative style over imperative one](#prefer-declarative-style-over-imperative-one)
  * [Use Static Imports for Static Declarative APIs](#use-static-imports-for-static-declarative-apis)
  * [Test behaviour, not implementation.](#test-behaviour-not-implementation-)
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

1. Resource intensive and complex  
Developing a custom framework demands significant investments of time, effort, and resources. Crafting an effective framework requires a deep understanding of software architecture, design patterns, and scalability principles. Additionally, creating a comprehensive solution that addresses various scenarios and edge cases introduces complexity that's often underestimated.

1. Maintenance burden and opportunity cost   
Once the custom framework is in place, ongoing maintenance becomes a substantial commitment. This includes fixing bugs, implementing updates, and ensuring compatibility as technology evolves. The time and resources devoted to maintaining the framework can divert attention from other critical aspects of your project, impacting its core goals.

1. Bad documentation   
Thorough documentation is crucial for any successful tool, and custom frameworks are no exception. Crafting clear and comprehensive documentation takes considerable effort. Poor documentation can lead to confusion, frustration, and inefficiencies among your team members, hindering adoption and usability.

1. Learning curve for the team  
Introducing a custom framework requires your development team to invest time in learning its intricacies. This learning curve impacts productivity, as developers adapt to new workflows and practices. Not all team members might grasp the new tool at the same pace, potentially leading to skill disparities and resistance to change.

Consider the [Spring Framework](https://github.com/spring-projects/spring-framework), a Java framework established in 2004. With 754 contributors and over 27,600 commits, this framework's success story illustrates the value of long-term commitment and extensive collaboration. It showcases that even with significant resources and community support, a framework is an ongoing endeavor, continually evolving to meet changing needs.

In conclusion, the decision to build a custom framework should be approached cautiously. Unless you have person-years of free resources to invest in development, maintenance, and documentation, leveraging well-established solutions like the Spring Framework is often more pragmatic. The complexities of framework development, coupled with the challenges of documentation and team learning, make opting for existing solutions a wise choice for most projects. Remember that simplicity and efficiency are often found not in building everything from scratch, but in leveraging the wisdom of the broader development community.

**True stories (directed by Robert B. Weide)**  
Actors:  
Framework Supplier (FS): The developer who creates the framework.  
Framework Consumer (FC): The developer who utilizes the framework for daily tasks.  

Story 0:   
FC: This component is useless for our use case. Could you please ensure components work with real-life examples?   
FS: We've tested it in our sandbox. It's your job to use it in real-life scenarios.    

Story 1:   
FS: Due to limited capacity, troubleshooting the framework is now your responsibility, FC.   
FC: Fuuuuu!  

Story 2:  
FC: (_Glancing at our tiny, chaotic, and poorly organized documentation, often lacking examples and sometimes even absent_) The documentation for our framework feels like fluffware.  
FS: From our perspective, it's comprehensive and valuable. If you find details lacking, create tickets to address them.  
FC: (Mentally comparing our documentation with mature open-source frameworks) I meant the documentation as a whole.  
FS: If you believe something is missed, create tickets. Goodbye.  


## Avoid Using XML

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

Here are the main pitfalls:  
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
The typical declarative API in Java is the Java util Stream API.

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

**Why declarative is preferred**   
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
Now, let's attempt to translate both examples into plain English:  
* Stream of 1, 2, 3, sorted Comparator comparing String length, collect Collectors to list.
* Stream of 1, 2, 3, sorted comparing String length, collect to list.   
The difference becomes clearer. The first sentence doesn't make much sense, while the second one is a proper English sentence.
By using static imports for static methods, you're not only writing cleaner code but also crafting code that speaks a language closer to everyday conversation. This practice not only enhances readability but also demonstrates your expertise in utilizing the full potential of Java's declarative APIs.

## Test behaviour, not implementation. 
A prevalent misconception exists that unit tests should mock virtually all dependencies and scrutinize each class and method in isolation. While this approach is appropriate for testing library or utility functions, it can have detrimental effects when applied to testing business logic.

But what exactly are unit tests meant to achieve? Their purpose is to guarantee that your code retains functionality throughout refactoring or the introduction of new features. If you find yourself modifying code and needing to adjust tests to accommodate the new implementation, these tests become counterproductive. Worse still, they result in duplicated efforts. In simpler terms, rather than facilitating refactoring, such tests impede it.  

Wrong unit test example:
...

