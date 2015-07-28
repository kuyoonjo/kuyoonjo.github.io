---
layout: post
title:  "UI Bootstrap Dual State Navbar"
date:   2015-07-27 22:14:38
tags: [angularjs, javascript, ui-bootstrap]
---

This is an extension of [UI Bootstrap Navbar Affix][1]. See [demo][2].

[1]: /2015/07/27/UI-Bootstrap-Navbar-Affix.html
[2]: http://plnkr.co/NHPjLoVhbs7F987bC79G

Requirements:

- yc-navbar-affix
- Angular UI Bootstrap
- Bootstrap CSS(Only the css file)
- No JQuery required. Please make sure you are not using Bootstrap default javascript.

Usage:

- put [yc-navbar-affix] in your navbar tag.
- put [yc-navbar-affix-dual-state] in your navbar tag.
- set attributes template-url and template-url-affix

Code:

{% highlight javascript %}
/**
 * Created by yuchen on 7/24/15.
 */

angular.module('yc.navbar.affix.dual.state', [])
  .directive('ycNavbarAffixDualState', function($window) {
    return {
      restrict: 'A',
      template: '<div ng-include="templateUrl" ng-show="tplSwitch"></div>' +
        '<div ng-include="templateUrlAffix" ng-show="!tplSwitch"></div>',
      link: function(scope, element, attrs) {
        scope.tplSwitch = true;
        scope.templateUrl = attrs.templateUrl;
        scope.templateUrlAffix = attrs.templateUrlAffix;
        angular.element($window).bind('scroll', function() {
          scope.$apply(function() {
            if (scope.condition()) {
              scope.tplSwitch = false;
            } else {
              scope.tplSwitch = true;
            }
          });
        });
      }
    };
  });
{% endhighlight %}