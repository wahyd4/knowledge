# Kotlin

## Some tips

### Builder mode in kotlin

```kotlin
class Car(
  val model: String?,
  val color: String?,
  val type: String?) {

    data class Builder(
      var model: String? = null,
      var color: String = "pink",
      var type: String? = null) {

        fun model(model: String) = apply { this.model = model }
        fun color(color: String) = apply { this.color = color }
        fun type(type: String) = apply { this.type = type }
        fun build() = Car(model, color, type)
    }
}
//use
val car = Car.Builder()
  .model("Ford Focus")
  .color("Black")
  .type("Type")
  .build()
```
Based on [stackoverflow](https://stackoverflow.com/questions/36140791/how-to-implement-builder-pattern-in-kotlin)
