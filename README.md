# Formula

A simple and powerful library for building interactive forms in the terminal. Powered by [Bubble Tea](https://github.com/charmbracelet/bubbletea).

## Tutorial

Formula provides a straightforward interface to prompt users for input.

There are several `Question` types available to use:
* [`Input`](#input)
* [`Text`](#text)
* [`Select`](#select)
* [`MultiSelect`](#multiple-select)

```go
package main

import (
  "github.com/charmbracelet/formula"
)

type Response struct {
  Shell    string
  Base     string
  Toppings string
  Name     string
  Discount string
}

func main() {
  form := formula.NewForm().
    Group(
      formula.Label("Welcome to `Tacocat`!"),
      formula.Description("> The _best_ Taco shop + Pet store ever."),
      formula.Select().
        Title("Shell?").
        Option("Hard").
        Option("Soft"),
      formula.Description("> Note, **beans** are refried."),
      formula.Select().
        Title("Base").
        Option("Chicken").
        Option("Beef").
        Option("Fish").
        Option("Beans"),
    ).
    Group(
      formula.Description("Choose up to 4 toppings."),
      formula.MultiSelect().
        Title("Toppings").
        Options("Lettuce", "Tomatoes", "Corn", "Sour Cream", "Cheese").
        Filterable(true).
        Limit(4)
      formula.Description("Anything else?"),
      formula.Text().
        Title("Special Instructions").
        CharLimit(400),
    ).
    Group(
      formula.Label("# Discount"),
      formula.Input().
        Key("name").
        Title("What's your name?").
        Validate(formula.ValidateLength(0, 20)),
      formula.Confirm().
        Key("discount").
        Title("Would you like 15% off"),
    )

    var res Responses
    err := form.Run(&res)
    if err != nil {
      log.Fatal(err)
    }
}
```

## Input

`Input`s are single line text fields.

```go
formula.Input().
  Title("What's for lunch?").
  Validate(formula.ValidateLength(0, 20)).
  Prompt("?")
```

## Text

`Text`s are multi-line text fields.

```go
formula.Text().
  Title("Tell me a story.").
  Validate(formula.ValidateLength(100, 400)).
  Prompt(">").
  Editor(true) // open in $EDITOR
```

## Select

`Select`s are multiple choice questions.

```go
formula.Select().
  Title("Pick a country.").
  Option("United States").
  Option("Germany").
  Option("Brazil").
  Option("Canada").
  Cursor("→")
```

Alternatively,

```go
formula.Select().
  Title("Pick a country.").
  Options("United States", "Germany", "Brazil", "Canada").
  Cursor("→")
```

## Multiple Select

`MultiSelect`s are multiple choice questions but allow multiple selections.

```go
formula.MultiSelect().
  Title("Toppings.").
  Option("Lettuce").
  Option("Tomatoes").
  Option("Cheese").
  Option("Corn").
  Limit(4)
```


## Feedback

We'd love to hear your thoughts on this project. Feel free to drop us a note!

* [Twitter](https://twitter.com/charmcli)
* [The Fediverse](https://mastodon.social/@charmcli)
* [Discord](https://charm.sh/chat)

## Acknowledgments

`formula` is inspired by the wonderful [Survey][survey] library by Alec Aivazis.

[survey]: https://github.com/AlecAivazis/survey

## License

[MIT](https://github.com/charmbracelet/bubbletea/raw/master/LICENSE)

***

Part of [Charm](https://charm.sh).

<a href="https://charm.sh/"><img alt="The Charm logo" src="https://stuff.charm.sh/charm-badge.jpg" width="400"></a>

Charm热爱开源 • Charm loves open source • نحنُ نحب المصادر المفتوحة
