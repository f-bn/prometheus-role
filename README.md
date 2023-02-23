<p><img src="https://cncf-branding.netlify.app/img/projects/prometheus/horizontal/color/prometheus-horizontal-color.svg" alt="prom-logo" title="prom" align="top" height=80 /></p>

*Prometheus, a Cloud Native Computing Foundation project, is a systems and service monitoring system. It collects metrics from configured targets at given intervals, evaluates rule expressions, displays the results, and can trigger alerts when specified conditions are observed*

### General informations

***Work in progress***

This Ansible role is designed to deploy and configure Prometheus instance(s) on target server(s).

**Table of Contents**

  - [Roles variables](#role-variables)
  - [Examples](#examples)
  - [Install and use this role](#install-and-use-this-role)

**References**

  - Prometheus : https://prometheus.io/

**Implementation notes**

  - ***AlertManager*** : this role only installs Prometheus server and doesn't setup AlertManager service
  - ***Supported architectures*** : this role only supports Linux on amd64 architecture for now

### Role variables

The role variables documentation are available here :

| Name                              | Default                      | Description                                                      |
| :-------------------------------- | :--------------------------- | :--------------------------------------------------------------- |
| `prometheus_version`              | `2.42.0`                     | Defines the version of Prometheus to install                     |
| `prometheus_install_dir`          | `/usr/local/bin`             | Defines the Prometheus binaries installation directory           |
| `prometheus_config_dir`           | `/etc/prometheus`            | Defines the Prometheus configuration directory                   |
| `prometheus_data_dir`             | `/var/lib/prometheus`        | Defines the Prometheus TSDB data directory                       |
| `prometheus_custom_args`          | `[]`                         | Defines the extra arguments to pass to the Prometheus process when starting the instance |
| `prometheus_binary_update`        | `false`                      | If set to `true`, force the Prometheus binaries update (if binary version is different)  |
| `prometheus_global_config`        | see [defaults](defaults/main.yml)| Defines the Prometheus global configuration                  |
| `prometheus_remote_write_enabled` | `false`                      | If set to `true`, enable Remote Write configuration              |
| `prometheus_remote_write_config`  | `{}`                         | Defines the Prometheus Remote Write configuration                |
| `prometheus_remote_read_enabled`  | `false`                      | If set to `true`, enable Remote Read configuration               |
| `prometheus_remote_read_config`   | `{}`                         | Defines the Prometheus Remote Read configuration                 |
| `prometheus_scrape_configs`       | `{}`                         | Defines the Prometheus scrape configurations                     |
| `prometheus_alerting_config`      | `{}`                         | Defines the Prometheus alerting configuration (AlertManager)     |
| `prometheus_alerting_rules`       | `{}`                         | Defines the Prometheus alerting rules using 
| `prometheus_alerting_rules_files` | `{}`                         | If non-empty, upload the file at the given path(s) from the Ansible controller to the Prometheus rules directory |
| `prometheus_storage_retention_time`| `15d`                       | Defines the Prometheus TSDB metrics retention time (see official [documentation](https://prometheus.io/docs/prometheus/latest/storage/) for details |
| `prometheus_storage_retention_size`| `0`                         | Defines the Prometheus TSDB metrics retention size (see official [documentation](https://prometheus.io/docs/prometheus/latest/storage/) for details | 
| `prometheus_web_listen_address`   | `0.0.0.0:9090`               | Defines the Prometheus endpoint address                          |
| `prometheus_web_config_path`      | `{{ prometheus_config_dir }}/web.yaml` | Defines the Prometheus web endpoint configuration file path |
| `prometheus_web_config`           | `{}`                         | Defines the Prometheus web endpoint configuration                |

### Examples

You can find some configurations examples :

  - [Manage global configuration](docs/examples.md#manage-global-configuration)
  - [Manage scrape configurations](docs/examples.md#manage-scrape-configurations)
  - [Manage Remote Write/Read configuration](docs/examples.md#manage-remote-writeread-configuration)
  - [Manage alerting configuration](docs/examples.md#manage-alerting-configuration)
  - [Managed alerting rules](docs/examples.md#manage-alerting-rules)

### Install and use this role

* Install the role using the command-line :

  ```shell
  $ ansible-galaxy role install git+https://github.com/f-bn/prometheus-role.git prometheus
  ```

* You can also install the role in your projects using a `requirements.yml` file and `ansible-galaxy` command-line :

  ```YAML
  $ cat requirements.yml
  ---
  roles:
    - name: prometheus
      src: https://github.com/f-bn/prometheus-role.git
      scm: git
      version: '1.0.0'

  $ ansible-galaxy install-f -r requirements.yml
  ```

* Once the role is installed, you can use it in your playbooks :

  ```yaml
  - name: Deploy
    hosts: <hosts>
    roles:
      - role: prometheus
  ```
