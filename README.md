# RemoteTimeSource-TS

A RemoteTimeSource provides a simple API for working with remote Time Sources.
Calls to RemoteTimeSource return Time related artifacts that mimic the underlying remote server's time.

Example Usage:
```
Date.now()
> 1586022512

let timesource = new RemoteTimeSource({
	domain: "somedomain.com",
	provider: remoteTimeProviders.fetch,
	interval: 500,
})
timesource.now()
> 1586023636

timesource.delta()
> 1124
```

# Overview
A RemoteTimeSource attempts to model a remote system's time.
This is done using [Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol).
The time source will repeatedly sync with the remote time source to try to accurately model the remote time.

When a RemoteTimeSource is constructed it requires an object of type Settings.
These settings determine:
- the server the RemoteTimeSource is attempting to sync with
- the time provider used to get the remote time from the server
- the interval at which the remote time source should be fetched.
- the window size over which to craft delta over

## RemoteTime Providers
RemoteTime Providers are functions that return the remote time source's current time.

*TLDR: for simplicity use fetch, accuracy or performance prefer a WebSocket based approach.*

On the web there are two types of remote time providers:
- [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) based
- [WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) based

|      | Fetch                                  | WebSocket                        |
|------|----------------------------------------|----------------------------------|
| Pros | - Easy to setup                        | - Performance<br>- More accurate |
| Cons | - Bad performance<br> - Worse accuracy | - Harder to set up               |

There are pros and cons to each approach.

## RemoteTimeProvider Implementations

| Implementation    | Framework | Setup Guide |
|-------------------|-----------|-------------|
| Fetch             | Any       |             |
| Phoenix-WebSocket | Phoenix   |             |

### Don't See an Implementation For Your Application?
[Open an Issue](https://github.com/LukeWood/RemoteTimeSource-TS/issues)


