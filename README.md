# elm-http

Make HTTP requests in Elm.

The `Http` module aims to cover some of the most common cases of requesting
JSON data, but also have lower-level functions such that the API covers all
of the underlying functionality.

## Example

```elm
import Http
import JavaScript.Decoder as JS exposing ((:=))
import Promise exposing (..)


lookupZipCode : String -> Promise Http.Error (List String)
lookupZipCode query =
    Http.get places ("http://api.zippopotam.us/us/" ++ query)


places : JS.Decoder (List String)
places =
  let place =
        JS.object2 (\city state -> city ++ ", " ++ state)
          ("place name" := JS.string)
          ("state" := JS.string)
  in
      "places" := JS.list place
```