# Keycloak Notes

[Wildfly Subsystem Configration](https://docs.jboss.org/author/display/WFLY8/Subsystem%20configuration.html).

## Extending Server

* Cli / Embed / SPI. [redhat.com](https://access.redhat.com/documentation/en-us/red_hat_single_sign-on/7.2/html/server_installation_and_configuration_guide/manage_subsystem_configuration).
* Plugin vs Module. [JBoss pipermail](https://lists.jboss.org/pipermail/keycloak-user/2017-November/012410.html).
* Examples [@zonaut/keycloak-extensions](https://github.com/zonaut/keycloak-extensions/).
* Even more examples [@thomasdarimont/keycloak-extension-playground](https://github.com/thomasdarimont/keycloak-extension-playground).
* OIDC Token Mapper [Keycloak sources](https://github.com/keycloak/keycloak/blob/master/services/src/main/java/org/keycloak/protocol/oidc/mappers/).
* Custom OIDC Token Mapper Example [@mschwartau/keycloak-custom-protocol-mapper-example](https://github.com/mschwartau/keycloak-custom-protocol-mapper-example).
* Discussions about custom OIDC token mapper on [stackoverflow](https://stackoverflow.com/questions/53089776/keycloak-add-extra-claims-from-database-external-source-with-custom-protocol-m).
* Custom User Storage Example [@thomasdarimont/keycloak-user-storage-provider-demo](https://github.com/thomasdarimont/keycloak-user-storage-provider-demo).

## Datasources in JBoss / Wildfly / Keycloak

* SPI with a third party database ... persistence.xml [JBoss pipermail](https://lists.jboss.org/pipermail/keycloak-user/2018-November/016462.html).
* How to get all defined datsources [Keycloak EntityManagerFactory sources](https://github.com/keycloak/keycloak/blob/master/model/jpa/src/main/java/org/keycloak/connections/jpa/util/JpaUtils.java#L47).
* Preferred way to make KeyCloak custom changes - Allow for extra entities in Hibernate besides persistence.xml [JBoss pipermail](https://lists.jboss.org/pipermail/keycloak-dev/2015-November/005844.html).
* How to get datasource via JNDI [Keycloak EjbExampleUserStorageProviderFactory sources](https://github.com/keycloak/keycloak-quickstarts/blob/latest/user-storage-jpa/src/main/java/org/keycloak/quickstart/storage/user/EjbExampleUserStorageProviderFactory.java).
* JBoss documetation [access.redhat.com](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/7.0/html/configuration_guide/datasource_management).
* [Some simplе article](http://www.mastertheboss.com/jboss-server/jboss-datasource/configuring-a-datasource-with-postgresql-and-jboss-wildfly).
* Lots of examples on [docs.jboss.org](https://docs.jboss.org/author/display/AS71/CLI%20Recipes.html#12484671_CLIRecipes-RemoveDefaultDatasourceandDriver).
* Why 2 datasources should be XA. [developer.jboss.org](https://developer.jboss.org/thread/259983).

## Docker

* Directories:
  * main scripts — `/opt/jboss/tools/`,
  * Keycloak home directory — `/opt/jboss/keycloak`.
  * directory for custom autorun scripts (`.sh` or [.cli](https://docs.jboss.org/author/display/WFLY/CLI%20Recipes.html)) — `/opt/jboss/startup-scripts/`.

* [Keycloak Cli Scripting](https://www.keycloak.org/docs/latest/server_installation/#cli-scripting).
* How to register module on start on [stackoverflow](https://stackoverflow.com/questions/58929318/cannot-connect-to-wildfly-in-dockerfile) (using `embed-sever` etc.),
* "Registering Module" example [@ieggel/DockerRegistryKeycloakUserNamespaceMapper](https://github.com/ieggel/DockerRegistryKeycloakUserNamespaceMapper).
* How to register a module in container [discussion](https://keycloak.discourse.group/t/how-to-package-extensions-in-a-docker-image/5542).
* Keycloak docker-compose examples [@trajakovic/keycloak-docker-compose](https://github.com/trajakovic/keycloak-docker-compose).

start / stop / restart

```shell
docker exec example_keycloak_1 /opt/jboss/keycloak/bin/jboss-cli.sh --connect command=:shutdown
```

### Database With Docker

[DB In Docker](http://www.mastertheboss.com/soa-cloud/docker/how-to-manage-a-postgresql-database-with-docker).

Run database script on start

```shell
docker exec -ti  example_postgres_1 /usr/bin/pg_dump --file "/var/tmp/init_data.sql" --host "localhost" --port "5432" --username "keycloak" --no-password --verbose --format=p "keycloak"
```
