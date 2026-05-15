# Домашнее задание к занятию «Кластеризация и балансировка нагрузки»

## Задание 1. Балансировка Round‑robin на 4-м уровне (TCP)
- Запущены два Python-сервера на портах `8001` и `8002` с разными index.html.
- Настроен HAProxy в режиме `mode tcp` на порту `8080`.
- Алгоритм балансировки: `roundrobin`.
- **Результат:** запросы к `http://localhost:8080` поочерёдно попадают на первый и второй сервер.


<img width="601" height="246" alt="image" src="https://github.com/user-attachments/assets/e1eab782-10d1-4a3d-b2e5-7da94e17de8e" />

[haproxyzd1.cfg](https://github.com/Almsst/sflt-haproxy-lab/blob/master/haproxyzd1.cfg)

## Задание 2. Взвешенный Round‑robin на 7-м уровне (HTTP) + привязка к домену
- Запущены три Python-сервера на портах `8003`, `8004`, `8005`.
- HAProxy переключён в режим `mode http` на порту `8081`.
- Добавлен ACL по заголовку `Host: example.local`.
- В бэкенде заданы веса:  
  - сервер `8003` — вес 1  
  - сервер `8004` — вес 2  
  - сервер `8005` — вес 3  
### Проверка с доменным именем (`Host: example.local`)
Запросы распределяются пропорционально весам

<img width="601" height="292" alt="image" src="https://github.com/user-attachments/assets/8d887ae5-50f2-4def-978a-561e3407dbc7" />

### Проверка без доменного имени
Запросы **не попадают** на взвешенные серверы

<img width="597" height="295" alt="image" src="https://github.com/user-attachments/assets/318ec4ee-2dbc-42f2-82fd-e99e3681306a" />

[haproxy.cfg](https://github.com/Almsst/sflt-haproxy-lab/blob/master/haproxy.cfg)






