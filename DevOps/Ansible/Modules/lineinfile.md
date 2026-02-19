It checks if a line exists in a file

### Example 1
```
    - name: Set journald storage to persistent
      lineinfile:
        path: /etc/systemd/journald.conf
        regexp: '^#?Storage='
        line: Storage=persistent
		state: present 
```
In this example, it looks for the regex in the specified file. If it finds, it changes the value. If it doesn't, it adds to the end of file

### Example 2
```
    - name: Use older but stable USB drive, to cmdline.txt
      lineinfile:
        path: /boot/firmware/cmdline.txt
        backrefs: yes
        regexp: '^(?!.*usb-storage\.quirks={{ ssd_adapter_id }}:u)(.*)$'
        line: 'usb-storage.quirks={{ ssd_adapter_id }}:u \1'
```

In this example, it looks for a more complex regex. Since backrefs is enabled, if it doesn't find the regex, *it doesn't do anything*. 

One thing to note, in this example, negative search used. It means if the regex is not found, it will modify the line. If it finds it, it doesn't do anything.