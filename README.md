
 #        OCTOPUS LINUX NETWORK CONFIGURATOR

Автор / Author: alinababenko.work@gmail.com

Версия / Version: 2.1 (Stable - TMP Edition 🐙)

-----------------------------------------------------

## [RU] ПОЛЬЗОВАТЕЛЬСКАЯ ИНСТРУКЦИЯ

### ОПИСАНИЕ:
Автоматизированный инструмент для настройки сети (NAT, DHCP, DNS, SSH).
Работает полностью оффлайн. В версии 2.1 добавлена самоизоляция в /tmp.

### КАК ЗАПУСТИТЬ:
1. Примонтируйте ISO-образ (например, в /mnt/cdrom):
```bash
   sudo mkdir -p /mnt/cdrom
   sudo mount /dev/sr0 /mnt/cdrom
   ```

2. Запустите установку прямой командой:
```bash
   sudo bash /mnt/cdrom/autostart.sh
   ```

### ЧТО ПРОИСХОДИТ ПОСЛЕ ЗАПУСКА:
- МИГРАЦИЯ: Скрипт автоматически копирует себя в /tmp/octopus_config.
- ПРАВА: Все необходимые права доступа (chmod) назначаются автоматически.
- ЧИСТОТА: После перезагрузки рабочая папка в /tmp будет удалена системой.
- ОТЧЕТ: Финальный отчет будет сохранен в домашнюю папку пользователя:
  ~/machine_report.txt

-----------------------------------------------------

## [EN] USER MANUAL

### DESCRIPTION:
Automated tool for network configuration (NAT, DHCP, DNS, SSH).
Fully offline. Version 2.1 features self-isolation in /tmp.

### HOW TO RUN:
1. Mount the ISO image (e.g., to /mnt/cdrom):
```bash
   sudo mkdir -p /mnt/cdrom
   sudo mount /dev/sr0 /mnt/cdrom
   ```

2. Run the installation with a single command:
```bash
   sudo bash /mnt/cdrom/autostart.sh
   ```

### WHAT HAPPENS AFTER START:
- MIGRATION: The script automatically copies itself to /tmp/octopus_config.
- PERMISSIONS: All necessary access rights (chmod) are assigned automatically.
- CLEANUP: The working directory in /tmp will be cleared by the OS after reboot.
- REPORT: The final report will be saved to the user's home directory:
  ~/machine_report.txt

=====================================================
