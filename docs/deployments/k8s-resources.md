# k8s-resources

This repository includes all the manifests and resources for kubernetes deployment.

## Clone

```bash
git clone git@gitlab.cyverse.org:tugraz/k8s-resources.git
```

## Generate config/secrets for pro env
```bash
./generate_configs.py -e prod
./generate_secrets.py -e prod
```

## Load config/secrets in your cluster for pro env
```bash
./load_configs.py -e prod -n prod
./load_secrets.py -e prod -n prod
```


## create a new env
Currently we have `prod` environment which is our productive instance.

To create new environment take these steps.

```bash
# we will create a new environment call it discover
cd config_values
vi discover.yaml
```

**fill in all these values:**
```yaml
# discover.yaml
---
Environment:

Agave:
  Key:
  Secret:
  RedirectURI:
  StorageSystem:
  CallbackBaseURI:
  ReadTimeout:
  Enabled:
  JobsEnabled:

AMQP:
  URI:

AnonFiles:
  BaseURI:

AppExposer:
  BaseURI:

BaseURLs:
  Analyses:
  Apps:
  AsyncTasks:
  DashboardAggregator:
  DataInfo:
  GrouperWebServices:
  IplantEmail:
  IplantGroups:
  JexAdapter:
  Metadata:
  Notifications:
  Permissions:
  Requests:
  Search:
  Terrain:
  UserInfo:

CAS:
  BaseURI:
  ServerName:
  UIDDomain:

DashboardAggregator:
  PublicGroup:
  LogLevel:

DataOne:
  BaseURI:

DE:
  Version:
  VersionName:
  AMQP:
    URI:
  Host:
  BaseURI:
  Legacy:
    BaseURI:
  Subscriptions:
    CheckoutURL:
  KeepAlive:
    Service:
    Target:
  ContextMenu:
    Enabled:
  BaseTrash:
    Path:
  ProdDeployment:
  DefaultOutputFolder:
  WSO2:
    JWTHeader:
  Coge:
    BaseURI:
  Tools:
    Admin:
      MaxCpuLimit:
      MaxMemoryLimit:
      MaxDiskLimit:

Docker:
  TrustedRegistries:
  Tag:

Elasticsearch:
  BaseURI:
  Username:
  Password:
  Index:

Email:
  AppDeletion:
    Src:
    Dest:
  AppPublicationRequest:
    Src:
    Dest:
  ToolRequest:
    Src:
    Dest:
  PermIDRequest:
    Src:
    Dest:
  Support:
    Src:
    Dest:

Grouper:
  Environment:
  MorphString:
  WebService:
    Password:
  Password:
  DB:
    User:
    Password:
    Host:
    Port:
    Name:
  FolderNamePrefix:
  Loader:
    URI:
    User:
    Password:
  SubjectSource:
    ID:
    Name:
    SearchBase:

ICAT:
  Host:
  Port:
  User:
  Password:

Infosquito:
  DayNum:
  PrefixLength:

InteractiveApps:
  BaseURI:
  ServiceSuffix:

Intercom:
  AppID:
  CompanyID:
  CompanyName:
  Intercom:

IRODS:
  AMQP:
    URI:
  Host:
  User:
  Zone:
  Password:
  AdminUsers:
  PermsFilter:
  ExternalHost:
  QuotaRootResources:

Jobs:
  DataTransferImage:

JobStatusListener:
  BaseURI:

Keycloak:
  ServerURI:
  Realm:
  ClientID:
  ClientSecret:
  VICE:
    ClientID:
    ClientSecret:

Kifshare:
  ExternalUri:

PGP:
  KeyPassword:

PermanentID:
  CuratorsGroup:
  DataCite:
    BaseURI:
    User:
    Password:
    DOIPrefix:

Redis:
  Host:
  Port:
  HA:
    Name:
  Password:
  DB:
    Number:

TimeZone:

Vault:
  Token:
  URL:
  IRODS:
    MountPath:
    ChildToken:
      UseLimit:

VICE:
  DB:
    User:
    Password:
    Host:
    Port:
    Name:
  FileTransfers:
    Image:
    Tag:
  JobStatus:
    BaseURI:
  K8sEnabled:
  BackendNamespace:
  ImagePullSecret:
  ImageCache:
  UseCSIDriver:
  DefaultImage:
  DefaultName:
  DefaultCasUrl:
  DefaultCasValidate:
  ConcurrentJobs:
  UseCaseCharsMin:
  DefaultBackend:
    LoadingPageTemplateString:

Sonora:
  BaseURI:

Terrain:
  CASClientID:
  CASClientSecret:
  JWT:
    SigningKey:
      Password:

Unleash:
  BaseUrl:
  APIPath:
  APIToken:
  MaintenanceFlag:

UserPortal:
  BaseURI:

DEDB:
  User:
  Password:
  Host:
  Port:
  Name:

NewNotificationsDB:
  User:
  Password:
  Host:
  Port:
  Name:

NotificationsDB:
  User:
  Password:
  Host:
  Port:
  Name:

PermissionsDB:
  User:
  Password:
  Host:
  Port:
  Name:

QMSDB:
  User:
  Password:
  Host:
  Port:
  Name:
  Reinitialize:

MetadataDB:
  User:
  Password:
  Host:
  Port:
  Name:

UnleashDB:
  User:
  Password:
  Host:
  Port:
  Name:

Admin:
  Groups:
  Attribute:

FileIdentifier:
  HtPathList:
  MultiInputPathList:

Analytics:
  Enabled:
  Id:

Harbor:
  URL:
  ProjectQARobotName:
  ProjectQARobotSecret:

QMS:
  Enabled:
  Base:
  Usage:

Jaeger:
  Endpoint:
```

## Generate config/secrets for discover env
```bash
./generate_configs.py -e discover
./generate_secrets.py -e discover
```

## Load config/secrets in your cluster for discover env
```bash
./load_configs.py -e discover -n discover
./load_secrets.py -e discover -n discover
```
