


Using In-line C to extend Varnish
---------------------------------

(Here there be dragons. Big and mean ones.)

You can use *in-line C* to extend Varnish. Please note that you can
seriously mess up Varnish this way. The C code runs within the Varnish
Cache process so if your code generates a segfault the cache will crash.

One of the first uses I saw of In-line C was logging to syslog.::

        # The include statements must be outside the subroutines.
        C{
                #include <syslog.h>
        }C
        
        sub vcl_something {
                C{
                        syslog(LOG_INFO, "Something happened at VCL line XX.");
                }C
        }
