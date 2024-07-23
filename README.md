Playbook для мониторинга сайта
Этот плейбук устанавливает сервисы Prometheus и Grafana на операционной системе CentOS8, добавляет источник данных Prometheus (размещенный на этом же сервере) в Grafana и загружает дашбоард 1860. Адрес сервера задается в файле inventory/hosts в группе [monitoring].

Для запуска используйте следующую команду:

bash
Копировать код
ansible-playbook --private-key PRIVATE_KEY_PATH -i inventory site-monitoring.yml
Playbook для node_exporter
Этот плейбук устанавливает сервис node_exporter на хосты, указанные в файле inventory/hosts в группе [target].

Для запуска используйте следующую команду:

bash
Копировать код
ansible-playbook --private-key PRIVATE_KEY_PATH -i inventory site-node_exporter.yml
Конфигурационный файл prometheus.yml динамически обновляется в зависимости от хостов, указанных в группе [target] файла inventory/hosts. Чтобы применить изменения, добавьте хост в группу [target] и запустите плейбук site-monitoring.

Скрипт add_annotation
Этот скрипт добавляет аннотацию с текущим временем на дашборд Grafana.

Необходимо создать сервисную учетную запись: перейдите в Administration -> Users and access -> Service accounts -> Add service account, укажите имя учетной записи и выберите роль Editor. Затем сгенерируйте и сохраните токен, выбрав Add service account token.

Также нужно получить DASHBOARD_ID и PANEL_ID. Для этого откройте дашборд и раскройте панель (нажмите на значок троеточия на панели и выберите пункт view). В адресной строке браузера orgId будет соответствовать DASHBOARD_ID, а viewPanel будет соответствовать PANEL_ID.

Внесите полученные данные, а также адрес сервера Grafana, в скрипт add_annotation.sh. Параметры TAG и TEXT укажите по своему усмотрению.