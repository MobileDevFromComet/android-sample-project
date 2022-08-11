## Presentation Model

This model is sorely for presenetation layer only. Normally, if we have to build an detail page, we put all UI together in a page and handle it base on the object coming from domain layer. In our app, all different components become a viewholder that will be populated by the recyclerview's adapter. We can reuse some views in this way. 

Let take a look at this sample image

[Sample Buy Page](https://github.com/TrustyCars/android-sample-project/blob/main/readme/images/buy_page_sample.png)

According to the screen, we can split into five different components. They can be headers, Recommended cars(For You), Find perfect match banner, top brands and popular cars. So, we can define view types like this

```
enum class BuyIndexViewType {
  Header,
  RecommendedCars,
  FindPerfectMatchBanner,
  TopBrands,
  PopularCars
}
```

But popular cars and recommended cars are very similar, we can use same viewtype for them. So, this is the outcome after the update.

```
enum class BuyIndexViewType {
  Header,
  Cars,
  FindPerfectMatchBanner,
  TopBrands
}
```

Now we have our viewtypes. To use them with our adapter, we must define our base model. This is our base UIModel for the buy page.

```
abstract class BuyIndexUIModel {
  abstract var viewType: BuyIndexViewType
}
```

For the Header type, we just need an UIModel with its viewtype. 

```
class BuyIndexHeaderUIModel: BuyIndexUIModel {
  override var viewType: BuyIndexViewType = Header
}
```

For the Cars type, we need list of cars and title since we are reusing. 
```
data class BuyIndexCarsUIModel: BuyIndexUIModel(
  val title: String,
  val cars: List<Car>
){
  override var viewType: BuyIndexViewType = Cars
}
```

For Top Brands type, we need a list of car models
```
data class BuyIndexCarsUIModel: BuyIndexUIModel(
  val models: List<CarModel>
){
  override var viewType: BuyIndexViewType = Cars
}
```

And so on for the rest of the view types. Basically, we can use those UIModel view types as adapter view types well. Just need to return `UIModel.Item.ordinal` for the adapter view type and check with that in creating viewholder and binding viewholder. 
