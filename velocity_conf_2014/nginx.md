# things you didn't know about nginx

Sarah Novotny, nginx

- nginx has lots of acceleration and edge services that used to only exist in hardware
- edge caching, load balancing, reverse proxy, ssl termination

- 146 million websites run nginx

## Advanced features

- thread exhaustion
- form spamming
- a/b testing
- compress assets
- rewrite content
- online upgrades
- configure flags
- include directive
- manipulate proxy headers


### A/B Testing

 split_clients module

 - send traffic, based on a hash and weighting mechanism you choose, to different variants of a page
 - nginx doesn't do any measurement, monitoring, or analysis of the results (obviously)

### Rewrite content inline

 - inline content rewriting
 - to change stuff that lives in every page you have, without having to update those pages

 - sub_filter_once ; on means single replace; off means all
 - sub_filter_types ; defaults to text/html
 - sub_filter ; "search_string" "replace_string"

 - gives an example of a copyright

### Online upgrades

- update either the config files or binary without losing any connections
- you do not need to restart the service

- config file update: nginx -s reload

- her slide shows how to do the binary upgrade. use kill -USR2 [nginx_pid]

- her slides show how you can even roll back... very cool

### Thread Exhaustion

 - use nginx in front of apache
 - mitigates slow_loris, keep dead, and front page of hacker news attacks
 - nginx can handle all of the keep-alive traffic
 - nginx doesn't have a 1:1 correspondence between a client and a thread


### Asset Compression

 - inline image manipulation
 - image_filter size;
 - image_filter resize width height;
 - image_filter crop width height


### Form Spamming

- stop brute force password attacks
- stop form spamming

use the nginx limit request module

- limit_req_zone
- limit_req

- can allow burstability


### Proxy headers

- mask content source, like assets in s3
- manage proxy behavior
- inject your own headers... host header or x-forward-for, etc

- proxy_hide_header
- proxy_set_header
- proxy_ignore_header

- her slide shows how to proxy to s3 and hide all the headers... cool!

- proxy_set_header X-Real-IP $remote_addr -- for returning the real IP for troubleshooting purposes

### Config flags

- nginx -V gives a nearly complete configuration script for compiling


### Include directive

- use the 'include' directive

include /etc/nginx/conf.d/mime.types;
... conf.d/, ...sites-enabled/; etc

