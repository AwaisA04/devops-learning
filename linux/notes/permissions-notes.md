# Permissions and ownership challenge

## task
Create a file that the owner can read and write, while group members and others can only read.

## command

'''text
touch permissions.txt
chmod 644 permissions.txt
ls -l permissions.txt
'''

## result

```text
-rw-r--r--
```

## explanation

`chmod 644` sets:

- Owner: read + write (`rw-`)
- Group: read only (`r--`)
- Others: read only (`r--`)