Helo 

Kotlin builder install

HtBuilder   Kotlin Builder Android Studio  Compenents catagori

basic  norm

`plugins {
    id("com.google.devtools.ksp")
}`  

or implementation install

`dependencies {
    implementation("com.htstudio:htbuilder-annotations:1.0.7")
    ksp("com.htstudio:htbuilder-processor:1.0.7")
}`


object or data 

`import com.htstudio.builder.Builder
@Builder
data class RequestData(
    var id: Int = 0,
    var action: String? = null,
    var payload: Any? = null
){
    companion object // Bu satırı ekleyin
}`


System go 

`     val requestset = RequestData.builder().id(52).action("URL").payload(object).build()
`
