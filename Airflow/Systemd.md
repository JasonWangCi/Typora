| Systemd command                | Sysvinit command             |
| ------------------------------ | ---------------------------- |
| systemctl start service_name   | service service_name start   |
| systemctl stop service_name    | service service_name stop    |
| systemctl restart service_name | service service_name restart |
| systemctl status service_name  | service service_name status  |
| systemctl enable service_name  | chkconfig service_name on    |
| systemctl disable service_name | chkconfig service_name off   |