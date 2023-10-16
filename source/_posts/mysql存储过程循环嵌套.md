---
title: mysql存储过程循环嵌套
date: 2023-10-06 08:47:00
excerpt: mysql存储过程循环嵌套。
tags: [mysql]
categories: mysql
---
## Docker 安装 MySQL
```
CREAT DEFINER=`root`@`%` PROCEDURE `name`(IN `PARM1` VARCHAR(300),OUT `OUTPUT` VARCHAR(300))
BEGIN
    -- 定义一个变量，默认为0
	DECLARE no_more_record INT DEFAULT 0;
	-- 定义变量给游标获取数据
	DECLARE p_id int(11);

	-- 定义一个游标，并将指定数据存入到游标
	DECLARE curl CURSOR FOR SELECT id from places where `level`=6 AND id<>1293;
	-- 当游标没有数据时，设定变量为1
	DECLARE CONTINUE HANDLER FOR NOT found SET no_more_record =1;

-- 打开游标
OPEN curl;
-- 获取游标的更新
FETCH curl INTO p_id;
	-- 当变量不为1时，执行操作
	WHILE no_more_record !=1 DO 
        BEGIN
	    -- 定义第二个变量给另一个游标获取数据（根据特定的情况来定义不同的变量）
	    DECLARE o_id int(11);
	    -- 定义一个游标，并将指定数据存入到游标
        DECLARE curl2 CURSOR FOR select id from objects where id>=1376 AND id<=1381;
	    -- 当游标没有数据时，设定变量为1
	    DECLARE CONTINUE HANDLER FOR NOT found SET no_more_record2 =1;
		-- 打开第二个游标
		OPEN curl2;
		-- 获取第二个游标的更新
		FETCH curl2 INTO o_id;
			-- 同上，当变量不为1时，往下执行操作
			WHILE no_more_record2 !=1 DO
				-- 向关联表中插入数据，此时插入的数据为第一个游标获取的第一个数据，另，第二个游标获取的一批数据会一行一行的执行插入到目标表中，直至第二个游标没有数据时，结束，即while语句结束
				set @sql='INSERT INTO space_object(object_id,place_id,number,created_at,updated_at) VALUES('||o_id||','||'p_id'||',0,NOW(),NOW())';
                execute sql;
				-- 继续获取数据循环
				FETCH curl2 INTO o_id;
			-- 当第二个游标的数据循环到最后没有数据时，变量no_more_record为1，停止循环
			END WHILE;
		-- 关闭游标2
		CLOSE curl2;
        END
    -- 游标1获取更新并循环直至结束
    FETCH curl INTO p_id;
	END while ;
CLOSE curl;
END
```