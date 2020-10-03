+++
title = "Lessons I've Learned in Tech"
date = "2020-10-03T14:39:37-07:00"
author = "Erik Goodman"
categories = ["Software"]
tags = ["software development"]
lastmod = "2020-10-03"
+++

# Lessons I've Learned in Tech

This page is an ongoing set of lessons that I consider important during my career in technology.

**1. Strangle; Don't Rewrite.** 
When considering rewriting a legacy application, it is often better to approach the rewrite piecemeal rather than all at once. Start the "rewrite" one feature at a time and transition users to the new implementation as individual components become available rather than attempting a feature-parity implementation in parallel with on-going support for the legacy app. If it's important enough to rewrite it is likely important enough to maintain and extend which will make it impossible to ever reach feature-parity.  

Key takeaway: progressively delete the old code base in favor of a new one.  

Resources
- https://martinfowler.com/bliki/StranglerFigApplication.html
- https://paulhammant.com/2013/07/14/legacy-application-strangulation-case-studies/
- https://understandlegacycode.com/blog/avoid-rewriting-a-legacy-system-from-scratch-by-strangling-it/ 
