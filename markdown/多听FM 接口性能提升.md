多听FM 接口性能提升

1、对App所有接口进行测试，分10次进行，得出平均花时：300ms，在10次中记录了耗时超过500ms的接口如下：
http://api.duotin.com/category/content
http://api.duotin.com/album
http://api.duotin.com/ranking/content
http://api.duotin.com/comment/lastComments
http://api.duotin.com/homepage
http://api.duotin.com/ad/info
http://api.duotin.com/album/page
http://api.duotin.com/message/token
http://api.duotin.com/live/detail
http://api.duotin.com/radio/index
http://api.duotin.com/album/latest
http://api.duotin.com/message/notify
http://api.duotin.com/homepage/region
http://api.duotin.com/user/podcastList
2、对所有接口进行同样的测试，在测试环境，平均花时：94ms，在10次中记录了耗时超过500ms的接口如下：
http://api.danxinben.com/version
http://api.danxinben.com/message/notify
http://api.danxinben.com/homepage
http://api.danxinben.com/ad/info
http://api.danxinben.com/album

3、喜马拉雅所有接口做同样测试，平均响应：59ms，超过500ms的接口如下：
http://mobile.ximalaya.com/mobile/discovery/v3/category/recommends
http://mobile.ximalaya.com/mobile/nonce/app
http://mobile.ximalaya.com/mobile/v1/album/detail


