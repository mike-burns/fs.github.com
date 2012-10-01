# Cucumber best practices

## Organization

Group steps by model. We’ve found the best way to keep track of them is to group
them by the primary model they affect. Some steps may affect multiple models,
but usually there is an obvious choice.

Put each feature in it’s own file. Don’t be afraid to put features in subdirectories.
For any large app, it’s almost essential.

Keep the file organized grouping the steps by Given / When / Then.

## Custom steps make your scenario DRY and accessible

Scenarios should have the same lifecyle as your code: Red, Green, Refactor to make
them DRY and easy to read.

## Background: setup the DRY way

Make the feature focus on one business object/action/context and the background
will get longer than the scenarios.

Use `Background` to consolidate common steps in a feature.

## Tags

You can use `@webmock` for enabling webmock functionality around some scenario. It's mean all real HTTP connection will be
disabled in the given scenario and you need to stub them with stub_request.

Checkout also:

* http://collectiveidea.com/blog/archives/2010/09/09/practical-cucumber-factory-girl-steps/
* http://collectiveidea.com/blog/archives/2010/09/13/practical-cucumber-organization/
* http://eggsonbread.com/2010/09/06/my-cucumber-best-practices-and-tips/
* http://github.com/aslakhellesoy/cucumber/wiki/Tutorials-and-Related-Blog-Posts
