# Change log for adding getex/lrangeex and modifying setex #

@ author leo
@ date 2014-3-24

## changes ##
1. Add command 'getex key ttl'
  It works as 'get key && expire key ttl' exept that the 'expire' command don't has any result reply;
    * if ttl > 0, set this key's time-to-live to ttl seconds;
    * if ttl == 0, keep this key's time-to-live as it was;
    * else (if ttl < 0), delete this key after get;

2. Add command 'lrangeex key start stop ttl'
  It works as 'lrange key start stop && expire key ttl', just like 'getex';

3. Modify command 'setex key ttl value'

  * The original version of this command means:
      * if ttl > 0, set this key's time-to-live to ttl seconds;
      * else (if ttl <= 0) returns error message 'ERR invalid expire time in SETEX';

  * The modified version means:
      * if ttl > 0, set this key's time-to-live to ttl seconds (same as before);
      * if ttl == 0, keep this key's time-to-live as it was;
      * if ttl == -1, remove this key's ttl, mark key as has no expire;
      * else returns error message '(error) ERR invalid expire time in SETEX, should be one of -1, 0, or positive interger.'.

