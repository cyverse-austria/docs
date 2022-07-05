# Services

![Discovery env](../assets/discoveryenv.png)

Here you will find all the services which are running on a Kubernetes Cluster.
## List of core-service

1. [analyses](https://github.com/cyverse-de/analyses) : Provides a HTTP API for interacting with analyses in the Discovery Environment.
2. [app-exposer](https://github.com/cyverse-de/app-exposer) : This is a service that runs inside of a Kubernetes cluster namespace and implements CRUD operations for exposing interactive apps as a Service and Endpoint.
3. [apply-labels](https://github.com/cyverse-de/apply-labels) : A small service in the Discovery Environment backend that periodically hits the app-exposer service to trigger the application of labels on VICE-related K8s resources
4. [apps](https://github.com/cyverse-de/apps) : apps is a platform for hosting App Services for the Discovery Environment web application.
5. [async-tasks](https://github.com/cyverse-de/async-tasks) : This service tracks and manages asynchronous tasks throughout the DE backend services.
6. [bulk-typer](https://github.com/cyverse-de/bulk-typer) : Like info-typer, but a bunch at once. hopefully.
7. [check-resources]()
8. [clockwork](https://github.com/cyverse-de/clockwork) : Scheduled jobs for the CyVerse Discovery Environment.
9. [dashboard-aggregator](https://github.com/cyverse-de/dashboard-aggregator) : Gathers data to populate the dashboard in Sonora.
10. [data-info](https://github.com/cyverse-de/data-info) : data-info is a RESTful frontend for getting information about and manipulating information in an iRODS data store.
11. [data-usage-api](https://github.com/cyverse-de/data-usage-api) : A service that provides an API around data usage tracking, and updates data usage numbers on request or periodically.
12. <del>[de-mailer](https://github.com/cyverse-de/de-mailer) :  A go module that send email notifications to users. This module will support HTML and rich text emails.</del>

13. de-nginx
14. [de-stats](https://github.com/cyverse-de/de-stats) : Service for obtaining CyVerse Discovery Environment stats and metrics.
15. [de-webhooks](https://github.com/cyverse-de/de-webhooks) : A service that listens to AMQP queues for DE notifications, check if the user has webhooks defined for that notification type and then post the notification to webhook if one is defined.
16. [dewey](https://github.com/cyverse-de/dewey) : An AMQP message based iRODS indexer for elasticsearch.
17. [email-requests](https://github.com/cyverse-de/email-requests) : A simple service to wait for email requests to arrive over AMQP and forward them to cyverse-email.
18. [event-recorder](https://github.com/cyverse-de/event-recorder) : This service listens to an AMQP topic for events, and records events that may be of interest to users in the notifications database.
19. [get-analysis]() : TODO: FIND the repo.
20. [grouper-loader]() : TODO: FIND the repo.
21. [grouper-ws]() : TODO: FIND the repo.
22. [info-typer](https://github.com/cyverse-de/info-typer) : An AMQP message based info type detector
23. [infosquito2](https://github.com/cyverse-de/infosquito2) : TODO FIND description.
24. [iplant-groups](https://github.com/cyverse-de/iplant-groups) : A RESTful facade in front of [Grouper](https://incommon.org/software/grouper/).
25. [requests](https://github.com/cyverse-de/requests) : Service for managing administrative requests in the CyVerse Discovery Environment.
26. [jex-adapter](https://github.com/cyverse-de/jex-adapter) : TODO FIND description.
27. [job-status-recorder](https://github.com/cyverse-de/job-status-recorder) : TODO FIND description.
28. [job-status-listener](https://github.com/cyverse-de/job-status-listener) : Listens over HTTP for job status updates, then publishes them to AMQP.
29. [kifshare](https://github.com/cyverse-de/kifshare) : A simple web page that allows users to download publicly available files without a CyVerse account.
30. [local-exim](): TODO: FIND the repo.
31. [metadata](https://github.com/cyverse-de/metadata) : The REST API for the Discovery Environment Metadata services.
32. [monkey](https://github.com/cyverse-de/monkey) : This is a service that synchronizes the tag documents in the data search index with the metadata database
33. [notifications](https://github.com/cyverse-de/notifications) : This service provides the RESTful API for the revised notification system.
34. [permissions](https://github.com/cyverse-de/permissions) : This service manages permissions for the Discovery environment.
35. [requests](https://github.com/cyverse-de/requests) : Service for managing administrative requests in the CyVerse Discovery Environment.
36. [terrain](https://github.com/cyverse-de/terrain) : Terrain provides the primary REST API used by the Discovery Environment. Its role is to validate user authentication and to coordinate calls to other web services. For more information, please see the [Discovery Environment API Documentation](https://cyverse-de.github.io/api/).
37. [resource-usage-api](https://github.com/cyverse-de/resource-usage-api) :  is a microservice developed as part of the CyVerse Discovery Environment that provides access to resource usage values (CPU hours, memory, etc.) consumed by users over a customizable time period.
38. [saved-searches](https://github.com/cyverse-de/saved-searches) : A service for the CyVerse Discovery Environment that provides CRUD access to a user's saved searches.
39. [search](https://github.com/cyverse-de/search) : This is a service which serves as a search facade for the DE and others to use. It uses the querydsl library under the covers to translate requests and provide documentation, then passes off queries to configured elasticsearch servers.
40. [sonora](https://github.com/cyverse-de/sonora) : UI for the Discovery Environment
41. [templeton-incremental]() : TODO: FIND the repo.
42. [templeton-periodic]() : TODO: FIND the repo.
43. [timelord](https://github.com/cyverse-de/timelord) : timelord periodically queries the DE database for running applications and kills any of them that have gone over their time limit.
44. [unleash]() : TODO: FIND the repo.
45. [user-info](https://github.com/cyverse-de/user-info) : A service for getting user-related information like sessions and preferences.
46. [vice-default-backend](https://github.com/cyverse-de/vice-default-backend) : Provides a default backend handler for the Kubernetes Ingress that handles routing for VICE apps. This backend decides whether to redirect requests to the loading page service, the landing page service, or to a 404 page depending on whether the URL is valid or not.
47. [qms-adapter](https://github.com/cyverse-de/qms-adapter) : Forwards usage information gathered within the Discovery Environment to the Quota Management System [QMS](https://github.com/cyverse/QMS).
48. [qms](https://github.com/cyverse/QMS) : QMS is the CyVerse Quota Management System. Its purpose is to keep track of resource usage limits and totals for CyVerse users.


## List of non-core services

1. redis-ha
2. redis-haproxy
3. elasticsearch
4. irods-csi-driver
5. keycloak
6. openebs
