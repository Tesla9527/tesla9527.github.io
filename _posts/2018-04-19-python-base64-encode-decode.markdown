---
layout:     post
title:      "python进行base64编码和解码"
subtitle:   ""
date:       2018-04-19
author:     "Tesla9527"
header-img: "img/post-bg-alitrip.jpg"
tags:
    - python
---
```python
import base64


# base64编码
a = """{"contact_mobile":"13291110987","DAS2":{"success":true,"asset_score":"47","behavior_score":"96","biz_no":"ZM201803203000000229000003500888","composite_score":"65","credit_history_score":"32","identity_score":"3","rsm_asset_score":"89","rsm_behavior_score":"12","rsm_credit_history_score":"66","rsm_identity_score":"55"},"ADDRESS":"河北省唐山市路北区学院路德力西大厦","contact_name":"测试","education_degree":"BACHELOR","contact_relation":"PARENTS","taxed_income":"BELOW_10"}"""
result = base64.b64encode(a.encode('utf-8'))
print(str(result, 'utf-8'))
```
Test Result:
![img](/img/in-post/base64/1.png)

```python
import base64


# base64解码
a = b"eyJjb250YWN0X21vYmlsZSI6IjEzMjkxMTEwOTg3IiwiREFTMiI6eyJzdWNjZXNzIjp0cnVlLCJhc3NldF9zY29yZSI6IjQ3IiwiYmVoYXZpb3Jfc2NvcmUiOiI5NiIsImJpel9ubyI6IlpNMjAxODAzMjAzMDAwMDAwMjI5MDAwMDAzNTAwODg4IiwiY29tcG9zaXRlX3Njb3JlIjoiNjUiLCJjcmVkaXRfaGlzdG9yeV9zY29yZSI6IjMyIiwiaWRlbnRpdHlfc2NvcmUiOiIzIiwicnNtX2Fzc2V0X3Njb3JlIjoiODkiLCJyc21fYmVoYXZpb3Jfc2NvcmUiOiIxMiIsInJzbV9jcmVkaXRfaGlzdG9yeV9zY29yZSI6IjY2IiwicnNtX2lkZW50aXR5X3Njb3JlIjoiNTUifSwiQUREUkVTUyI6Iuays+WMl+ecgeWUkOWxseW4gui3r+WMl+WMuuWtpumZoui3r+W+t+WKm+ilv+Wkp+WOpiIsImNvbnRhY3RfbmFtZSI6Iua1i+ivlSIsIkNyZWRpdFNjb3JlIjp7InN1Y2Nlc3MiOnRydWUsImJpel9ubyI6IlpNMjAxNzAzMjczMDAwMDAwOTIyOTAwMDAxOTE2ODA5Iiwiem1fc2NvcmUiOiI3OSJ9LCJlZHVjYXRpb25fZGVncmVlIjoiQkFDSEVMT1IiLCJjb250YWN0X3JlbGF0aW9uIjoiUEFSRU5UUyIsInRheGVkX2luY29tZSI6IkJFTE9XXzEwIn0="

result = base64.decodebytes(a)
print(result.decode("utf-8"))
```
Test Result:
![img](/img/in-post/base64/2.png)