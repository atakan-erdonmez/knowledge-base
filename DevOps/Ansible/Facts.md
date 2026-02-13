It is the generic info about the client. It is run by the module 'setup'. It is run automatically.

```
tasks:
- debug:
	  var: ansible_facts
```

You can disable gathering facts in play via:
`gather_facts: no`