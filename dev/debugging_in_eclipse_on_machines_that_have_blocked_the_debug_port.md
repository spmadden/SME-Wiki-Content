## Debugging in Eclipse on machines that have blocked the Debug Port

Create a new Run configuration called 'Project-debug'

In the JVM Options, add the following line

      -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=y,address={addr}

Where {addr} is a port that you have listen access on.

The SSE has opened port 1527 for listening.

Create a new Remote Debug configuration called 'Project-Debug'

    Select 'Standard (Socket Attach)'
    Select host localhost
    Select port {addr} from above

Start the Run configuration first, you should see the following line:

    Listening for transport dt_socket at address: {addr}

Start the Debug configuration next, then debug as usual.
