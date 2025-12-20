Для эмуляции на основе `qemu/kvm` необходимы следующие компоненты:

- `virt-manager` — GUI для работы с `libvirt` и `qemu`. Позволяет подключаться к локальному и/или удалённому экземпляру `qemu/kvm`. Поключение к удалённому экземпляру `libvirt` и просмотр консоли удалённой эмулируемой машины обеспечивает ssh-туннель.

- `qemu` — программа, умеющая эмулировать различные процессоры и другое оборудование.

- `libvirt` — библиотека для работы с `kvm` из _пространства пользователя_.

- `kvm` — гипервизор, модуль находящийся в ядре системы, значительно ускоряющий выполнение эмулируемой машины в `qemu`.

```bash
sudo xbps-install -Su virt-manager libvirt qemu
```

Добавляем себя к группам пользователей-эмуляторов:

```bash
sudo usermod -aG kvm $USER
sudo usermod -aG libvirt $USER
```

**Активация необходимых служб:**

```bash
# Основная служба libvirt
sudo ln -s /etc/sv/libvirtd /var/service/
sudo ln -s /etc/sv/virtlockd /var/service/
sudo ln -s /etc/sv/virtlogd /var/service/
```

Улучшаем производительность 

```bash
# Установка дополнительных кодеков и библиотек
sudo xbps-install \
    spice-vdagent \
    spice-gtk \
    libguestfs \
    seabios \
    edk2-ovmf \
    virtiofsd

# Для Windows гостей (опционально)
sudo xbps-install virtio-win
```

