# session

##### 相关问题

1 session用途？跟踪用户信息：对登录用户生成SessionID（UUID），把SessionID和对应用户信息进行缓存（redis），把SessionID写入Cookie，用户请求时根据SessionID从缓存中获取用户信息，然后根据用户信息查找数据库信息。