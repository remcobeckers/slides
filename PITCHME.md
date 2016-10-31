#Hello

#HSLIDE

##Second larges
###Third largest

#HSLIDE?image=img/autumn.jpg

##Autumn

#HSLIDE

###Now it's time for some code

#VSLIDE

Parsing git repositories listing

```scala
import io.circe._, io.circe.parser._
import scalaj.http._

val jsText  = Http("https://api.github.com/repositories?since=0").asString.body
val json = parse(jsText).getOrElse(Json.Null)

json.hcursor.focus.asArray.map(
          for {
            repo <- _
            c    =  repo.hcursor
            id   <- c.get[Long]("id").toOption
            name <- c.get[String]("full_name").toOption
          } yield (id, name))
```
