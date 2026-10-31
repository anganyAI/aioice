Changelog
=========

.. currentmodule:: aioice

0.10.2+angany.2
---------------

 * Send the nominating check to an ICE-lite peer, without waiting for its
   answer: a peer that waits for USE-CANDIDATE completes, and one that refuses
   or ignores it still leaves the pair nominated.

0.10.2+angany.1
---------------

The anganyAI fork, on top of 0.10.2: what an ICE session needs to hold a call
with a relay that redirects and restarts.

 * Add :meth:`Connection.restart` to restart ICE with new remote credentials and
   candidates, keeping the local transports and TURN allocations.
 * Add :meth:`Connection.update_remote_credentials` to change the remote
   ufrag/pwd without a restart.
 * Add :meth:`Connection.set_ice_controlling` to override the ICE role.
 * Add a `nomination_strategy` parameter to :class:`Connection`, `"aggressive"`
   (the default) or `"regular"`.
 * Follow a TURN server's 300 Try Alternate answer, up to five redirects.
 * Gather no host or server-reflexive candidates under
   :attr:`TransportPolicy.RELAY`.
 * Nominate an ICE-lite peer's pair without a USE-CANDIDATE round trip.
 * Log each received packet at DEBUG instead of INFO.

0.10.2
------

 * Fix local ice-ufrag/ice-pwd validation.

0.10.1
------

 * Remove a `print()` statement which was accidentally added in 0.10.0.

0.10.0
------

 * Enforce full type annotations on all the code.
 * Allow creating a connection with ufrag and pwd.
 * Fix an `IndexError` when decoding an invalid XOR-MAPPED-ADDRESS.
 * Connect to TURN server in parallel to STUN checks and catch errors.

0.9.0
-----

 * Switch from `netifaces` to `ifaddr`.
 * Do not start candidate pair check if already started.

0.8.0
-----

 * Allow gathering only relay (STUN/TURN) candidates.
 * Use padding when sending over data over TCP.
 * Add support for Python 3.11.

0.7.7
-----

 * Close underlying transport when a TURN allocation is deleted.
 * Shutdown mDNS stack when it is no longer referenced.
 * Rewrite asynchronous tests as coroutines.

0.7.6
-----

 * Ensure `dnspython` version is at least 2.0.0.
 * Avoid 400 error when using TURN with concurrent sends.
 * Avoid error if a connection is lost before the local candidate is set.

0.7.5
-----

 * Emit an event when the ICE connection is closed.

0.7.4
-----

 * Perform mDNS resolution using an A query, as Firefox does not respond
   to ANY queries.
 * Use full module name to name loggers.

0.7.3
-----

 * Defer mDNS lock initialisation to avoid mismatched event-loops,
   fixes errors seen with uvloop.
 * Correctly gather STUN candidates when there are multiple components.

0.7.2
-----

 * Add support for resolving mDNS candidates.

0.7.1
-----

TURN
....

 * Use the LIFETIME attribute returned by the server to determine the
   time-to-expiry for the allocation.
 * Raise stun.TransactionFailed if TURN allocation request is rejected
   with an error.
 * Handle 438 (Stale Nonce) error responses.
 * Ignore STUN transaction errors when deleting TURN allocation.
 * Periodically refresh channel bindings.

0.7.0
-----

Breaking
........

 * Make :meth:`Connection.add_remote_candidate` a coroutine.
 * Remove the `Connection.remote_candidates` setter.
