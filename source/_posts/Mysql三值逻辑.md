

Mysql三值逻辑
Mysql 使用三值逻辑 True、False、UNKNOWN
和NULL做比较时会和 UNKNOWN 做比较
所以Mysql提供了is NULL 和 is NOT NULL来对NULL做判断
在查询时，如果要包括值为NULL的情况，WHERE语句中需要额外判断is NULL



~~select * from user where user_id != 2;~~ 
select * from user where user_id != 2 or user_id is NULL; (正确)