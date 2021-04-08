# Zephyr Hardware Results Dashboard
## Using Docker Compose

To start the app:

1. Install [docker-compose](https://docs.docker.com/compose/install/) on the docker host.
1. Optionally, change default credentials or Grafana provisioning.
1. Run the following command from the root of the cloned repo:
```
docker-compose up -d
```
(Change port if port 3001 is already used)

To stop the app:

1. Run the following command from the root of the cloned repo:
```
docker-compose down
```

Grafana will be accessible on your server ip address on port 3000.

Clone both repos:

 - https://github.com/zephyrproject-rtos/zephyr.git
 - https://github.com/zephyrproject-rtos/test_results.git

into your workspace.

Change the configuration in the script import.sh and make sure the following
variables reflect what you have created above:


	RESULTS_REPO_PATH=/path/to/test_results
	ZEPHYR_REPO_PATH=/path/to/zephyr/
	INFLUX_DB=influxdb://<server-ip>:8086/zephyr_test_results

Import the data using the ``import.sh`` script.

In grafana, create a new data source and add the above database you have just created.

There are 2 ways the import script can be called:

- Bulk import: This will import all results (v2.5.0 results) in one call. For
  this, call the script without any arguments
- Single Run: Specify the commit you want to import as the first argument to import.sh
- Commit import: Only import new files that are part of a single commit. The
  first argument should be a commit hash in the test_results repo
