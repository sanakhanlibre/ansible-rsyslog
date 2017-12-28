# Rsyslog Ansible role

[![The MIT License](https://img.shields.io/badge/license-MIT-orange.svg?style=flat-square)](http://opensource.org/licenses/MIT)

This role manages configuration of `rsyslog` client and makes sure that it's installed.

## Requirements & Dependencies

### Ansible
It was tested on the following versions:
 * 1.9

### Operating systems

Currently the module was only tested on Debian.

### Role variables

 * `rsyslog_conf_file`: string, the path to `rsyslog.conf`
 * `rsyslog_d_dir`: string, where are the config files`
 * `rsyslog_user`: the owner group of `rsyslog.conf`
 * `rsyslog_group`: the owner user of `rsyslog.conf`


### Specific variables

Rsyslog support traffic encryption with TLS (SSL). [More info](http://www.rsyslog.com/doc/v8-stable/tutorials/tls_cert_summary.html)

To enable it, `ca_certificate` must be defined.

*Default configuration* :
```yaml
    rsyslog_udp: True
    rsyslog_udp_port: 514

    rsyslog_tcp: True
    rsyslog_tcp_port: 514
    rsyslog_default_template: RSYSLOG_TraditionalFileFormat
    
    rsyslog_parameters: |
      module(load="imfile")   # provides kernel logging support
      input (type="imfile"
      File="/var/log/*test.log"
      Tag="test-log"
      Severity="info"
      Facility="local3"
      addMetadata="on")
      $template test,"%TIMESTAMP% %HOSTNAME% %APP-NAME% [%$!metadata!filename%]: %msg%\n"
 
    rsyslog_server_logging_udp: example.fr
    rsyslog_server_logging_udp_port: 5253
    
    rsyslog_server_logging_tcp: example.fr
    rsyslog_server_logging_tcp_port: 2992

    rsyslog_server_tcp_send_with_template: test
    rsyslog_server_tcp_send_with_template: test
    
    ca_certificate: True
    ca_certificate_path: /etc/ssl/certs/ca-cert.pem
    
```

  
