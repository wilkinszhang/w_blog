广告分场景数据分析-2024年12月18日（deepseek-广告数据埋点与数仓关系分析）

# **数据分析报告**
## **一、背景及目标**
### 1.1 项目背景介绍
    * 在地图上投放的广告营销已经有一定的规模，25年规划重点建设智能化广告投的技术基建，在进行技术基建建设前，需要对数据进行整体的分析，确立优化的目标和路径

### 1.2 分析目标
    * 确定投放广告各个场景的点展情况（点击量 + 展现量）和转化情况
    * 确定广告在各个场景上分时间段投放情况（计划曝光量，实际曝光量）
    * 分行业看各个位置消耗情况

### 1.3 预期成果
    * 希望通过本次分析确定后续优化的方向。

## **二、数据来源及样本**
## 2.1 数据来源概述
数据周期：2024年11月15日~2024年11月30日

|数据表名称|用途说明|备注|
|-|-|-|
|lbsmap_cjh_bgc_user_action_hi|用户商业行为相关埋点存储表|这里获取了一份，可以直接用afs://aries.afs.baidu.com:9902/user/map-living-base/online_data/ad_model/behavior_data/all_maidian/分场景的埋点信息参考下面 2.2 埋点说明|
|lbsmap_cjh_bgc_poi_info|地图商户poi数据|poi_uid |
|lbsmap_cjh_bgc_ad_event_log_hi|地图推广中台广告计费日志|计费sql 含义解释 参考链接 select
  sum(billing_price)
from
  default.lbsmap_cjh_bgc_ad_event_log_hi
where
  event_name = '$act_name'
  and billing_status = 2
  and data_src in (1, 2, 11)
  and event_type in (1, 2);|
|sql表-计划投流表|投流数据表|存储路径：afs://aries.afs.baidu.com:9902/user/map-living-base/jianghanmin/ad_model/analysis/test/plan_time_20241205.txt列名：bid	start_time	end_time	    is_close|



