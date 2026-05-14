# Домашнее задание к занятию «Кластеризация и балансировка нагрузки»

## Задание 1. Балансировка Round‑robin на 4-м уровне (TCP)
- Запущены два Python-сервера на портах `8001` и `8002` с разными index.html.
- Настроен HAProxy в режиме `mode tcp` на порту `8080`.
- Алгоритм балансировки: `roundrobin`.
- **Результат:** запросы к `http://localhost:8080` поочерёдно попадают на первый и второй сервер.


<img width="601" height="246" alt="image" src="https://github.com/user-attachments/assets/e1eab782-10d1-4a3d-b2e5-7da94e17de8e" />

https://github.com/Almsst/sflt-haproxy-lab/blob/master/haproxyzd1.cfg

## Задание 2. Взвешенный Round‑robin на 7-м уровне (HTTP) + привязка к домену
- Запущены три Python-сервера на портах `8003`, `8004`, `8005`.
- HAProxy переключён в режим `mode http` на порту `8081`.
- Добавлен ACL по заголовку `Host: example.local`.
- В бэкенде заданы веса:  
  - сервер `8003` — вес 1  
  - сервер `8004` — вес 2  
  - сервер `8005` — вес 3  
- **Результат:** при обращении с доменом `example.local` запросы распределяются пропорционально весам (примерно 1:2:3).

<img width="600" height="292" alt="image" src="https://github.com/user-attachments/assets/9dc333a1-fa3e-492e-b32f-a79564364018" />

<img width="597" height="402" alt="image" src="https://github.com/user-attachments/assets/27534ceb-c3f1-4541-8d58-d0796eaf51c7" />

