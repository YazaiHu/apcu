
APCu
====

APCu is userland caching: APC stripped of it's opcode caching in preparation for the deployment of Zend Optimizer+ as the primary solution to opcode caching in future versions of PHP.

APCu has a revised and simplified codebase, by the time the PECL release is available, every part of APCu being used will have recieved review and where necessary or appropriate, changes.

Simplifying and documenting the API of APCu completely removes the barrier to maintenance and development of APCu in the future, and additionally allows us to make optimizations not possible previously because of APC's inherent complexity.

APCu only supports userland caching (and dumping) of variables, providing an upgrade path for the future. When O+ takes over, many will be tempted to use 3rd party solutions to userland caching, possibly even distributed solutions; this would be a grave error. The tried and tested APC codebase provides far superior support for local storage of PHP variables.

Specific Changes
================

    * appropriate changes (removals) to configuration parameters (complete)
    * appropriate changes to userspace management script (complete)
	* revision of APC locking (ongoing, unix-like OS tested & working, more testing to be done)
    * revision of APC's caching API (complete)
    * revision of APC's PHP internals (complete)
    * revision of APC's userspace API (complete, exception apc_bin.c)
    * revision of APC's shared memory allocator (complete)
    * revision of APC's pooling API (complete, no functional changes, documented)
    * installation of SIGUSR1 handler (where possible) to clear cache (complete)
    * slot level locking (complete)
    * format API headers so they can be referenced externally (complete, see apcue)
    * apc.smart allows runtime adjustable control over how the cache is purged (complete)
    * documentation of all associated API's (ongoing, mostly complete, all headers and source file documented and commented)

Still to Do:
============

	* serializer needs to be moved out of globals to aid third parties, apc_context_t/apc_cache_t
    * cleanup config.m4/config.w32
    * 

The C api does not retain backward compatibility, anyone relying on APC that will rely on APCu in the future should review the changes as soon as possible and continue to track them.
The PHP api will retain compatibility with APC, as will common configuration options, providing a drop in replacement.

Possible Ideas
==============

In no particular order:

	* an asyncronous apc_store/apc_add solution (already tested, removed in the interest of simplicity)
	* TCP failover for APCu, utilizing the binary API and TCP sockets (untested, would love it)
    * local connection to an instance of APCu in another process ( or SAPI ) from at least CLI

If you have any thoughts, please provde them to me, by any means.
