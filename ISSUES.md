1. Issue with dirtyflag - i couldnt figure out what to do with it except restore from snapshot
```
Failed to initialize
info  2024-01-17T08:42:07.773 chronicle decoder_plugin.cpp:649        plugin_initialize    ] Initialized decoder_plugin
info  2024-01-17T08:42:07.774 chronicle exp_ws_plugin.cpp:469         plugin_initialize    ] Initialized exp_ws_plugin
info  2024-01-17T08:42:07.774 chronicle receiver_plugin.cpp:1624      plugin_initialize    ] Starting in scan mode
info  2024-01-17T08:42:07.774 chronicle receiver_plugin.cpp:1639      plugin_initialize    ] Using shared memory lock at /var/local/chronicle/chronicle-data/receiver-state/lock.bin
warn  2024-01-17T08:42:07.774 chronicle receiver_plugin.cpp:1840      plugin_initialize    ] 13 N5boost10wrapexceptINSt3__112system_errorEEE: Database dirty flag set
rethrow Database dirty flag set: 
    {"what":"Database dirty flag set"}
    chronicle-recei  receiver_plugin.cpp:1840 plugin_initialize

Failed to initialize
```