---
title: Fast API
slug: Fast-API
lastmod: 2025-07-01T00:00:00+00:00
---

# Fast API

# 配置项目的python环境

可以 install python 所需的所有环境，不用一个一个的 pip install

```jsx
pip freeze > piplist.txt
pip install -r piplist.txt
```

# 创建 fastapi

```python
from fastapi import FastAPI

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=['Content-Type','application/xml'],
)

@app.get("/gettest")
async def gettest():
		return {"hello world"}

@app.post("/posttest")
async def posttest(json_data: Dict):

		# 传进 JSON_DATA 注意 尾行不留空格
		# {
		#     "investdate": "2022-03-04",
		#     "weights":[
		#         {
		#             "id": "AMD",
		#             "weight": -0.344
		#         },
		#         {
		#             "id": "AMZN",
		#             "weight": 0.699
		#         },
		#         {
		#             "id": "ZM",
		#             "weight": 0.499
		#         }
		#     ]
		# }

    # 如何处理 json 数据
		investdate = json_data['investdate']
    weight = json_data['weights']

    # 如何把 json 数组转化成 dict
    input_weght = dict()
    for data in weight:
        id = data["id"]
        weight = data["weight"]
        input_weght[id] = weight
  
    # 接口里定义的函数 逻辑部分
		def inquirie_for_customer(investdate, weight: dict)：
				return return_json
		
		# 如何把结果传回去
		result = inquirie_for_customer(investdate,input_weght)
    return JSONResponse(status_code=200, content=result)
```

# 运行 fastapi

```jsx
py fastapi_server.py
```

![Untitled](Fast%20API%201118a2a5f576468f9ad750757fd02a1b/Untitled.png)

# 调试 fastapi

```jsx
http://127.0.0.1:8888/docs
```

然后就可以输入 request body

![Untitled](Fast%20API%201118a2a5f576468f9ad750757fd02a1b/Untitled%201.png)

# React 中调用 fastapi

GET

![Untitled](Fast%20API%201118a2a5f576468f9ad750757fd02a1b/Untitled%202.png)

# 传图片 base64格式

```python
@app.post("/main", response_model=ResposeModel, description="收到请求并返回图片数据(Base64格式)")
def test(request: RequestModel):
    time.sleep(1)
    return {
        "img": {
            "weight": convert2Base64("./imgs/weight.png"),
            "AMD": convert2Base64("./imgs/AMD.png"),
            "AMZN": convert2Base64("./imgs/AMZN.png"),
            "ZM": convert2Base64("./imgs/ZM.png")
        },
        "img_dl": {
            "weight": convert2Base64("./imgs/weight_dl.png"),
            "AMD": convert2Base64("./imgs/AMD_dl.png"),
            "AMZN": convert2Base64("./imgs/AMZN_dl.png"),
            "ZM": convert2Base64("./imgs/ZM_dl.png")
        }
    }
```

```python
<img src={"data:image/Jpeg;base64,".concat(imgUrl)}/
```

# 报错

**422 Unprocessable Entity**

1. 检查是不是都用的双引号
2. 行尾不能有多的逗号
3. 正确的写法如下

```jsx
{
    "investdate": "2022-03-04",
    "weights":[
        {
            "id": "AMD",
            "weight": -0.344
        },
        {
            "id": "AMZN",
            "weight": 0.699
        },
        {
            "id": "ZM",
            "weight": 0.499
        }
    ]
}
```