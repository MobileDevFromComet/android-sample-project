## Presentation Mapper

The purpose of the mapper is to convert domain object to list of UIModels to represent data in the presentation layer. 
If you don't know about UIModel, please read it [here](https://github.com/TrustyCars/android-sample-project/blob/main/readme/presentation/model.md). 

We have an **ModelMapper** interface for this. So, for our sample in Buy page. 

```
class BuyIndexUIMapper @Inject constructor() : ModelMapper<BuyIndex?, MutableList<BuyIndexUIModel>> {

  override fun map(entity: BuyIndex?): MutableList<BuyIndexUIModel> {
      // check data and return list of UIModel
     
  }
  
}
```
