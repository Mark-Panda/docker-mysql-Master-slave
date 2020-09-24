
从数据库
    show master status;
    show  slave status;

    CHANGE MASTER TO
		MASTER_HOST='mysql',
		MASTER_USER='root',
		MASTER_PASSWORD='prisma',
		MASTER_LOG_FILE='replicas-mysql-bin.000003',
		MASTER_LOG_POS=154;
    stop slave;
    start slave;


    reset slave all;  #清除主从复制


主数据库
    show master status;


    show binlog events in 'replicas-mysql-bin.000001';

    #暂时不讲操作追加到Bin日志中   基于会话层面的  只针对当前连接的会话，其他会话不影响，但是如果设置的是（set global sql_log_bin=0)，这样会导致所有在Master数据库上执行的语句都不记录到binlog
    SET sql_log_bin=1;  #开启
    SET sql_log_bin=0;  #关闭

    show variables like "sql_log_bin";



    SET FOREIGN_KEY_CHECKS=0;
    -- ----------------------------
    -- Table structure for course
    -- ----------------------------
    DROP TABLE IF EXISTS `course`;
    CREATE TABLE `course` (
      `id` int(11) NOT NULL AUTO_INCREMENT,
      `name` varchar(20) NOT NULL,
      `lesson_period` double(5,0) DEFAULT NULL,
      `score` double(10,0) DEFAULT NULL,
      PRIMARY KEY (`id`)
    ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
