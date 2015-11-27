
import sys
import urllib2
import time
from datetime import datetime, timedelta
import json
import requests


# 인천 미세먼지 
url = 'http://www.airkorea.or.kr/index'
url_local ="http://127.0.0.1:4242/api/put"

def insert(metric_name, tag_site, value):
    data={
        "metric":"dust",
        "timestamp":time.time(),
        "value":value,
        "tags":{
            "host":mypc
        }
    }
    ret = requests.post(url_local, data=json.dumps(data))
    print ret


def getData(buffers):
    a = buffers.split('<tbody id="mt_mmc2_10007">')[1]
    #print a

    b = a.split('</tbody>')[0].replace('<tr>','').replace('</tr>','').replace('</td>','')
    #print b

    c = b.split('<td>')
    # incheon
    print c[7]
    print c[8]

    # incheon
    print c[7]
    print c[8]

    insert(int(c[8]))
    

if __name__ == '__main__':
    while 1 :
        t = time.localtime()
        tsec = t.tm_sec

        if tsec%10!=0:
            print tsec
            time.sleep(1)
        else :
            page = urllib2.urlopen(url).read()
            getData(page)
