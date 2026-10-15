# VPC network segmentation

## Problem

The exercise separates a public web tier from a database tier and requires working web-to-database connectivity. The strongest outcome evidence is the networking DIY validator's completion message.

## Routing change

RouteTable2 displays a saved-routes success banner. The exact route destinations are not visible in this crop, so it does not independently prove the full Internet Gateway configuration.

![Route-table update succeeded](../images/05-route-tables-updated.png)

## Web-tier rules

The inbound-change banner confirms a saved security-group update; the rules themselves are below the crop.

![Web inbound rule update succeeded](../images/07-webserver-sg-inbound.png)

The egress table shows HTTP 80, HTTPS 443 and MySQL 3306 entries. Their destinations require the fuller editor view below.

![Web-tier outbound ports](../images/08-webserver-sg-outbound.png)

The editor shows HTTP/HTTPS destinations, a database security-group destination for MySQL, and an additional all-traffic row. This is an editing state: it is not evidence that every displayed row was saved or that egress is narrowly restricted. Review and remove unnecessary broad egress in a production design.

![Outbound rule editor and destination scope](../images/09-edit-outbound-rules.png)

## Database change and validator outcome

The database group shows an inbound-rule update success banner. Its exact saved source/port is below the crop. The accompanying validator reports networking assignment completion; this is broader workflow evidence, not a packet capture or per-rule audit.

![Database inbound update succeeded](../images/12-dbserver-sg-inbound.png)

![Networking DIY validation passed](../images/13-you-did-it.png)

## Lessons

Check direction, source/destination and port together; a port alone is not segmentation. Security groups are stateful, so tracked response traffic is allowed without a separate reverse-direction rule. Record saved configuration and positive/negative reachability tests before claiming production isolation.
