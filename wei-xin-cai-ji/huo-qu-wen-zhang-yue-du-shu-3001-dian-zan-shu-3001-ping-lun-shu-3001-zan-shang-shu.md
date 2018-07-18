```
from datetime import datetime
from http.cookiejar import LWPCookieJar
from random import random
from selenium import webdriver
import logging,config,json,utils,os,time,re,html,requests,pymongo
from urllib.parse import urlsplit

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)
base_url = "https://mp.weixin.qq.com"
search_url = "https://mp.weixin.qq.com/cgi-bin/searchbiz?"
appmsp_url = "https://mp.weixin.qq.com/cgi-bin/appmsg?"

opt = webdriver.ChromeOptions()
opt.set_headless()

# 登录微信公众号
def login_wechat():
    # 使用webdriver1驱动启动谷歌浏览器
    logger.info("启动浏览器，打开微信公总号登录界面")
    driver = webdriver.Chrome()
    driver.get(base_url)

    # 用于存储cookies
    post = {}
    logger.info("输入微信公总号登录账号和密码")
    # 清空账号框中的内容
    driver.find_element_by_xpath('//*[@id="header"]/div[2]/div/div/form/div[1]/div[1]/div/span/input').clear()
    # 自动填入登录账号
    driver.find_element_by_xpath('//*[@id="header"]/div[2]/div/div/form/div[1]/div[1]/div/span/input').send_keys(config.USERNAME)
    # 清除密码框中的内容
    driver.find_element_by_xpath('//*[@id="header"]/div[2]/div/div/form/div[1]/div[2]/div/span/input').clear()
    # 自动填入登录密码
    driver.find_element_by_xpath('//*[@id="header"]/div[2]/div/div/form/div[1]/div[2]/div/span/input').send_keys(config.PASSWORD)
    logger.info("请记住在登录界面点击:记住账号")
    time.sleep(1)
    logger.info("登录")
    driver.find_element_by_xpath('//*[@id="header"]/div[2]/div/div/form/div[4]/a').click()
    logger.info("需要拿手机进行扫描二维码登录公总号")
    time.sleep(5)
    # 获取cookies
    logger.info("正在获取cookies中.....")
    # cookies = driver.get_cookies()
    # with open("cookies.json",'w+',encoding='utf-8') as f:
    #     f.write(json.dumps(cookies))
    cookie_items = driver.get_cookies()
    # 获取到的cookies是列表形式，将cookies转成json形式并存入本地名为cookie的文本中
    with open("cookies.json","w+",encoding="utf-8") as f:
        f.write(json.dumps(cookie_items))
    logger.info("cookies存储完毕")

# 搜索文章
def query_message(query=None,begin=0):
    """
    :param query: 查询名称
    :param begin: 查询页数
    :param count: 每页查询数量
    :param random: 随机生成数
    :return:
    """
    # query为要爬取的公众号名称
    logger.info("开始爬取公众号名称")
    logger.info("开始搜索相关公众号:"+str(query))
    # 设置headers
    response = requests.get(base_url, headers=config.HEADERS_LOGIN)
    token = re.findall(r'token=(\d+)', str(response.url))[0]
    logger.info("获取token值:"+str(token))

    query_param = {
        'action': 'search_biz',
        'token': token,
        'lang': 'zh_CN',
        'f': 'json',
        'ajax': '1',
        'random': random(),
        'query': query,
        'begin': begin,
        'count': '5',
    }

    search_response = requests.get(search_url,headers=config.HEADERS_LOGIN,params=query_param)
    # print(search_response.json())
    # 获取搜索结果的第一个公众号
    datas = search_response.json().get("list")[0]
    fakeid = datas['fakeid']
    query_appmsg_opertor(fakeid,token,query)

# 查询文章
def query_appmsg_opertor(fakeid,token,query):
    try:
        query_appmsg_param = {
            'token': token,
            'lang': 'zh_CN',
            'f': 'json',
            'ajax': '1',
            'random':random(),
            'action': 'list_ex',
            'begin': '0', # 第几页
            'count': '5',
            'query':'',
            'fakeid': fakeid,
            'type': '9',
        }

        appmsp_response = requests.get(appmsp_url,headers=config.HEADERS_LOGIN,params=query_appmsg_param)
        # print(appmsp_response.json())
        appdatas = appmsp_response.json()
        # 获取文章总数
        app_msg_cnt = appdatas.get("app_msg_cnt")
        logger.info("该公众号有:"+str(app_msg_cnt)+"篇文章")
        index_num = int(int(app_msg_cnt) / 5)
        begin_page = 0
        page_num = 0
        while index_num+1 >0:

            query_appmsg_param = {
                'token': token,
                'lang': 'zh_CN',
                'f': 'json',
                'ajax': '1',
                'random': random(),
                'action': 'list_ex',
                'begin': begin_page,  # 第几页
                'count': '5',
                'query': '',
                'fakeid': fakeid,
                'type': '9',
            }
            logger.info("正在翻页:"+str(page_num))
            query_response = requests.get(appmsp_url, headers=config.HEADERS_LOGIN, params=query_appmsg_param)
            query_response = query_response.json()
            app_msg_list = query_response.get("app_msg_list")

            # 文章各自的信息
            for msg in app_msg_list:
                # print(msg)
                time.sleep(2)
                link = msg["link"]
                print(link)
                useful_info(link,msg,query)
            time.sleep(1)
            index_num -= 1
            page_num += 1
            begin_page = int(begin_page)
            begin_page += 5
    except:
        pass


# 爬取文章评论数和阅读数
def useful_info(link,msg,query):
    """
    :param link_num: 点赞数
    :param read_num: 阅读数
    :param comment_id: 评论id号
    :return:
    """
    try:
        logger.info("公众号文章:"+msg.get("title")+"阅读数和点赞数爬取")
        post = link

        data_url_params = config.DATA_URL_PARAMS

        # url 转义处理
        content_url = html.unescape(post)
        # 截取content_url的查询参数部分
        content_url_params = urlsplit(content_url).query
        # 将参数转化为字典类型
        content_url_params = utils.str_to_dict(content_url_params, '&', "=")
        # 更新到data_url
        data_url_params.update(content_url_params)
        body = "is_only_read=1&req_id=18129wOQUktiTW8xkUueJ3MN&pass_ticket=XY9%252BDmGx9R5lOivTLAmZUnQ6Me3AdfJfPFRld0kAp40%253D"
        data = utils.str_to_dict(body, "&", "=")

        headers = config.HEADERS_USEFUL_INFO

        headers = utils.str_to_dict(headers)

        data_url = "https://mp.weixin.qq.com/mp/getappmsgext"

        response = requests.post(data_url, data=data, params=data_url_params, headers=headers)
        response = response.json()
        # print(response)
        if response.get("appmsgstat"):
            appmsgstat = response.get("appmsgstat")
            read_num = appmsgstat.get("read_num")  # 阅读数
            like_num = appmsgstat.get("like_num")  # 点赞数
            # print("阅读数:" + str(read_num))
            logger.info("文章标题:" + msg.get("title") + ",阅读数:"+str(read_num)+",点赞数:"+str(like_num))
            msg.update(appmsgstat)
            # print(msg)
            save_to_mongodb(msg,query)
            time.sleep(2)
    except:
        pass

def save_to_mongodb(msg,query):
    try:
        msg = change_dict(msg)
        client = pymongo.MongoClient("localhost",27017)
        db = client.weixin_2
        collection = db[str(query)]
        # print(db.collection_names())
        data = collection.insert_one(msg)
        # print(data)
        logger.info("成功存储到MongoDB数据库.....")
    except:
        pass

def change_dict(msg):
    msg_change = {}
    keys = {'title':"标题", 'content_link':"文章链接", 'digest':"摘要", 'cover':"封面图", 'read_num':"阅读数", 'like_num':'点赞数'}

    for key,value in msg.items():
        if key in keys.keys():
            # print(key,value)
            msg_change.update({
                keys[key]:value
            })
    msg_change["发布时间"] = time.strftime("%Y-%m-%d %H:%M:%S",time.localtime(msg.get("update_time")) )
    msg_change["数据更新时间"] = time.strftime("%Y-%m-%d %H:%M:%S",time.localtime(datetime.now().timestamp()))

    return msg_change

if __name__ == "__main__":
    query_message(query="青春黔言",begin=0)

```

