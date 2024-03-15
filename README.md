# cisco_acl_redirect

Генерация acl для L4 redirct по файлу с URL

## Описание

Клонируем репозиторий.
В файле white.txt находятся URL к которым необходимо обеспечить доступ.

Для корректной работы необходимы утелиты:
- dig
- whois

Логика работы скрипта:
- Получаем ip адреса по URL
- Определяем AS которой принадлежит данный IP
- Далее получаем список IPv4 сетей данной AS
- Конвертируем маску подсети в wildcard
- Генерируем ACL в файл cisco_acl.txt

ACL необходимо добавить в ip access-list extended traffic-for-redirect
Также добавляем следующие ACL:
- 1 deny tcp any 62.76.205.0 0.255.255.255 eq 443 
- 2 deny tcp any 185.170.2.0 0.255.255.255 eq 443 
- 1000 permit tcp any any eq www
- 1001 permit tcp any any eq 443

