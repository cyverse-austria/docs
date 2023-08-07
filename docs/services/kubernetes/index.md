# Services

![Discovery env](../assets/discoveryenv.png)

Here you will find all the services which are running on a Kubernetes Cluster.
## List of core-service

* [analyses](https://github.com/cyverse-de/analyses) : Provides a HTTP API for interacting with analyses in the Discovery Environment.
* [app-exposer](https://github.com/cyverse-de/app-exposer) : This is a service that runs inside of a Kubernetes cluster namespace and implements CRUD operations for exposing interactive apps as a Service and Endpoint.
* [apply-labels](https://github.com/cyverse-de/apply-labels) : A small service in the Discovery Environment backend that periodically hits the app-exposer service to trigger the application of labels on VICE-related K8s resources
* [apps](https://github.com/cyverse-de/apps) : apps is a platform for hosting App Services for the Discovery Environment web application.
* [async-tasks](https://github.com/cyverse-de/async-tasks) : This service tracks and manages asynchronous tasks throughout the DE backend services.
* [bulk-typer](https://github.com/cyverse-de/bulk-typer) : Like info-typer, but a bunch at once. hopefully.
* [check-resource-access](https://github.com/cyverse-de/check-resource-access) : Looks up the permissions that a subject has for a resource. By default, the subject type is 'user' and the resource type is 'analysis'. Only performs look ups against the permissions service.
* [clockwork](https://github.com/cyverse-de/clockwork) : Scheduled jobs for the CyVerse Discovery Environment.
* [dashboard-aggregator](https://github.com/cyverse-de/dashboard-aggregator) : Gathers data to populate the dashboard in Sonora.
* [data-info](https://github.com/cyverse-de/data-info) : data-info is a RESTful frontend for getting information about and manipulating information in an iRODS data store.
* [data-usage-api](https://github.com/cyverse-de/data-usage-api) : A service that provides an API around data usage tracking, and updates data usage numbers on request or periodically.
* <del>[de-mailer](https://github.com/cyverse-de/de-mailer) :  A go module that send email notifications to users. This module will support HTML and rich text emails.</del>
* <del>[de-stats](https://github.com/cyverse-de/de-stats) : Service for obtaining CyVerse Discovery Environment stats and metrics.</del>
* [de-webhooks](https://github.com/cyverse-de/de-webhooks) : A service that listens to AMQP queues for DE notifications, check if the user has webhooks defined for that notification type and then post the notification to webhook if one is defined.
* [dewey](https://github.com/cyverse-de/dewey) : An AMQP message based iRODS indexer for elasticsearch.
* [discoenv-analyses](https://github.com/cyverse-de/discoenv-analyses) : A small service that makes analysis-related information available over NATS.
* [discoenv-users](https://github.com/cyverse-de/discoenv-users) : Is a microservice for the CyVerse Discovery Environment which allows users to look up information about a user. It uses NATS for communication.
* [email-requests](https://github.com/cyverse-de/email-requests) : A simple service to wait for email requests to arrive over AMQP and forward them to cyverse-email.
* [event-recorder](https://github.com/cyverse-de/event-recorder) : This service listens to an AMQP topic for events, and records events that may be of interest to users in the notifications database.
* [get-analysis-id](https://github.com/cyverse-de/get-analysis-id) : Microservice that uses the DE's apps service to return the analysis UUID associated with the provided external UUID.
* [grouper]() : - `grouper-loader` & `grouper-ws` TODO: FIND the repo.   - From kubectl apply
* [group-propagator]() :
* [info-typer](https://github.com/cyverse-de/info-typer) : An AMQP message based info type detector
* [infosquito2](https://github.com/cyverse-de/infosquito2) : TODO FIND description.
* [iplant-groups](https://github.com/cyverse-de/iplant-groups) : A RESTful facade in front of [Grouper](https://incommon.org/software/grouper/).
* [jex-adapter](https://github.com/cyverse-de/jex-adapter) : TODO FIND description.
* [job-status-recorder](https://github.com/cyverse-de/job-status-recorder) : TODO FIND description.
* [job-status-listener](https://github.com/cyverse-de/job-status-listener) : Listens over HTTP for job status updates, then publishes them to AMQP.
* [job-status-to-apps-adapter](https://github.com/cyverse-de/job-status-to-apps-adapter) :
* [kifshare](https://github.com/cyverse-de/kifshare) : A simple web page that allows users to download publicly available files without a CyVerse account.
* [local-exim (exim-sender)](): TODO: FIND the repo. - From kubectl
* [metadata](https://github.com/cyverse-de/metadata) : The REST API for the Discovery Environment Metadata services.
* [monkey](https://github.com/cyverse-de/monkey) : This is a service that synchronizes the tag documents in the data search index with the metadata database
* [monitoring-agent](https://github.com/cyverse-de/monitoring-agent) : A service for the Discovery Environment that checks on the state of various internal and external resources and reports that state back to a central data aggregation service for later export to Prometheus.
* [notifications](https://github.com/cyverse-de/notifications) : This service provides the RESTful API for the revised notification system.
* [permissions](https://github.com/cyverse-de/permissions) : This service manages permissions for the Discovery environment.
* [requests](https://github.com/cyverse-de/requests) : Service for managing administrative requests in the CyVerse Discovery Environment.
* [terrain](https://github.com/cyverse-de/terrain) : Terrain provides the primary REST API used by the Discovery Environment. Its role is to validate user authentication and to coordinate calls to other web services. For more information, please see the [Discovery Environment API Documentation](https://cyverse-de.github.io/api/).
* [resource-usage-api](https://github.com/cyverse-de/resource-usage-api) :  is a microservice developed as part of the CyVerse Discovery Environment that provides access to resource usage values (CPU hours, memory, etc.) consumed by users over a customizable time period.
* <del>[saved-searches](https://github.com/cyverse-de/saved-searches) : A service for the CyVerse Discovery Environment that provides CRUD access to a user's saved searches.</del>
* [search](https://github.com/cyverse-de/search) : This is a service which serves as a search facade for the DE and others to use. It uses the querydsl library under the covers to translate requests and provide documentation, then passes off queries to configured elasticsearch servers.
* [sonora](https://github.com/cyverse-de/sonora) : UI for the Discovery Environment
* [templeton](https://github.com/cyverse-de/templeton) : includes `templeton-incremental` & `templeton-periodic` TODO: add description.
* [timelord](https://github.com/cyverse-de/timelord) : timelord periodically queries the DE database for running applications and kills any of them that have gone over their time limit.
* [unleash]() : TODO: FIND the repo. - From kubectl apply
* [user-info](https://github.com/cyverse-de/user-info) : A service for getting user-related information like sessions and preferences.
* [vice-default-backend](https://github.com/cyverse-de/vice-default-backend) : Provides a default backend handler for the Kubernetes Ingress that handles routing for VICE apps. This backend decides whether to redirect requests to the loading page service, the landing page service, or to a 404 page depending on whether the URL is valid or not.
* [qms-adapter](https://github.com/cyverse-de/qms-adapter) : Forwards usage information gathered within the Discovery Environment to the Quota Management System [QMS](https://github.com/cyverse/QMS).
* [qms](https://github.com/cyverse/QMS) : QMS is the CyVerse Quota Management System. Its purpose is to keep track of resource usage limits and totals for CyVerse users.
* [irods-csi-driver](https://github.com/cyverse/irods-csi-driver) : iRODS Container Storage Interface (CSI) Driver implements the [CSI Specification](https://github.com/container-storage-interface/spec/blob/master/spec.md) to provide container orchestration engines (like Kubernetes) iRODS access.
* <del>[dataone-indexer](https://github.com/cyverse-de/dataone-indexer) : Event indexer for the DataONE member node service.</del>

## List of non-core services

1. redis-ha
2. redis-haproxy
3. elasticsearch
5. keycloak
6. openebs
