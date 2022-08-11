# android-sample-project
This is sample app to standardise code structure for android projects in Carro. 


# Objectives
- Features should be able to controlled with Flag 
- Features can be vary base on country
- Business logic for features should depend on the country
- Need to support for Localization 
- Architecture has to be testable and clean
- Support Dark theme
- Follow strictly for PDS(Product Design System)

# Architecture
The architecture is built around Android Architecture Components and follows the recommendations laid out in the Guide to App Architecture. Logic is kept away from Activities and Fragments and moved to ViewModels. Data is observed using Kotlin Flows and the View Binding Library binds views to have an ID for the layout's views.

The Repository layer handles data operations. Repository modules are responsible for handling all data operations and abstracting the data sources from the rest of the app.

A lightweight domain layer sits between the data layer and the presentation layer, and handles discrete pieces of business logic off the UI thread. See the .\*UseCase.kt files under shared/domain for examples.

The Navigation component is used to implement navigation in the app, handling Fragment transactions and providing a consistent user experience.

Room is used for saving configuration of the app.

UI tests are written with Espresso and unit tests use Junit4 with Mockito when necessary.

# Design
[Design Screenshots](https://github.com/TrustyCars/android-sample-project/tree/main/design)

# Tech
- MVVM
- Hilt
- Room
- Couroutine
- Paging
- List Adapter
- Navigation
- Kotlin DSL
- Benchmarking


## App Structure
  - di
    - {modules}
  - data
    - model
    - remote
      - api
        - {ApiService}
    - repository
      - {RepositoryImpl}
  - domain
    - model
    - repository
    - usecase
  - presentation
    - feature1
      - adapter 
      - [mapper](https://github.com/TrustyCars/android-sample-project/blob/main/readme/presentation/mapper.md)
      - [model](https://github.com/TrustyCars/android-sample-project/blob/main/readme/presentation/model.md)
      - viewholder
      - [viewmodel](https://github.com/TrustyCars/android-sample-project/blob/main/readme/viewmodel.md)
      - {Fragments/Activity}
    - feature2
  - utils
