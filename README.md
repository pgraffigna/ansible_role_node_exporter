# ansible_role_prometheus_grafana_telegraf

Ansible Playbook para configurar node_exporter de prometheus en clientes para recoger metricas de los equipos.

Testeado con Vagrant + qemu + ubuntu_20.04 + ansible_2.10.

----

roles:
- telegraf
- prometheus
- grafana
- node_exporter

----

archivos:
- prometheus.yml
- node_exporter.service

----

notas:
- for loop para creacion de jobs dinamicos en prometheus.yml

```yaml
scrape_configs:
{% for client in groups['clientes'] %}
  - job_name: "{{ hostvars[client]['nodo'] }}"
    scrape_interval: 5s
    static_configs:
      - targets: ["{{ hostvars[client]['inventory_hostname'] }}:9100"]
{% endfor %}
```

- [dashboard para grafana](https://grafana.com/grafana/dashboards/15172-node-exporter-for-prometheus-dashboard-based-on-11074/)