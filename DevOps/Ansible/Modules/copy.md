It is to deal with the content of a file

```
- name: Configure Docker storage driver
  copy:
    dest: /etc/docker/daemon.json
    content: |
      {
        "storage-driver": "overlay2"
      }
    owner: root
    group: root
    mode: '0644'
```