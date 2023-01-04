
# python

fastapi

`pip3 install fastapi[all]`



新建main.py

```python
from fastapi import FastAPI

import uvicorn

app = FastAPI()

@app.get("/")

async def root():

    return {"message":"Hello world, FastAPI"}



if __name__ == '__main__':

    uvicorn.run(app='main:app', host="127.0.0.1", port=5555, reload=True, workers=100)

```

运行

`uvicorn main:app --reload`