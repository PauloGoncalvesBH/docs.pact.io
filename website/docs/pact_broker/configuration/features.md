---
title: Features
---

See the [settings](/pact_broker/configuration/settings) page for a comprehensive list of all configuration options.

__NOTE: This page describes how to configure the *native Ruby Pact Broker* application. The Pact Broker Ruby application is distributed in 2 different Docker images, one based on [Puma](/pact_broker/docker_images/pactfoundation) (this is our default recommendation) and one based on [Passenger](/pact_broker/docker_images/dius) (older, but still supported). Each of the Docker images is configurable using environment variables that map to the Ruby Pact Broker application configuration options. Please see the documentation for your Docker image for the names and formats of the environment variables.__

## Getting started

The only required configuration settings to get started are the database credentials. You can set the connection string to the database using the environment variable [`PACT_BROKER_DATABASE_URL`](/pact_broker/configuration/settings#database_url) in the format `{database_adapter}://{database_username}:{database_password}@{database_host}:{database_port}/{database_name}`. See the [database section](/pact_broker/configuration/settings#database) of the settings page for futher details.

Once you are up and running, we recommend you set the [`base_url`](/pact_broker/configuration/settings#base_url) and the `webhook_host_whitelist` as per the documentation [below](#webhook-whitelists)

## Webhooks

### Webhook whitelists

To ensure that webhooks cannot be used maliciously to expose either data about your contracts or your internal network, the following validation rules are applied to webhooks via the Pact Broker configuration settings.

- **Scheme**: Must be included in the [`webhook_scheme_whitelist`](/pact_broker/configuration/settings#webhook_scheme_whitelist), which by default only includes `https`. You can change this to include `http` if absolutely necessary, however, keep in mind that the body of any http traffic is visible to the network.
- **HTTP method**: Must be included in the [`webhook_http_method_whitelist`](/pact_broker/configuration/settings#webhook_http_method_whitelist), which by default only includes `POST`. It is highly recommended that only `POST` requests are allowed to ensure that webhooks cannot be used to retrieve sensitive information from hosts within the same network.
- **Host**: If the [`webhook_host_whitelist`](/pact_broker/configuration/settings#webhook_host_whitelist) contains any entries, the host must match one or more of the entries. By default, it is empty. If the host whitelist is empty, any host is allowed, but for security purposes the response details will not be logged to the UI \(though they can be seen in the application logs at debug level\).

  The host whitelist may contain hostnames \(eg `"github.com"`\), IPs \(eg `"192.0.345.4"`\), network ranges \(eg `"10.0.0.0/8"`\) or regular expressions \(eg `/.*\.foo\.com$/`\). Note that IPs are not resolved, so if you specify an IP range, you need to use the IP in the webhook URL. If you wish to allow webhooks to any host \(not recommended!\), you can set `webhook_host_whitelist` to `[/.*/]`. Beware of any sensitive endpoints that may be exposed within the same network.

  The recommended set of values to start with are:

  - your CI server's hostname \(for triggering builds\)
  - your company chat \(eg. Slack, for publishing notifications\)
  - your code repository \(eg. Github, for sending commit statuses\)

  Alternatively, you could use a regular expression to limit requests to your company's domain. eg `/.*\.foo\.com$/` \(don't forget the end of string anchor\). You can test Ruby regular expressions at [rubular.com](http://rubular.com).

### Webhook SSL certificates

If your broker needs to execute a webhook against a server that has a self signed certificate, you will need to add the certificate to the broker's certificate store.

From Pact Broker version 2.90.0, you can use the [webhook_certificates](/pact_broker/configuration/settings#webhook_certificates) setting in the `pact_broker.yml` config file to configure the certificates.

In previous versions of the Pact Broker, the only way to load the certificates is to use the script [script/prod/insert-self-signed-certificate-from-url.rb](https://github.com/pact-foundation/pact_broker/blob/master/script/prod/insert-self-signed-certificate-from-url.rb). The easiest way to run this is to copy it to the machine where the broker is deployed, and modify the database credentials to match those of your broker.

### Webhook HTTP proxies

If your webhooks need to execute via a HTTP proxy, set the `http_proxy` environment variable to the address of your proxy.

## Healthcheck/Heartbeat URL

The heartbeat is available at `/diagnostic/status/heartbeat`. No database connection will be made during the execution of this endpoint.

If you have enabled basic auth, and you are running the Pact Broker within an AWS autoscaling group or similar and you need to make a heartbeat URL publicly available, set [`public_heartbeat`](/pact_broker/configuration/settings#public_heartbeat) to `true`. 

## Badges

Behind the scenes, the Pact Broker uses [img.shields.io](https://img.shields.io) to dynamically create the text on the badges. Older versions of the Pact Broker proxy the badge file from the shields.io server, but newer versions use a redirect response so that the image is fetched directly from the browser. If the shields.io server cannot be made available within your organisation, set `config.shields_io_base_url` to nil, and you will get badges with the hardcoded title "pact" instead of "foo/bar pact".

If you cannot allow access to the public shields server because of Network Security, then you could run your own local [docker](https://github.com/beevelop/docker-shields) one.

NOTE: If you have added your own authentication on top of the broker, you'll need to add a rule to allow public access to the badge URLs.

## Ordering versions

By default, pacticipant versions \(and hence their related pacts\) are sorted by date published. In earlier versions of the Pact Broker, the versions were sorted semantically. Semantic ordering is now deprecated, as the best practice is to publish pacts using the git sha as the consumer version.

You are on a very old version of the Broker, and wish to use date ordering, you will need to set `config.order_versions_by_date = true`. After you have restarted, you will need to publish a new pact to trigger a resort, as the ordering is done on insertion.

## Checking for potential duplicate pacticipant names

When a pact is published normally \(via a PUT to `/pacts/provider/PROVIDER/consumer/CONSUMER/version/CONSUMER_APP_VERSION`\) the `consumer`, `provider` and `consumer version` resources are automatically created.

To prevent a pacticipant \(consumer or provider\) being created multiple times with slightly different name variants \(eg. FooBar/foo-bar/foo bar/Foo Bar Service\), if a new pacticipant name is deemed similar enough to an existing name, a 409 will be returned. The response body will contain instructions indicating that the pacticipant name should be corrected if it was intended to be an existing one, or that the pacticipant should be created manually if it was intended to be a new one.

To manually create the pacticipant with the similar name, use the [create-or-update-pacticipant](/pact_broker/client_cli/readme#create-or-update-pacticipant) command from the Pact Broker Client CLI.

eg.

```
pact-broker create-or-update-pacticipant --name <NAME>
```

To turn this feature off, set `check_for_potential_duplicate_pacticipant_names = false` (or set the appropriate environment variable if using a Docker image) in the Pact Broker configuration, and make sure everyone is very careful with their naming! The usefulness of the broker depends on the integrity of the data, which in turn depends on the correctness of the pacticipant names.

## Running the broker behind a reverse proxy

If the pact broker is setup behind a reverse proxy then there are a few headers that must be set for the hypermedia links in the JSON resources to be generated with the correct base URLs. The required headers to be sent depend on the proxy configuration. For example if the reverse proxy is configured to forward from [https://broker.example.com](https://broker.example.com) -&gt; [http://internal.broker](http://internal.broker) then X-Forwarded-Host, X-Forwarded-Port and X-Forwarded-Ssl or X-Forwarded-Scheme would need to set in the nginx configuration.

* **X-Forwarded-Scheme**

  Set this to either "http" or "https" depending on the scheme used by the reverse proxy. For example if the URL configured at the proxy is [https://broker.example.com](https://broker.example.com) then this should be "https".

* **X-Forwarded-Host**

  Set this to the host name used by the reverse proxy. For example if the URL configured at the proxy is [https://broker.example.com](https://broker.example.com) then this should be "broker.example.com".

* **X-Forwarded-Port**

  Set this to the port used by the reverse proxy. For example if the URL configured at the proxy is [https://broker.example.com](https://broker.example.com) then this should be "443".

* **X-Forwarded-Ssl**

  Set this to "on" if the scheme of the reverse proxy is https. For example if the URL configured at the proxy is [https://broker.example.com](https://broker.example.com) then this should be "on".

See [this example](https://github.com/DiUS/pact_broker-docker/issues/58#issuecomment-358819665) for how to achieve this with Nginx.

### When the base URL configuration is supported (v2.46.0 and later)

Please set the base URL of the Pact Broker application (eg. `https://pact-broker.mycompany.com`) via the supported configuration mechanism for the deployment artifact (the environment variable `PACT_BROKER_BASE_URL` for the Docker images, or `PactBroker.configuration.base_url = "..."` for native Ruby). Setting the base URL is recommended as it prevents some security vulnerabilities associated with dynamically inferring the base URL from the request headers.

From version `2.79.0`, multiple base URLs can be configured for architectures that use gateways or proxies that allow the same Pact Broker instance to be addressed with different base URLs. To use this feature, list all the base URLs in the base URL string, separated by a space. eg. `"http://my-internal-pact-broker:9292 https://my-external-pact-broker"`

### When the base URL configuration is not supported (versions prior to 2.46.0)

*It is preferrable to upgrade to the latest version of the Pact Broker, as 2.46 is old and may contain vulerabilities. Also, determining the base URL dynamically using the X-Forwarded headers leaves the application open to [DNS cache poisoning](https://www.cloudflare.com/learning/dns/dns-cache-poisoning/).*

