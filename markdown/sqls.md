# sql
### queryAlbumsByCategoryId

```
SELECT DISTINCT t.*  FROM duotin_album t INNER JOIN duotin_category_album ca ON t.id=ca.album_id WHERE 1=1 and t.content_count>0 AND ca.is_del=0 AND t.is_del =0 AND t.status = 1 AND ca.category_id =550 AND t.is_excellent =1;
```

### selectGroupByContentByTime
select sum(a.random_times) as listen_num,a.track_id,a.album_id from (select random_times,track_id,album_id from duotin_user_listen_history_2016_12 where created_at BETWEEN '2016-12-01 00:00:00' and '2016-12-07 23:59:59' order by null) a group by a.track_id order by listen_num desc;
### selectGroupByContent
select sum(random_times) as listen_num, track_id, album_id from duotin_user_listen_history_2016_11 group by track_id order by listen_num desc;

### 专辑日订阅量，selectGroupByAlbumIdWithCreatedAt


### 本年度主播上传节目榜

```
select b.id,b.realname,a.counts from dt_www.duotin_users b,(select count(b.user_id) as counts,b.user_id from duotin_content a,duotin_album b where a.album_id =b.id and a.status=1 and a.is_del=0 and a.created_at>='2016-01-01 00:00:00' group by b.user_id) a where a.user_id=b.id and b.is_podcaster=1 order by a.counts desc;
```

#### selectHistoryGroupByContentId
```
select sum(a.random_times) as random_times,a.track_id,sum(time_to_sec(a.progress)) as progress,a.album_id from (select track_id,random_times,progress,album_id from duotin_user_listen_history_2016_12 where created_at between '2016-12-15 00:00:00' and '2016-12-15 23:59:59' order by track_id) a group by a.track_id;
```
#### selectHistoryGroupByAlbumId
```
select sum(a.random_times) as random_times,a.album_id,sum(time_to_sec(a.progress)) as progress from (select album_id,random_times,progress from duotin_user_listen_history_2016_12 where created_at between '2016-12-15 00:00:00' and '2016-12-15 23:59:59' order by album_id) a group by a.album_id;
```
#### selectHistoryGroupByContentIdAndSource

```
select sum(a.random_times) as random_times,a.track_id,sum(time_to_sec(a.progress)) as progress,a.album_id,a.source from (select track_id,random_times,progress,album_id,source from duotin_user_listen_history_2016_12 where created_at between '2016-12-15 00:00:00' and '2016-12-15 23:59:59' order by track_id) a group by a.track_id,a.source;
```
#### selectHistoryGroupByAlbumIdAndSource
```
select sum(a.random_times) as random_times,a.album_id,sum(time_to_sec(a.progress)) as progress,a.source from (select album_id,random_times,progress,source from duotin_user_listen_history_2017_01 where created_at between '2017-01-18 00:00:00' and '2017-01-18 23:59:59' order by album_id) a group by a.album_id,a.source;
```
#### commentMapperExt.selectGroupByContentId

```
select count(a.track_id) as comment_num,a.track_id from (select track_id from duotin_comment where is_delete = 0 and created_at BETWEEN '2016-12-19 00:00:00' and '2016-12-19 23:59:59' order by null) a group by a.track_id;
```
### 专辑下节目

```
select * from duotin_content where album_id=84869 and status=1 and is_del=0 order by online_time desc;
```

### queryStartupPagesByPosition

```
select * from duotin_startup_page a,duotin_startup_page_channel b where a.id=b.startup_page_id and position=12 and a.is_del=0 and b.is_del=0 and a.app_id=1018 and region in ('全国','浙江省') 
#and started_at <= and ended_at>=
and b.channel_short_title='duotin' order by a.id desc;
```
### 敏感词
```sql
select *,
case level
when 1 then '内容可以发布，但需要审核'
when 2 then '内容中敏感词直接替换为***'
when 3 then '内容不可发布'
end as '等级说明'
 from duotin_sensitive_words where is_del=0 order bylevel desc, id desc;
```

### FM首页-分栏内容

```sql
select * from duotin_page_content where column_id=627 and `status`=0 order by display_order desc;
```

### dashboard 类目列表
#### 一级分类
```sql
select * from duotin_category where is_del=0 and is_system=0 and parent_id=0 order by display_order desc;
```

#### 二级分类
```sql
select * from duotin_category where is_del=0 and `is_show`=1 and parent_id=550 order by display_order desc;
```

#### 一级分类下专辑，queryAlumCategoryByTitleOrId
```sql
SELECT  a.id,a.title,a.image_url,a.is_excellent,c.updated_at,c.admin_id from duotin_album a
        LEFT JOIN duotin_category_album c ON c.album_id=a.id where 1=1  and a.is_del=0 and status=1 and c.is_del=0 and c.category_id=550 
order by a.id desc;
```

#### 二级分类下专辑，queryAlbumCategorySub
```java
 SELECT  a.id,a.title,a.image_url,c.updated_at,c.admin_id from duotin_album a JOIN duotin_category_album c ON c.album_id=a.id and c.sub_category_id=663 and a.is_del=0  and c.is_del=0 order by c.updated_at desc;
```

#### 新广告系统查询广告

```
select b.* from duotin_ad_channel_region a, duotin_advertiser b where a.ad_id=b.id and status=1 and is_del=0 
and a.position_map_id = 58 and a.channel_id= 18 and started_at <= '2017-03-23 11:30:19' and ended_at >= '2017-03-23 11:30:19' and a.region_id in ( 383,31,1 ) ORDER BY b.id, a.region_id desc;
```
 

