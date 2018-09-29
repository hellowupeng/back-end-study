# session

##### session用途
跟踪用户信息，对登录用户记录sessionID（UUID），把sessionID和对应用户信息进行缓存（redis），把sessionID写入Cookie，用户请求时根据sessionID从缓存中获取用户信息，然后根据用户信息查找数据库信息。
