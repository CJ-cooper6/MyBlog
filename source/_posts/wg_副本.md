

```
docker run -d -p 8888:5000 -e USER_EXTERNAL_QUERY_FIELD=username --name core_data_console registry.cn-hangzhou.aliyuncs.com/wg-common/core-data-console:1.4.develop-c7d735fa /opt/docker-entrypoint.sh

docker run -d -p 8888:5000 \
-e USER_EXTERNAL_QUERY_FIELD=username \
--name core_data_console \
registry.cn-hangzhou.aliyuncs.com/wg-common/core-data-console:1.4.develop-c7d735fa \
/opt/docker-entrypoint.sh


docker run -d -p 8888:5000 \
-e USER_EXTERNAL_QUERY_FIELD=username \
--name core_data_console \
registry.cn-hangzhou.aliyuncs.com/wg-common/core-data-console:1.4.develop-c7d735fa \
/opt/docker-entrypoint.sh –privileged=true

```

/opt/apps/core-data-console





该用户拥有的应用：

selectedApplicationIds



所有应用：

allApplications







可以控制个人应用和自己角色的应用

