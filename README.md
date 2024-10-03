# Interfaces War of C23, C++23, Rust, Go 1.23, Zig and V
Interfaces War and Styles of C23 (FPs), C++23, Rust (Traits), Go 1.23, Zig and V with JavaScript (Node.js) analyzed.

This project will use a non-lanugage specific spec for an `interface API` and generate the language-specific interface constructs in the following languages to analyze their differences. The exception to pure construct of interfaces is C, Rust and Zig. C logical equivalent is a C `struct` with function pointers to dispatch the calls. Rust logical equivalent with signficant differences against its counterparts uses the `Trait` construct. Zig logical equivalent is .....


## The Reference Interface API

The following is the non-language specific interface API spec.

**Interface Dispatcher**

```C
 - dispatch_event(event: Event, src: Endpoint, dst: Endpoint) return Result 
 - dispatch_events(events: Event[], src: Endpoint, dst: Endpoint) return Result
 - dispatch_event(event: Event, src: Endpoint, dst: Endpoint, timeout: Ticker) return Result 
 - dispatch_event(events: Event[], src: Endpoint, dst: Endpoint, timeout: Ticker) return Result 
```


## C23 Interfaces (Function Pointers)

C does NOT have traditional `interface` language construct and as it provides a logical equivalent through the the use of the a C `struct` containing API spec `function pointers`. This struct serves a `v-table` like a C++ struct or class that contains `pure virtual API`.

The C spec for this Dispatcher interface is as follows.

```C
#include <stdio.h>
#include <time.h>

typedef struct Event {
    int id;
} Event;

typedef struct Endpoint {
    char address[100];
} Endpoint;

typedef struct Result {
    int status;
} Result;

typedef struct Ticker {
    struct timespec duration;
} Ticker;

// Dispatcher Interface using function pointers
typedef struct Dispatcher {
    Result (*dispatch_event)(struct Event, struct Endpoint, struct Endpoint);
    Result (*dispatch_events)(struct Event*, size_t, struct Endpoint, struct Endpoint);
    Result (*dispatch_event_with_timeout)(struct Event, struct Endpoint, struct Endpoint, struct Ticker);
    Result (*dispatch_events_with_timeout)(struct Event*, size_t, struct Endpoint, struct Endpoint, struct Ticker);
} Dispatcher;

Result dispatch_event_impl(struct Event event, struct Endpoint src, struct Endpoint dst) {
    // implementation
    Result result = { .status = 0 }; // success
    printf("Dispatching event with ID %d from %s to %s\n", event.id, src.address, dst.address);
    return result;
}

Result dispatch_events_impl(struct Event* events, size_t count, struct Endpoint src, struct Endpoint dst) {
    // implementation
    Result result = { .status = 0 }; // success
    for (size_t i = 0; i < count; ++i) {
        printf("Dispatching event with ID %d from %s to %s\n", events[i].id, src.address, dst.address);
    }
    return result;
}

// Assigning function implementations to the Dispatcher struct
Dispatcher create_dispatcher() {
    Dispatcher dispatcher = {
        .dispatch_event = dispatch_event_impl,
        .dispatch_events = dispatch_events_impl,
        .dispatch_event_with_timeout = NULL, // implement as needed
        .dispatch_events_with_timeout = NULL // implement as needed
    };
    return dispatcher;
}

int main() {
    Dispatcher dispatcher = create_dispatcher();
    struct Event event = { .id = 1 };
    struct Endpoint src = { .address = "Source" };
    struct Endpoint dst = { .address = "Destination" };

    dispatcher.dispatch_event(event, src, dst);
    return 0;
}
```

## C++23 Interfaces

C++ does NOT have traditional `interface` language construct and as it provides a logical equivalent through the the use of the a C++ `struct` or `class` that contains `virtual functions` . This declaration of the virtual functions generates a `v-table` that is indexed to the correct descendant at run-time to satisfy the call.

```C++
#include <iostream>
#include <vector>
#include <chrono>

struct Event {
    int id;
};

struct Endpoint {
    std::string address;
};

struct Result {
    int status;
};

using Ticker = std::chrono::steady_clock::duration;

// Interface (Abstract class) Dispatcher
class Dispatcher {
public:
    virtual Result dispatch_event(const Event& event, const Endpoint& src, const Endpoint& dst) = 0;
    virtual Result dispatch_events(const std::vector<Event>& events, const Endpoint& src, const Endpoint& dst) = 0;
    virtual Result dispatch_event_with_timeout(const Event& event, const Endpoint& src, const Endpoint& dst, Ticker timeout) = 0;
    virtual Result dispatch_events_with_timeout(const std::vector<Event>& events, const Endpoint& src, const Endpoint& dst, Ticker timeout) = 0;
};

// Concrete implementation of Dispatcher
class EventDispatcher : public Dispatcher {
public:
    Result dispatch_event(const Event& event, const Endpoint& src, const Endpoint& dst) override {
        std::cout << "Dispatching event with ID " << event.id << " from " << src.address << " to " << dst.address << "\n";
        return { 0 }; // success
    }

    Result dispatch_events(const std::vector<Event>& events, const Endpoint& src, const Endpoint& dst) override {
        for (const auto& event : events) {
            std::cout << "Dispatching event with ID " << event.id << " from " << src.address << " to " << dst.address << "\n";
        }
        return { 0 }; // success
    }

    Result dispatch_event_with_timeout(const Event& event, const Endpoint& src, const Endpoint& dst, Ticker timeout) override {
        std::cout << "Dispatching event with timeout...\n";
        return { 0 }; // success
    }

    Result dispatch_events_with_timeout(const std::vector<Event>& events, const Endpoint& src, const Endpoint& dst, Ticker timeout) override {
        std::cout << "Dispatching events with timeout...\n";
        return { 0 }; // success
    }
};

int main() {
    EventDispatcher dispatcher;
    Event event{ 1 };
    Endpoint src{ "Source" };
    Endpoint dst{ "Destination" };
    dispatcher.dispatch_event(event, src, dst);

    return 0;
}
```

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