## 2.2 数据埋点说明
[大表数据分布](https://ku.baidu-int.com/knowledge/HFVrC7hq1Q/A6A5OXVVEn/T5CAgR9wv0/56c0d659601d46?t=mention&mt=doc&dt=sheet)

|页面|位置|曝光埋点|点击埋点|参数说明|竞价参数解析|
|-|-|-|-|-|-|
|检索sug|sug列表|MCEDmm.PoiSearchPG.liuliangbaosug.show|MCEDmm.PoiSearchPG.liuliangbaosug.click|计费类型：pay_type1=CPM2=CPCdata_src：商搜来源1=行业商户通2=-基础商户通11-酒店带客宝unit_price: 计费金额（单位分）|商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
|列表页【一般是1358，酒店是147，美食休娱是358】|品专|CEMim.PoiDPG.tuiguangtongbrand.show|CEMim.PoiDPG.tuiguangtongbrand.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||商搜1位|PoiDPG.tuiguangtong1.show|PoiDPG.tuiguangtong1.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||商搜2位|PoiDPG.tuiguangtong2.show|PoiDPG.tuiguangtong2.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||商搜3位|PoiDPG.tuiguangtong3.show|PoiDPG.tuiguangtong3.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||商搜4位|PoiDPG.tuiguangtong4.show|PoiDPG.tuiguangtong4.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||商搜5位|PoiDPG.tuiguangtong5.show|PoiDPG.tuiguangtong5.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||商搜6位|PoiDPG.tuiguangtong6.show|PoiDPG.tuiguangtong6.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||商搜7位|PoiDPG.tuiguangtong7.show|PoiDPG.tuiguangtong7.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||商搜8位|PoiDPG.tuiguangtong8.show|PoiDPG.tuiguangtong8.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||商搜9位|PoiDPG.tuiguangtong9.show|PoiDPG.tuiguangtong9.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||商搜10位|PoiDPG.tuiguangtong10.show|PoiDPG.tuiguangtong10.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
|详情页|大家还在看卡片|PoiDPG.MCEDmm.DjhzkDetailPG.tuiguangtong.show|PoiDPG.MCEDmm.DjhzkDetailPG.tuiguangtong.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price注意：商业点位uid = url_params["log_param"].ad_uid|
|周边feed|周边feed推广（每8出1）|CEMim.NearbySearchSurroundComH5.tuiguangtong.show|CEMim.NearbySearchSurroundComH5.tuiguangtong.click||商搜来源：url_params["data_src"]计费类型：url_params["feed_param"].pay_type计费金额（单位分）：url_params["feed_param"].unit_price|
|驾车导航结束页|导航结束页banner|CEMim.FMCarNavPG.tuiguangtong.show|CEMim.FMCarNavPG.tuiguangtong.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||导航结束页双poi点位1位|CEMim.FMCarNavPG.destinationtuiguang1.show|CEMim.FMCarNavPG.destinationtuiguang1.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||导航结束页双poi点位2位|CEMim.FMCarNavPG.destinationtuiguang2.show|CEMim.FMCarNavPG.destinationtuiguang2.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
|步骑行导航结束页|导航结束页banner|CEMim.WalkNaviEndPG.tuiguangtong.show|CEMim.WalkNaviEndPG.tuiguangtong.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||导航结束页双poi点位1位|MCEDsg.zhongdiantuiguang1.PGshow|MCEDsg.zhongdiantuiguang1.content.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
||导航结束页双poi点位2位|MCEDsg.zhongdiantuiguang2.PGshow|MCEDsg.zhongdiantuiguang2.content.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
|手百阿拉丁B页|B页检索列表|MCEDmm.MAPPnc.B.display.Blist.tuiguangtong.show|MCEDmm.MAPPnc.B.display.Blist.tuiguangtong.click||商搜来源：url_params["data_src"]计费类型：缺失，待补充计费金额（单位分）：缺失，待补充|
|端外投放-商户聚合页|商户聚合页列表|MCEDmm.liuliangbaoshanghujuheye.shanghupoi.show|MCEDmm.liuliangbaoshanghujuheye.shanghupoi.click||商搜来源：url_params["data_src"]计费类型：url_params["log_param"].pay_type计费金额（单位分）：url_params["log_param"].unit_price|
|端外投放-DPA|poi详情页|PoiDPG.MCEDmm.liuliangbaodpajifei.show|/|||



**转化埋点**[@姜汉民](https://ku.baidu-int.com?t=mention&mt=contact&id=fa3d0e80-bd30-11ef-8dac-b317f3719039)

|转化埋点|解释|过滤条件|备注|
|-|-|-|-|
|PoiDPG.click|地图icon点击|innerPos=map||
|PoiDPG.click|电话icon点击（固定）|innerPos=phone||
|BMapPOI.merchant.phone.click |电话icon点击（悬浮）|||
|PoiDPG.naviClick|导航点击|||
|PoiDPG.goThere|到这去点击|||
|PoiDPG.newButton.click|打车点击 |||
|MCEDcateLeisure.merchantpromotion.contact.click|商品热卖点击|||
|PoiDPG.newFavorite|收藏|||
|PoiDPG.MCEDpoidp.businessCard.copy.click|详情页-商家名片--账号复制按钮点击|||
|PoiDPG.naHidden|详情页上滑|||
|||||
|BMapPOI.card.meglocalmedcaselist.megLocal.phoneClick|行业商户通-案例卡-电话|||
|BMapPOI.card.meglocalmedfloatphone.megLocal.phoneClick|行业商户通-右下角悬浮电话|||
|BMapPOI.card.meglocalmedgoodscard.megLocal.phoneClick|行业商户通-商品-电话|||
|BMapPOI.card.meglocalstaff.megLocal.phoneClick|行业商户通-人员-立即咨询|||
|BMapPOI.card.megLocalToolkitsPhone.megLocal.phoneClick|行业商户通-头卡电话|||
|BMapPOI.card.noticecard.megLocal.consult.click|行业商户通-tips引导卡-立即咨询按钮 |||
|BMapPOI.card.noticecard.megLocal.phoneClick|行业商户通-tips引导卡-电话按钮 |||
|||||



各垂类曝光点击埋点

|垂类|检索|曝光|点击|
|-|-|-|-|
|丽人||PoiListPG.itemShow|PoiListPG.poilistCell|
|交通设施||PoiListPG.itemShow|PoiListPG.poilistCell|
|休闲娱乐|MCEDse.PoiListNew.PGshow每1页打一条|MCEDse.PoiModulesExposure.show|同时出MCEDse.PoiListNew.Poi.clickPoiListPG.poilistCell|
|公司企业||PoiListPG.itemShow|PoiListPG.poilistCell|
|教育培训||PoiListPG.itemShow|PoiListPG.poilistCell|
|汽车服务||MCEDse.PoiModulesExposure.show|同时出MCEDse.PoiListNew.Poi.clickPoiListPG.poilistCell|
|生活服务||PoiListPG.itemShow|PoiListPG.poilistCell|
|美食||MCEDse.PoiModulesExposure.show|同时出MCEDse.PoiListNew.Poi.clickPoiListPG.poilistCell|
|购物||MCEDse.PoiModulesExposure.show|同时出MCEDse.PoiListNew.Poi.clickPoiListPG.poilistCell|
|运动健身||PoiListPG.itemShow|PoiListPG.poilistCell|



## 2.3 统计要求与分工
    * 说明数据清洗、缺失值处理、异常值检测等预处理步骤，确保数据质量。

|位置|统计要求|owner|备注|
|-|-|-|-|
|检索相关（sug列表，品专、商搜 1-10位）|分位置的 点击、展现 转化率等分时间段的点击、展现 转化率-（确定个时间段内的消耗情况）分位置的流量统计 （某query可能召回的，但未必展现）【通过log日志】|@陈涛|3 遗留一个todo：配置minos任务  group.mapsc-LivingAdSearchAs.MAP-SC.all，日志地址：/home/work/log/service/service.log【完成：上传地址：afs://aries.afs.baidu.com:9902/app/dt/minos/100030927/70088075/  】2024年12月17日开始|
|推荐相关（详情页，周边feed，驾车导航结束页，步骑行导航结束页）|分位置的 点击、展现 点击率等分时间段的点展-（确定各时间段内的消耗情况）分位置的流量统计 （某query可能召回的，但未必展现）|@姜汉民|#导航结束页单日限制by小时-非赠包
{"0":0.02,"1":0.04,"2":0.06,"3":0.08,"4":0.1,"5":0.12,"6":0.15,"7":0.20,"8":0.30,"9":0.38,"10":0.46,"11":0.54,"12":0.62,"13":0.70,"14":0.78,"15":0.86,"16":0.94,"17":1,"18":1,"19":1,"20":1,"21":1,"22":1,"23":1}
# 导航结束页单日限制by小时-赠包
{"0":0.02,"1":0.05,"2":0.07,"3":0.09,"4":0.11,"5":0.13,"6":0.15,"7":0.17,"8":0.19,"9":0.25,"10":0.33,"11":0.40,"12":0.47,"13":0.55,"14":0.62,"15":0.69,"16":0.76,"17":0.85,"18":0.92,"19":0.97,"20":0.98,"21":0.98,"22":0.98,"23":1}
lbsmap_cjh_bgc_ad_event_log_hi表里面有个 extInfo["order_pay_price"] = 0 代表赠包
|

# **三、数据分析和结论**
## 3.1 搜索场景数据
[分tag分位置点击转化](https://ku.baidu-int.com/knowledge/HFVrC7hq1Q/A6A5OXVVEn/T5CAgR9wv0/0b99ab78374e49?t=mention&mt=doc&dt=sheet)

竞价情况：待旭哥上线

[流量差异-垂类-小时](https://ku.baidu-int.com/knowledge/HFVrC7hq1Q/A6A5OXVVEn/T5CAgR9wv0/185446c810554f?t=mention&mt=doc&dt=sheet)

[流量差异-10min](https://ku.baidu-int.com/knowledge/HFVrC7hq1Q/A6A5OXVVEn/T5CAgR9wv0/91676760a7974a?t=mention&mt=doc&dt=sheet)



## 3.2 推荐场景数据
### 3.2.1 分位置的 点击、展现、点击率
![](https://rte.weiyun.baidu.com/wiki/attach/image/api/imageDownloadAddress?attachId=a1d579d780d44d2f80828021d5ca14cc&docGuid=jJXETo6PD3O2so "")


![](https://rte.weiyun.baidu.com/wiki/attach/image/api/imageDownloadAddress?attachId=68d4ecc61bdc4afa89135883274493ca&docGuid=jJXETo6PD3O2so "")


![](https://rte.weiyun.baidu.com/wiki/attach/image/api/imageDownloadAddress?attachId=716837aaadc84deba03c0ed08945350d&docGuid=jJXETo6PD3O2so "")


![](https://rte.weiyun.baidu.com/wiki/attach/image/api/imageDownloadAddress?attachId=9927308e7bbe47c7b4ee453fcfc9a870&docGuid=jJXETo6PD3O2so "")
取std_tag一级分类的点击、展现、点击率 。区分行业商户通和基础商户通

![](https://rte.weiyun.baidu.com/wiki/attach/image/api/imageDownloadAddress?attachId=084ea33a1e874279908c5be7138275fe&docGuid=jJXETo6PD3O2so "")
![](https://rte.weiyun.baidu.com/wiki/attach/image/api/imageDownloadAddress?attachId=5f24c8aef118469b979aba126381b83f&docGuid=jJXETo6PD3O2so "")


### 3.2.2 分时间段的展现流量
![](https://rte.weiyun.baidu.com/wiki/attach/image/api/imageDownloadAddress?attachId=b30ac773ad9b45c9a7d4accbaa065303&docGuid=jJXETo6PD3O2so "")


![](https://rte.weiyun.baidu.com/wiki/attach/image/api/imageDownloadAddress?attachId=db13bbda586d4bc4a636182dd6fd1c6c&docGuid=jJXETo6PD3O2so "")
![](https://rte.weiyun.baidu.com/wiki/attach/image/api/imageDownloadAddress?attachId=445ac239f17c47db88cf6872d3ac6ad2&docGuid=jJXETo6PD3O2so "")


![](https://rte.weiyun.baidu.com/wiki/attach/image/api/imageDownloadAddress?attachId=4baf0d1226ed488c9244911431932e67&docGuid=jJXETo6PD3O2so "")


### 3.2.3 分时段消耗数据（产出中）




# **四、整体结论与建议**
## 4.1 主要结论
    * 总结分析的主要发现，回答分析目标提出的问题。

## 4.2 策略建议
    * 根据分析结果提出具体的业务策略或改进措施，如优化产品设计、调整营销策略、加强用户服务等。

## 4.3 后续行动计划
    * 规划实施建议的步骤、时间表和资源需求，以及监控和评估计划执行效果的机制。

## 4.4 风险与挑战
    * 分析实施建议可能面临的风险和挑战，提出应对策略。
