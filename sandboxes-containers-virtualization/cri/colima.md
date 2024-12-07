# Colima

link: [https://github.com/abiosoft/colima/](https://github.com/abiosoft/colima/)

Использует lima: [https://github.com/lima-vm/lima](https://github.com/lima-vm/lima)

Platform: macos, linux

Управление docker и containerd контейнерами (как замена Docker Desktop, а точнее его платной части — docker engine)

Установка:

```
brew install docker  # Эта часть бесплатна
brew install colima
```

После установки, перезагружаем компьютер

## Возможные проблемы

### Не хватает прав для управления volumes на macOS

Следует обновить до 13-й оси (с этой версии в macos доступна virtiofs и виртуализация механизмами macos)

Удаляем все настройки и контейнеры:

```
colima delete
```

Запускаем с поддержкой виртуализации macos (не qemu) и virtiofs:

```
colima start -t vz --mount-type virtiofs
```

После снова собираем и запускаем наши образы

link: [https://github.com/abiosoft/colima/issues/1067](https://github.com/abiosoft/colima/issues/1067)

### docker контейнеры не резолвят dns имена

Оказывается, у colima своя виртуальная машина (подключиться через \`colima ssh\`) и свой конфиг, отличный от docker: \`\~/.colima/default/colima.yaml\`. Правим настройки dns серверов:

```
network:
    dns:
        - 8.8.8.8
        - 8.8.4.4
        - 1.1.1.1
```

Перезапускаем:

```
colima stop
colima start
```