```
config.py


USERNAME = "1326925615@qq.com"
PASSWORD = "1326925615@qq.com"

HEADERS_LOGIN = {
        "HOST": "mp.weixin.qq.com",
        "User-Agent": "Mozilla/5.0 (Windows NT 6.1; WOW64; rv:53.0) Gecko/20100101 Firefox/53.0",
        "Cookie": "ua_id=awLtV6JZxEkuCcggAAAAAGlW4U-iD8C6f9P7aobbWiI=; mm_lang=zh_CN; pgv_pvi=1536361472; pgv_si=s2566961152; uuid=9ad330ed158d164feeaf0e36e88af6ef; bizuin=3534922651; ticket=4093bdd873da38b123b83f73eb44920d7338f798; ticket_id=gh_e8718df7f69a; cert=dsvleSo41cc4smkQUxX7FXtRPEoxlB6o; noticeLoginFlag=1; data_bizuin=3534922651; data_ticket=TKUyKVEP9vD23yqXbMHyKAGKcDucWtScnWXD32cVgv3r9b8gyqCPXZAGQYBuTBdN; slave_sid=N3JnRXBjd2x4QnRESzVUbGJMUnlWTnlxNTRaeEFLazFqUjRqc3FNSW9uVXkwRm84WlE2X3JaekZncW5oS2VGV044bW92Q1B6bWwxdThEaDQ1ZEZEb0VGUnpLREJ2X2d1b0htZXZtalZLMGVtcURNWTVGRm1PY1hMdm9rZGlZR2MwN3A1N2ZkaFE3NURDYjlI; slave_user=gh_e8718df7f69a; xid=ffdf3cfa703e04b3cc10161b59015dba; openid2ticket_om6Oy0ksIJ20KIix8ru4-EUv68Pg=ncHQSS+E41ZuC7FAmPDV+17OYR2VCC6ld1NOn8fq7bQ="
    }

HEADERS_USEFUL_INFO =   """
Host: mp.weixin.qq.com
Connection: keep-alive
Content-Length: 858
Origin: https://mp.weixin.qq.com
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Linux; Android 8.0; MI 6 Build/OPR1.170623.027; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/57.0.2987.132 MQQBrowser/6.2 TBS/044033 Mobile Safari/537.36 MicroMessenger/6.6.7.1321(0x26060739) NetType/WIFI Language/zh_CN
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept: */*
Referer: https://mp.weixin.qq.com/s?__biz=MzAxNzQ3NDIzOQ==&mid=2650932476&idx=1&sn=f00567fe8a6f463349cc7f36f6395001&chksm=8012532cb765da3a7245c06aa1665ff212bfd2357d04ca2aa94a455947c45005ae67b0d3334c&scene=126&ascene=0&devicetype=android-26&version=26060739&nettype=WIFI&abtest_cookie=AwABAAoACwAMAAYAPoseACOXHgC7lx4ADJgeAHmYHgAImR4AAAA%3D&lang=zh_CN&pass_ticket=XY9%2BDmGx9R5lOivTLAmZUnQ6Me3AdfJfPFRld0kAp40%3D&wx_header=1
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,en-US;q=0.8
Cookie: rewardsn=; wxtokenkey=777; wxuin=0; devicetype=android-26; version=26060739; lang=zh_CN; pass_ticket=XY9+DmGx9R5lOivTLAmZUnQ6Me3AdfJfPFRld0kAp40=; wap_sid2=COq2kioSXGVfREJQWnJKZVh6aWNzRDRkRXRESVJ1MkJKOG1vdmNLamxoT21LZXR1R0NmUmswYm9nZVh2VDdvQkw4bVJKeFFmUDNaUE9sRzVRM01GMmxwUVZRWjVzVURBQUF+MIP4utoFOA1AAQ==
Q-UA2: QV=3&PL=ADR&PR=WX&PP=com.tencent.mm&PPVN=6.6.7&TBSVC=43610&CO=BK&COVC=044033&PB=GE&VE=GA&DE=PHONE&CHID=0&LCID=9422&MO= MI6 &RL=1080*1920&OS=8.0.0&API=26
Q-GUID: 608bfe6fe0080f54b9d6f9c013b788cb
Q-Auth: 31045b957cf33acf31e40be2f3e71c5217597676a9729f1b
        """

HEADERS_USEFUL_COMMENT = """
  GET https://mp.weixin.qq.com/mp/appmsg_comment?action=getcomment&scene=0&__biz=MzAxNzQ3NDIzOQ==&appmsgid=2650932470&idx=1&comment_id=372522035265421313&offset=0&limit=100&uin=777&key=777&pass_ticket=FhBQs3QUrWK1Lb0qAVIF1anDuG2lPea9SddGWMcEGrE%25253D&wxtoken=777&devicetype=android-26&clientversion=26060739&appmsg_token=965_F7poVf5sOAlgd8ojaKW-iFtSODGl6FuGDbVytiZD3bU0F_zrfACUpZXLVio~&x5=1&f=json HTTP/1.1
Host: mp.weixin.qq.com
Connection: keep-alive
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Linux; Android 8.0; MI 6 Build/OPR1.170623.027; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/57.0.2987.132 MQQBrowser/6.2 TBS/044033 Mobile Safari/537.36 MicroMessenger/6.6.7.1321(0x26060739) NetType/WIFI Language/zh_CN
Accept: */*
Referer: https://mp.weixin.qq.com/s?__biz=MzAxNzQ3NDIzOQ==&mid=2650932470&idx=1&sn=f04d566dd85926531654d3eef6d03e4b&chksm=80125326b765da3058c6f9713c58af0a681b2960be2ec95b49edbc9dc20ffb292ea523e2e999&scene=0&ascene=7&devicetype=android-26&version=26060739&nettype=WIFI&abtest_cookie=AwABAAoACwAMAAcAPoseACOXHgC7lx4ADJgeAD6YHgB5mB4ACJkeAAAA&lang=zh_CN&pass_ticket=FhBQs3QUrWK1Lb0qAVIF1anDuG2lPea9SddGWMcEGrE%3D&wx_header=1
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,en-US;q=0.8
Cookie: rewardsn=; wxuin=0; devicetype=android-26; version=26060739; lang=zh_CN; pass_ticket=FhBQs3QUrWK1Lb0qAVIF1anDuG2lPea9SddGWMcEGrE=; wap_sid2=COq2kioSXHZpZFdIX2ZqVzB3RFBaWEpEZVh4TFB5OXFqMTZudzQ1RFdSNWJWLXVNaFdLUzJFdzlWRE9UQ05RR21nVGxPYllSQkJqMUg4bWMwQ013NTMtZGsybHA4VURBQUF+MNmjuNoFOA1AAQ==; wxtokenkey=777
Q-UA2: QV=3&PL=ADR&PR=WX&PP=com.tencent.mm&PPVN=6.6.7&TBSVC=43610&CO=BK&COVC=044033&PB=GE&VE=GA&DE=PHONE&CHID=0&LCID=9422&MO= MI6 &RL=1080*1920&OS=8.0.0&API=26
Q-GUID: 608bfe6fe0080f54b9d6f9c013b788cb
Q-Auth: 31045b957cf33acf31e40be2f3e71c5217597676a9729f1b
        """

DATA_URL_PARAMS = {
        '__biz': 'MzAxNzQ3NDIzOQ==',
        'appmsg_type': '9',
        'mid': '2650932476', # 改变
        'sn': 'f00567fe8a6f463349cc7f36f6395001', # 改变
        'idx': '1',
        'scene': '126',  # 改变
        'title': '%E6%9D%8E%E5%85%8B%E5%BC%BA%E5%B0%B1%E7%94%B5%E5%BD%B1%E3%80%8A%E6%88%91%E4%B8%8D%E6%98%AF%E8%8D%AF%E7%A5%9E%E3%80%8B%E5%BC%95%E7%83%AD%E8%AE%AE%E4%BD%9C%E6%89%B9%E7%A4%BA',
        'ct': '1531878131', # 改变
        'abtest_cookie': 'AwABAAoACwAMAAYAPoseACOXHgC7lx4ADJgeAHmYHgAImR4AAAA=',
        'devicetype': 'android-26',
        'version': '26060739',
        'f': 'json',
        'r': '0.3900514331545941',
        'is_need_ad': '1',
        'comment_id': '373894696226799617',
        'is_need_reward': '0',
        'both_ad': '0',
        'reward_uin_count': '0',
        'msg_daily_idx': '1',
        'is_original': '0',
        'uin': '777',
        'key': '777',
        'pass_ticket': 'XY9%252BDmGx9R5lOivTLAmZUnQ6Me3AdfJfPFRld0kAp40%253D',
        'wxtoken': '777',
        'clientversion': '26060739',
        'appmsg_token': '965_ZwpNJe3OIbtqUS2dube1NMT59_5fSUo4JpJuGxAjcUXGreBLIE6_erAi1B4~',
        'x5': '1',
    }
```



