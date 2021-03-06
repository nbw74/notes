IaC: подход к инфраструктуре как к коду
=======================================
Infractructure as code (IaC)  -- это подход к управлению вычислительной инфраструктурой, подразумевающий автоматизацию развертывания и управления инфраструктурой через составление конфигурационных файлов для спец. ПО, которое и производит все необходимые действия. Эти конфигурационные файлы (которые и называются "кодом" в аббревиатуре IaC) можно и нужно хранить в системах контроля версий.
### Цели IaC
+ снижение стоимости: при использовании данного подхода уменьшается время, затрачиваемое специалистами на настройку и поддержание инфраструктуры (уменьшается кол-во "ручной работы"), что высвобождает их время для задач, связанных с дальнейшим развитием бизнеса;
+ увеличение скорости выполнения операций: система IaC позволяет выполнять задачи по настройке инфраструктуры значительно быстрее "традиционных" методов, в том числе за счёт возможности интеграции с процессами других подразделений компании (например, связанных с развёртыванием приложений);
+ уменьшение рисков: автоматизация позволяет избежать рисков, связанных с человеческими ошибками (например, неверной конфигурации сервисов) и позволяет добавить автоматические проверки перед применением изменений.

Вот это последнее свойство мы и рассмотрим подробнее на примере практической реализации доставки обновлений (CD -- то, что изучали в предыдущем курсе) с предварительной проверкой работоспособности конфигурации -- т.н. "blue-green deployment". С помощью ansible мы настроим веб-серверы и балансировщик haproxy, а затем продемонстрируем процесс установки обновлений с переключением апстрима.

Для начала посмотрим, как организовать выполнение инфраструктурного кода "для людей", а не "только для избранных":
Хранение и применение конфигураций
=========================================
Тут объяснение того, что ансиблокод правильно хранить в гитлабе, для того, чтобы коллеги могли работать над ним удобно, прозрачно и совместно.
### Запуск инфраструктурного кода через гитлаб
Практика написания плейбуков и ролей
====================================
### Что такое playbooks, plays и roles, как их применять на примере ролей common, rails и haproxy.
- плейбуки -- то, с чего начинается ansible;
- плей как составная часть плейбука;
- roles (роли) -- это способ организации и переиспользования (reuse) кода. Конкретный состав и назначение ролей зависит от вашей инфраструктуры и приложений, но чаще всего делают одну или несколько ощих ролей (common или base), которые применяются ко всем системам, и набор специфических ролей, которые применяются только к определённым частям инфраструктуры.
### Как правильно писать плейбуки и роли, в каких случаях нужны роли, а в каких -- не очень
Тут можно развернуть мысли об оркестрации, поддержании конфигурации и переиспользовании кода (когда оно уместно и когда нет). Также можно довести вытекающую из переиспользования идею о максимальной автономности ролей.
### Идемпотентность -- важное свойство инфраструктурного кода
И сразу продемонстрировать, как ведёт себя идемпотентный код.
### Императивный код в ролях и декларативное описание конфигурации в inventory
Blue-green deployment
=====================
### Практика деплоя с переключением апстримов.
