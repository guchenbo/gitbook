# Oracle几点
### 修改表空间
表：
    
    alter table 表名 move tablespace 新表空间名;
索引重建：

    alter index 索引名 rebuild
LOB字段：
    
    ALTER TABLE 表名 MOVE LOB(lob字段名) STORE AS (TABLESPACE 新表空间名);


