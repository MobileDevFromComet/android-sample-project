# ViewModel

ViewModel is a class that is responsible for preparing and managing the data for an Activity or a Fragment. 

A ViewModel is always created in association with a scope (an fragment or an activity) and will be retained as long as the scope is alive. 
E.g. if it is an Activity, until it is finished.

In other words, this means that a ViewModel will not be destroyed if its owner is destroyed for a configuration change (e.g. rotation). 
The new instance of the owner will just re-connected to the existing ViewModel.

The purpose of the ViewModel is to acquire and keep the information that is necessary for an Activity or a Fragment. The Activity or the Fragment should be able to observe changes in the ViewModel. ViewModels usually expose this information via LiveData or Android Data Binding. You can also use any observability construct from you favorite framework.

ViewModel's only responsibility is to manage the data for the UI. It should never access your view hierarchy or hold a reference back to the Activity or the Fragment.

![Viewmodel Diagram](https://github.com/TrustyCars/android-sample-project/blob/main/readme/images/android_architecture_presentation.png)
*Figure: Diagram of Viewmodel in app architecture(from developer.android.com)* 

## How to use
In normal cases, there should be only one viewmodel for one **activity/fragment**. Viewmodels should not be shared among different activities/fragments. 

**Special case** 

Although we need to follow above rule normally, there might be a case to use viewmodel in component level. Which mean lifecycle of viewmodel will be tied to activity. 
You can take Login component as an example. The whole component actually has only one purpose which is to verify user and register if it is new user. And you have to pass data and handle it back and forth within component. To save from that nightmare, we can just simply use viewmodel in component level.


## Naming Convention
For naming, viewmodel has to follow the view class. It should starts with an uppercase letter and use camel case. 

```
class DetailFragment {
  ...
}

class DetailViewModel
: ViewModel() {
  ...
}
```

*For special case, format should be 
` {Component Name}ComponentViewModel `
e.g. LoginComponentViewModel*


# Exposing data to View
We use StateFlow for states and SharedFlow for events

Reference
https://developer.android.com/kotlin/flow/stateflow-and-sharedflow

# How to access data
To request data from viewmodel, it'll always have to go through domain layer. Usecases in our case. 
Since we have to support for multiple countries, it is the best to use domain layer. You might find using repository directly. They are from old codes. We will refactor them components by components. As for the new features, it has to follow this format. 
