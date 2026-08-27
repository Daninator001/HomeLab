# HomeLab  

## Introduction  

The purpose of the repository is to publish my experiments on my personal HomeLab and to remind some practice on tools.

## PCloud  
PCloud is a cloud drive service. I use pcloudcc to secure my NAS archives.

## Troubleshoot

When pcloud status is BAD_LOGIN_TOKEN, verify the repository is up-to-date and then run
  ```bash
  sqlite3 ~/.pcloud/data.db
  sqlite> delete from setting where id='auth';
  sqlite> <ctrl-D>
  pcloudcc -u <<userlogin>> -p -s
  ```
Type password when asked, sychronization should be restored
