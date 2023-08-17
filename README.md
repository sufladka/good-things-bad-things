# Good Things - Bad Things: A Cookbook for Java Developers

<!-- TOC -->
* [Good Things - Bad Things: A Cookbook for Java Developers](#good-things---bad-things-a-cookbook-for-java-developers)
  * [Introduction](#introduction)
  * [Avoid creating custom frameworks unless you have person-years of free resources](#avoid-creating-custom-frameworks-unless-you-have-person-years-of-free-resources)
  * [Avoid Using XML](#avoid-using-xml)
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



## Test behaviour, not implementation. 
A prevalent misconception exists that unit tests should mock virtually all dependencies and scrutinize each class and method in isolation. While this approach is appropriate for testing library or utility functions, it can have detrimental effects when applied to testing business logic.

But what exactly are unit tests meant to achieve? Their purpose is to guarantee that your code retains functionality throughout refactoring or the introduction of new features. If you find yourself modifying code and needing to adjust tests to accommodate the new implementation, these tests become counterproductive. Worse still, they result in duplicated efforts. In simpler terms, rather than facilitating refactoring, such tests impede it.  

Wrong unit test example:
...

