##RU

# OpenVPN Wazuh Logging for OPNsense

Этот проект содержит:

- Cкрипты логирования OpenVPN-подключений на OPNsense
- Кастомный дополнительный декодер для Wazuh
- Дополнительные правила обнаружения для мониторинга активности VPN

## Содержимое

- `scripts/user-connected-logging.sh`          scripts/ — Bash-скрипты, читающий `openvpn-status.log` и отправляющий данные
- `scripts/user-disconnected-logging.sh`
- `wazuh/decoders/custom-decoder.xml` — Декодер для разбора логов
- `wazuh/rules/custom-rules.xml` — Правила для генерации событий в Wazuh

## Использование

1. Разместите bash скрипты на OPNsense в `/usr/local/bin/` и добавьте в cron.
2. Импортируйте декодер и правила в Wazuh.
3. Перезапустите wazuh-manager на сервере после добавления. На Opnsense перезапускать ничего не нужно, только добавить в ossec.conf строчку куда сохраняются логи подключений openvpn

```
<localfile>
  <log_format>syslog</log_format>
  <location>/var/log/название-логфайла-исходя-из-скриптов-логгирования.log</location>
</localfile>
```




-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
##EN
# OpenVPN Wazuh Logging for OPNsense

This project includes:

- Bash scripts for logging OpenVPN connection events on OPNsense
- A custom decoder for Wazuh to interpret the logs
- Custom detection rules for monitoring VPN activity

## Contents

- `scripts/user-connected-logging.sh` — Script for detecting and logging user connections
- `scripts/user-disconnected-logging.sh` — Script for detecting and logging user disconnections
- `wazuh/decoders/custom-decoder.xml` — Custom Wazuh XML decoder
- `wazuh/rules/custom-rules.xml` — Wazuh rules to generate alerts based on OpenVPN activity

## Usage

1. Upload the bash scripts to your OPNsense system (e.g., `/usr/local/bin/`) and schedule them via `cron` or a system hook.
2. Import the decoder and rules into your Wazuh manager:
   - Place the decoder in `/var/ossec/etc/decoders/`
   - Place the rules in `/var/ossec/etc/rules/`
   - Restart the Wazuh manager with: `systemctl restart wazuh-manager`

3. Add in ossec.conf on your OpnSense new rows

```
<localfile>
  <log_format>syslog</log_format>
  <location>/var/log/название-логфайла-исходя-из-скриптов-логгирования.log</location>
</localfile>
```


---

This setup allows centralized monitoring of OpenVPN sessions using Wazuh, enhancing your VPN audit capabilities and improving network security visibility.
