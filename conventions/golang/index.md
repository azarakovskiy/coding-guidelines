## Overview

This document defines guidelines and conventions on our coding style. 

As a baseline, we rely on [Golang's conventions](https://golang.org/doc/code.html) and [recommendations](https://golang.org/doc/effective_go.html). 
Another very useful resource is a guideline for what to look for when [reviewing a pull request](https://github.com/golang/go/wiki/CodeReviewComments). 

Additionally, in _pricing team_ we have got few internal agreements on specific subjects that we should follow.

### Legend

🔴 : it is a **MUST** and it should be followed no matter what.

🟠 : it is a **SHOULD** and should be followed unless there is a very compelling reason not to do so.

🟢 : it is a **COULD** and it is good to consider.

There might be more than one guideline to address a category of problems. These guidelines will use a combination of 🟠 and 🟢 labels.

### Table of content

* [Project structure](#project-structure)
    * [Dependencies between `internal/app` and `internal/infra`](#dependencies)
    * [Dependency injection](#dependency-injection)
* [Code style](#code-style)
    * [Accept interfaces, return structs](#accept-interfaces)
    * [Method names](#method-names)

## Project structure {#project-structure}

We use [Canary service](https://github.com/taxibeat/canary-service) as a template for our microservices.
It includes our standard toolkit such as Go, Patron, Kafka, etc.

### Dependencies between `internal/app` and `internal/infra` {#dependencies}

Each project is roughly divided into two parts: `internal/app` and `internal/infra`. 

The former contains definitions of business models and interfaces, and also layers with business logic and definitions how different parts of the system interact with each other,
without concrete details of how individual components are implemented.

The latter contains specific implementation of these components, e.g. to save data to an SQL database or consume Kafka stream.

🔴 `internal/app` package must not import anything from `internal/infra`.

🟠 `internal/infra` should implement interfaces from `internal/app`.

### Dependency injection {#dependency-injection}

Since our `internal/app` package doesn't define which components' implementation it is using, we must do a dependency injection that defines it. 
The place for it is a file `internal/<app-name>.go`; it is called from `main.go`. 
It defines a single method that couples all the parts of an application together and makes sure to import interfaces and packages, and setup final dependencies.

```
├── internal/
│   ├── <app-name>.go
│   ├── app/
│   └── infra/
```

🔴 Dependency injection must happen in `internal/<app-name>.go`.

## Code style {#code-style}

### Accept interfaces, return structs {#accept-interfaces}

To decouple implementations from interfaces and help testing, it is advised that your methods accept interfaces and parameters but return concrete struct.
More clarification you can find [here](https://medium.com/@cep21/what-accept-interfaces-return-structs-means-in-go-2fe879e25ee8)

🟠 Methods should accept interfaces but return structs.

### Method names {#method-names}

As per Go's convention, naming should be _short, concise, evocative_. There is no sense to repeat the name of a package or add any obvious information. 
Prefer having `httpclient.New()` to `httpclient.NewHttpClient()`, or `rule.NewClient()` and `rule.NewService()` to `rule.NewRuleClient()` and `rule.NewRuleService()`.
Yet, try not to drop any useful information from a name if it clearly helps reading the code (e.g. when there are client and a service in a single package, it is advised to separate their constructors).

🔴 Don't repeat package name in your method name.

🟠 Don't drop any useful non-repetitive information from a method name.

```
package rule
 
func NewClient() {  // OK
}

func New() { // Might be NOT OK, not clear what it returns, 
	         // also possibly clashes with a rule.Service if exists
}

func NewRuleClient() { // NOT OK, repeats package name
}
```

but 

```
package httpclient

func New() { // OK
}

func NewClient() { // NOT OK, repeats package name
}

func NewHttpClient() { // NOT OK, repeats package name
}
```

Home reading on better naming can be found [here](https://golang.org/doc/effective_go.html#names).
