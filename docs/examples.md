Examples
--------

#### Manage global configuration

```YAML
prometheus_global_config:
  scrape_interval: '30s'
  scrape_timeout: '10s'
```

More informations in the official [documentation](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#configuration)

#### Manage scrape configurations

```YAML
prometheus_scrape_configs:
  - job_name: my-app
    static_configs:
      - targets: ['1.2.3.4:8000']
        labels:
          my_new_target_label: foo
```

More informations in the official `scrape_configs` [documentation](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#scrape_config)

#### Manage Remote Write/Read configuration

```YAML
prometheus_remote_write_enabled: true
prometheus_remote_write_config:
  - name: remote-write
    url: "https://1.2.3.4:9000/prometheus/remote/write"
    remote_timeout: 30s

prometheus_remote_read_enabled: true
prometheus_remote_read_config:
  - name: remote-read
    url: "https://1.2.3.4:9000/api/v1/read"
    remote_timeout: 30s
```

More informations in the official [Remote Write](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#remote_write) and [Remote Read](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#remote_read) documentations.

#### Manage alerting configuration

```YAML
prometheus_alerting_config:
  alertmanagers:
  - static_configs:
      - targets: ['localhost:9093']
```

More informations in the official alerting [documentation](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#alertmanager_config)

#### Manage alerting rules

There are two ways of configuring Prometheus alerting rules :

* **Using embedded template**

  ```YAML
  prometheus_alerting_rules:
  - group: mygroup
    rules:
    - alert: InstanceDown
      expr: up == 0
      for: 5m
      labels:
        severity: page
      annotations:
        summary: "{% raw %}Instance {{ $labels.instance }} down{% endraw %}"
        description: "{% raw %}{{ $labels.instance }} of job {{ $labels.job }} has been down for more than 5 minutes.{% endraw %}"
  ```
  
  **Note**: don't forget to use Jinja2 `raw` anchor to avoid issues with Go templating in your rules definitions.

* **Bring your own rules**

  You can also bring your own static rules files by specifying their paths (absolute or relative) on your Ansible controller. The rule files will be uploaded into the Prometheus configuration directory dedicated to alerting rules (default: `/etc/prometheus/rules`) :

  ```YAML
  prometheus_alerting_rules_files:
    - prometheus/rules/*.rules
    - /home/ansible/project/prometheus/rules/hardware.rules
  ```

More informations in the official [documentation](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/)
