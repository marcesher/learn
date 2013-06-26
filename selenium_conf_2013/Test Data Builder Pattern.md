problem: leaving around data after tests

some people solve it by creating sql script that's run when tests start

User u = UserBuilder.build()

u = UserBuilder.build().withName("marc").withPassword("hi");

hide all the stuff behind "build()"
 - api calls
 - rest calls
 - db lookups, filesystem lookups, etc


POINT: sensible defaults, extensible with with() methods, chaining

Delarative Example

Given
 When
 Then


Chain builders together

  - user builders as params to other builders

  IssueBuilder.withReporter( new UserBuilder()...build() )


Factories

