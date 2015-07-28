---
layout: post
title:  "AngularJS Sticky Footer"
date:   2015-07-27 22:14:38
tags: [angularjs, javascript]
---

This is a pure angularjs sticky footer. No CSS or JQuery is required. 
See [demo][1].

Usage: 

- Add `'yc.stickyfooter'` to your module.
- Add `yc-sticky-footer` directive to your html body tag
- (Optional) Set the attribute `offset` to your html body tag
- Add `ng-style="footer"` to your footer tag

Algorithm:

- Compare window's height(`hw`) and the document's heigh(`hd`)
- Put the footer to bottom when `hw` is greater than `hd`.

Code:

{% highlight javascript %}
/**
 * Created by yuchen on 7/24/15.
 */

angular.module('yc.stickyfooter', [])
  .directive('ycStickyFooter', function($window) {
    return {
      restrict: 'A',
      scope: true,
      link: function(scope, element, attrs) {
        // Get the heights
        scope.heights = function() {
          return {
            window: $window.innerHeight,
            body: element[0].offsetHeight
          };
        };
        
        // Set the offset. It is optional. Generally leave it blank.
        var offset = attrs.offset || 0;
        
        // Relocate the footer.
        var setFooter = function() {
          if (scope.windowHeight > scope.bodyHeight + offset) {
            scope.footer = {
              position: 'absolute',
              bottom: 0
            };
          } else {
            scope.footer = {};
          }
        };

        // Watch the heights
        scope.$watch(scope.heights, function(newValue, oldValue) {
          scope.windowHeight = newValue.window;
          scope.bodyHeight = newValue.body;
          setFooter();
        }, true);

        // Add the listener
        angular.element($window).bind('resize', function() {
          scope.$apply();
        });
      }
    };
  });
{% endhighlight %}

[1]: http://embed.plnkr.co/mNo27DZQX9CSVG59dqB8/preview
