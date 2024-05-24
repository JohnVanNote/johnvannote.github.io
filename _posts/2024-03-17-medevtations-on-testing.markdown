---
layout: post
title:  "Medevtations on Testing"
date:   2024-03-17
categories: testing
---

Earlier in my career I focus on unit testing and strived for the elusive 100% code coverage. I even when to far as Unit testsing accessors (getters) and mutators (setters) and wrote test only implementations of interfaces or abstract classes to test the default methods. This was a completely unnecessary use of code coverage, but I want to set the stage for how I did it at that time.

For context, most of my professional work deals with Spring boot applications. Spring boot applications follow the common MVC pattern. With the Controller representing the, well, controller, the JPA entity representing the model, and the view representing whatver

{% highlight java %}
class MedevtationController {

  private final MedevtationService medevtationService;

  @GetMapping(path = "/medevtation")
  MedevtationResponse retrieveMedevtation(@RequestParam Long id) {
    return medevtationService.goAndDoTheServicePart(id);
  }
}
{% endhighlight %}

{% highlight java %}
class MedevtationService {

  private final MedevtationDao medevtationDao;

  MedevtationResponse goAndDoTheServicePart(Long id) {
    final Medevtation medevtation = medevtationDao.loadById(id);
    return new MedevtationResponse(medevtation.getImportantField());
  }
}
{% endhighlight %}