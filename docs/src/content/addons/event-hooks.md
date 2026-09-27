---
title: "Event Hooks"
weight: 2
# this is important so that the relative links in the generated file work.
url: api/events.html
aliases:
    - /addons-events/
---

# Event Hooks

Addons hook into mitmproxy's internal mechanisms through event hooks. These are
implemented on addons as methods with a set of well-known names. Many events
receive `Flow` objects as arguments - by modifying these objects, addons can
change traffic on the fly. For instance, here is an addon that adds a response
header with a count of the number of responses seen:

{{< example src="examples/addons/http-add-header.py" lang="py" >}}

## Addon lifecycle

During a normal startup, mitmproxy calls the lifecycle hooks in this order:

1. `load(loader)` runs when an addon is registered. Use it to register options
   and commands.
2. `configure(updated)` runs with the initial option values. It runs again
   whenever options change, including after startup.
3. `running()` runs after mitmproxy has set up its proxy servers and is ready
   to handle traffic.
4. `done()` runs during shutdown, if `running()` was called.

In short: `load` → `configure` → `running` → `done`, with additional
`configure` calls when settings change. See [Custom Options]({{< relref
"/addons/options" >}}) for an example of handling `configure`.

## Available Hooks

The following addons list all available event hooks.

{{< readfile file="/generated/api/events.html" >}}
