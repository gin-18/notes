# mongodb

---

[TOC]

## 用户管理

---

### 添加用户

---

```javascript
db.createUser({user:"<username>", pwd:"<password>", roles:[{role:"<role>", db:"<db>"}]})
```

role说明：

| 角色           | 说明                                                                            |
|----------------|---------------------------------------------------------------------------------|
| 数据库用户角色 | read、readWrite                                                                 |
| 数据库管理角色 | dbAdmin、dbOwner、userAdmin                                                     |
| 集群管理角色   | clusterAdmin、clusterManager、clusterMonitor、hostManager                       |
| 备份恢复角色   | backup、restore                                                                 |
| 所有数据库角色 | readAnyDatabase、readWriteAnyDatabase、userAdminAnyDatabase、dbAdminAnyDatabase |
| 超级用户角色   | root                                                                            |

