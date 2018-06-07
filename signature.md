## 签名认证

1. 在请求的url带上认证信息的query
2. api_secret 申请API之后后台生成，请妥善保管，不要泄露。
3. 认证信息包括三个部分：`accesskey`,`timestamp`,`signature`
  - accesskey:用户的accesskey
  - timestamp:10位的时间戳
  - signature:使用accesskey,api_secret和timestamp生成的字符串，然后进行`sha1`签名，最后使用`base64`进行编码

### python例子
```python
accesskey='accesskey'
api_secret='api_secret'
timestamp = int(time.time())
signature = base64.b64encode(sha1(email + api_secret + str(timestamp)).hexdigest())

query = {
    'accesskey': accesskey,
    'timestamp': timestamp,
    'signature': signature
}
request_url = 'https://gizmohub.com/api/v2/contents?{0}'
response = requests.get(request_url.format(urlencode(query))
```

### 注意事项
- `timestamp`与服务器时间相差90秒以内
- 服务器时间以北京时间一致