---
layout: post
title: Improve AngularJS Form Experience
---

It may sound odd to discuss and write about AngularJS 1.x when Angular 4 do exists in the market. But hey, AngularJS is still amazing framework. No doubt. This post documents how I improved the overall UX of modifying data in Angular Form using `ng-model-options`.

<!--more-->

I was asked to create a new page that enables user to modify tabular data and save it back to db. It was actually very easy to create a form that does the job. I wrote a quick basic code that loads data on `$scope` for the supplied `record id`. We all know, two way binding behviour of `Angular JS`, anything you update on view will reflect on its `$scope` on controller.

I wanted to provide `Reset` button.