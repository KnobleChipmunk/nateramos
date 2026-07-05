+++
title = 'Notes on the Platform Rebuild'
date = 2025-03-10
draft = false
series = ['platform-rebuild']
+++

Placeholder post added alongside the projects section so the series
cross-link between blog posts and portfolio projects has something real to
point at. See the ["Example Data Platform Migration"](/projects/example-project/)
project for the full write-up this post accompanies.

Notes from partway through the migration: the incremental cutover approach
(running old and new pipelines side by side and diffing output) caught several
edge cases in currency rounding that would have otherwise shipped silently.
