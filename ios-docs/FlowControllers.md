# Flow Controllers

## Handling navigation on iOS

There are two main approaches how we currently handle navigation on iOS:

1. **Segues**

2. **UINavigationController/UIViewController**

**Segues** introduce following constraints:

1. The need to use Storyboards and reflecting the application flow in them.
    
2. `prepareForSegue` function usually gets full of `if` statements to handle more
   complex navigation.

**UINavigationController/UIViewController** approach has a responsibility issue
-  ViewControllers should not be responsible for displaying other
ViewControllers. There is a missing component responsible for a navigation. See
[Improve your iOS Architecture with FlowControllers][] for more. Another good
example is a problem when we want to reuse a ViewController in different context
as seen in [Flow Controllers on iOS for a Better Navigation Control][].

## Responsible navigation

### VIPER The answer for having a component handling segues / transitions
between other modules is design pattern / architecture named **VIPER**. VIPER
stands for **V**iew **I**nteractor **P**resenter **E**ntity **R**outer where
***Router*** is responsible for navigation. ![VIPER
diagram](https://cdn-images-1.medium.com/max/1600/1*0pN3BNTXfwKbf08lhwutag.png)

The problem with VIPER architecture is that it is very complex and adds a lot of
boilerplate code in smaller projects. I recommend using VIPER for very large and
complex applications.

### MVVM + Flow Controllers
While developing apps who are not suitable for VIPER (small to mid applications)
an alternative approach is to use a design pattern / architecture known as MVVM.

#### MVVM
MVVM stands for **M**odel **V**iew **V**iew**M**odel. This design pattern helps to prevent **Massive ViewController** problem known from Apple's ***MVC***. This is done by the ***ViewModel*** layer which is UIKit independent representation of ***View*** and its state [[1][]]. In comparasion with VIPER, MVVM is less complex and can be used in even small to medium applications without adding a lot of overhead. 
![MVVM diagram](https://cdn-images-1.medium.com/max/1600/1*uhPpTHYzTmHGrAZy8hiM7w.png)

MVVM paradigm does not have a router component, as opposite to VIPER, thus the navigation happens in the ***View*** layer (see diagram). The missing piece is a 
component responsible for handling navigation events - Flow Controller.

#### Flow Controllers
The main purpose of Flow Controller is to configure ViewController for a specific context (eg. displaying grid or list layout, displaying VC as an overlay or fullscreen based on a device, etc.). It also provides all neccesary objects needed for ViewControllers purposes, thus reducing the need for Singletons. [[2]] The Flow Controller serves as a delegate for the ViewController and listens and handles events. An example application with Flow Controllers structure is shown on diagram below.

![Example app with Flow Controllers](https://github.com/enrian/docs/blob/master/ios-docs/img/FlowControllers.png)

1. Flow Controllers can have child controllers.
2. Flow Controller configures and coordinates different screens. 

When making a transition to a new ViewController, an adequate Flow Controller is created, and the ViewController gets configured by the Flow Controller. 

As a result, we have a tool how to make reusable and easily testable ViewControllers, coherent navigation throughout the project and simpler code injection and removal of singletons. [[2][]].

## Resources

[iOS Application Architecture
(talk)](https://academy.realm.io/posts/krzysztof-zablocki-mDevCamp-ios-architecture-mvvm-mvc-viper/)

[Coordinators Redux (blog post)](http://khanlou.com/2015/10/coordinators-redux/)

[Improve your iOS Architecture with FlowControllers (blog
post)](http://merowing.info/2016/01/improve-your-ios-architecture-with-flowcontrollers/)

[Flow Controllers on iOS for a Better Navigation Control (blog
post)](http://albertodebortoli.com/blog/2014/09/03/flow-controllers-on-ios-for-a-better-navigation-control/)

[Architectures in Swift (slides)](
https://drive.google.com/file/d/0B-z48z3RTavzYTN4Nmozcll5QWM/view?usp=sharing)

[iOS Architecture Patterns
(post)](https://medium.com/ios-os-x-development/ios-architecture-patterns-ecba4c38de52)

[Architecting iOS Apps with
VIPER](https://www.objc.io/issues/13-architecture/viper/)

[Introduction to MVVM](https://www.objc.io/issues/13-architecture/mvvm/)

[Improve your iOS Architecture with FlowControllers]:
http://merowing.info/2016/01/improve-your-ios-architecture-with-flowcontrollers/

[Flow Controllers on iOS for a Better Navigation Control]:
http://albertodebortoli.com/blog/2014/09/03/flow-controllers-on-ios-for-a-better-navigation-control/

[1]:https://medium.com/ios-os-x-development/ios-architecture-patterns-ecba4c38de52

[2]:http://merowing.info/2016/01/improve-your-ios-architecture-with-flowcontrollers/