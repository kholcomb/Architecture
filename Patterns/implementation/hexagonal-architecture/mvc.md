---
name: Model-View-Controller
category: implementation/hexagonal-architecture
also-known-as: [MVC]
tags: [separation-of-concerns, ui-pattern, web, desktop, request-response]
parent: hexagonal-architecture
related: [mvvm, model-view-presenter, clean-architecture, hexagonal-architecture]
source: https://github.com/denyspoltorak/metapatterns/wiki/Hexagonal-Architecture
---

## Summary
Model-View-Controller separates an application into three interconnected components: the Model (data, business rules, and state), the View (UI presentation and rendering), and the Controller (receives user input, updates the Model, and selects the View to render). The Controller mediates between the other two, keeping presentation logic out of the Model. MVC is the most widely adopted pattern for web and desktop UI frameworks, appearing in Rails, Django, Spring MVC, ASP.NET MVC, and many others.

## When To Use
- Building web or desktop applications where separating UI from business logic provides clear value
- Using a framework that enforces or encourages MVC conventions (Rails, Django, Laravel, Spring MVC)
- The team needs a well-understood, widely documented structure that simplifies onboarding
- Request-response interaction models map naturally to the Controller's input-handling role

## When To Avoid
- The UI is highly reactive and data-binding-driven — MVVM or reactive architectures fit better
- The View must update frequently from model changes without user input — MVP or MVVM reduces coupling
- The application has no meaningful UI (batch jobs, microservices) — MVC adds structure with no benefit
- Business logic is complex enough to warrant domain isolation — Clean Architecture or Hexagonal provides stronger boundaries

## Pros and Cons

* Good, because the separation of Model, View, and Controller makes each component independently testable
* Good, because the pattern is universally understood, lowering onboarding costs for new team members
* Good, because most web frameworks provide MVC scaffolding, reducing boilerplate and convention decisions
* Bad, because Controllers tend to accumulate business logic over time, becoming fat controllers that violate separation of concerns
* Bad, because the View and Controller are often tightly coupled in practice, making View-layer testing difficult
* Bad, because the pattern does not prescribe how to structure complex domain logic, leading to inconsistent model layers

## Evolutions
- **From:** Procedural UI code (introduce separation of concerns between data, presentation, and input handling)
- **To:** MVP (make the View fully passive and move all UI logic to the Presenter), MVVM (replace Controller with data-bound ViewModel for reactive UIs), Clean Architecture (add explicit layer boundaries and dependency inversion around the Model)
