# Interfaces War of C23, C++23, Rust, Go 1.23, Zig and V
Interfaces War and Styles of C23 (FPs), C++23, Rust (Traits), Go 1.23, Zig and V with JavaScript (Node.js) analyzed.

This project will use a non-lanugage specific spec for an `interface API` and generate the language-specific interface constructs in the following languages to analyze their differences. The exception to pure construct of interfaces is C, Rust and Zig. C logical equivalent is a C `struct` with function pointers to dispatch the calls. Rust logical equivalent with signficant differences against its counterparts uses the `Trait` construct. Zig logical equivalent is .....


## The Reference Interface API

The following is the non-language specific interface API spec.

Interface Dispatcher

```C
 - dispatch_event(event: Event, src: Endpoint, dst: Endpoint) return Result 
 - dispatch_events(events: Event[], src: Endpoint, dst: Endpoint) return Result
 - dispatch_event(event: Event, src: Endpoint, dst: Endpoint, timeout: Ticker) return Result 
 - dispatch_event(events: Event[], src: Endpoint, dst: Endpoint, timeout: Ticker) return Result 
```


## C23 Interfaces (Function Pointers)

## C++23 Interfaces

## Rust Traits

## Go Interfaces

## Zig 

## V Interfaces

In `V` language to create V project issue the following.

```shell
v new <v-project-name> 
```

To create V `interfaces` project issue the followng.

```shell
v new interfaces
```
The resulting V project tree shows as follows.

```shell
interfaces
├── src
│   └── main.v
└── v.mod
```

To compile the project into .exe issue the following.

```shell
v .
```

V is totally trivial to create, compile and run projects.

To run the .exe issue the following.

```shell
./interfaces
```




