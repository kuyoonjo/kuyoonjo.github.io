---
layout: post
title:  "UI Bootstrap Navbar Affix"
date:   2015-07-27 22:14:38
tags: [angularjs, javascript, ui-bootstrap]
---

This post is for lads who do not want to use JQuery with AngularJS for some conflict issues. If you persist in JQuery, I suggest a JQuery solution [here][1]. The [demo][2] is hosted on [Plunker][3].

[1]: http://www.sitepoint.com/understanding-bootstraps-affix-scrollspy-plugins/
[2]: http://plnkr.co/KsWsRHWCyQ5UWATacbS6
[3]: http://plnkr.co

Requirements

- Angular UI Bootstrap
- Bootstrap CSS(Only the css file)
- No JQuery required. Please make sure you are not using Bootstrap default javascript.

Usage:

- put `yc-navbar-affix` in your navbar tag.

Code: 

{% highlight javascript %}
/**
 * Created by yuchen on 7/24/15.
 */

angular.module('yc.navbar.affix', [])
  .directive('ycNavbarAffix', function($window) {
    return {
      restrict: 'A',
      link: function(scope, element, attrs) {
        var orignOffsetTop = element[0].offsetTop;
        scope.condition = function() {
          return $window.pageYOffset > orignOffsetTop;
        };

        angular.element($window).bind('scroll', function() {
          scope.$apply(function() {
            if (scope.condition()) {
              angular.element(element).addClass('navbar-fixed-top');
            } else {
              angular.element(element).removeClass('navbar-fixed-top');
            }
          });
        });
      }
    };
  });
{% endhighlight %}