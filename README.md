<p><img src="https://cncf-branding.netlify.app/img/projects/prometheus/horizontal/color/prometheus-horizontal-color.svg" alt="prom-logo" title="prom" align="top" height=80 /></p>

*Prometheus is an open-source systems monitoring and alerting toolkit originally built at SoundCloud. Since its inception in 2012, many companies and organizations have adopted Prometheus, and the project has a very active developer and user community*

### General informations

This Ansible role is designed to deploy and configure Prometheus instance(s) on target server(s).

**Table of Contents**

  - [Roles variables](#role-variables)
  - [Examples](#examples)
  - [Install and use this role](#install-and-use-this-role)

**References**

  - Prometheus : https://prometheus.io/

### Role variables

The role variables documentation are available here :

  - [General](docs/variables.md)

### Examples

You can find some configurations examples :

  - [Example](docs/examples.md)

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
