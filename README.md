# DynamiData

A simple way to programmatically build data storage or queries.

## Intro

This project will target three languages: Javascript primarily, F# secondary, and C# as an extra.

For targeting Javascript we plan to use JSX syntax, for F# Elmish, and C# we will have to roll our own.

## Some examples
These are entirely likely to change and are purely illustrative of the idea of the project.

This could, for example, be used to build GraphQL queries, with something akin to the following:
```jsx
const query = (
  <graphQL variables={["mediatitle"]} search={["title", "$mediatitle"]}>
    <str>id</str>
    <num>avg_rating</num>
    <record tag="title">
      <str>full</str>
      <str>short</str>
      <str>native</str>
    </record>
  </graphQL>
);
const result = await query.execute(endpoint, {mediatitle: "Example title"});
```

And here is an example for the F# API:
```fs
open DynamiData // DynamiData.Json.etc

let serialiseBook (book: Book) =
  Json.record [
    "title", Json.str book.Title
    "author", Json.record [
        "name", Json.str book.Author.Name
        "age", Json.num book.Author.Age
      ]
  ]

let serialiseLibrary (library: Library) =
  Json.record [
    "name", Json.str library.Name
    "books", library.Books |> List.map serialiseBook
  ]

let json = localCommunityLibrary |> serialiseLibrary |> string
```
