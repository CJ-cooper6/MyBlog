---
title: alembic

---



数据库迁移与版本控制工具，用于在数据库模式发生变化时进行管理。

## 常用命令

**初始化alembic环境**

```
alembic init migrations
```



**创建空的迁移脚本**

```
alembic revision -m "delete_waste_tables"
```

`-m` 参数用于描述此次迁移的目的。



**升级数据库**

```
alembic upgrade head
```

`head` 表示最新的迁移版本



**降级数据库**

```
alembic downgrade <revision>
```

`<revision>` 是要降级到的迁移版本。



**查看迁移历史**

```
alembic history
```



**显示当前版本**

```
alembic current
```

