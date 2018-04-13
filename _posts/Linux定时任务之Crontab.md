crontab -u //设定某个用户的cron服务，一般root用户在执行这个命令的时候需要此参数 
crontab -l //列出某个用户cron服务的详细内容 
crontab -r //删除没个用户的cron服务 
crontab -e //编辑某个用户的cron服务

基本用法: 
1. crontab -l 
     列出当前的crontab任务 
2. crontab -d 
     删除当前的crontab任务 
3. crontab -e (solaris5.8上面是 crontab -r) 
     编辑一个crontab任务,ctrl_D结束 
4. crontab filename 
     以filename做为crontab的任务列表文件并载入

crontab file的格式: 
    crontab 文件中的行由 6 个字段组成，不同字段间用空格或 tab 键分隔。前 5 个字段指定命令要运行的时间 
       分钟 (0-59) 
       小时 (0-23) 
       日期 (1-31) 
       月份 (1-12) 
       星期几（0-6，其中 0 代表星期日） 
       第 6 个字段是一个要在适当时间执行的字符串 
例子: 
      #MIN HOUR DAY MONTH DAYOFWEEK COMMAND 
      #每天早上6点10分 
      10 6 * * * date 
      #每两个小时 
      0 */2 * * * date    (solaris 5.8似乎不支持此种写法) 
      #晚上11点到早上8点之间每两个小时，早上8点 
      0 23-7/2，8 * * * date 
      #每个月的4号和每个礼拜的礼拜一到礼拜三的早上11点 
      0 11 4 * mon-wed date 
      #1月份日早上4点 
      0 4 1 jan * date