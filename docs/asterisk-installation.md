# Установка Asterisk через Ansible

1. Установка пакетов Asterisk.
2. Настройка PJSIP (транспорт, абонент 1001).
3. Настройка extensions.conf (Echo Test на 600, звонки на 1001).
4. Настройка manager.conf (доступ для asterisk_exporter).

Все конфиги хранятся в `ansible/roles/asterisk/templates/`.
