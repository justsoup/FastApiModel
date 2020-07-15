
#在VScode中配置virtualenv+fastapi

创建文件FastApiModel
ctrl+\`打开终端（+shift新终端）


python -m venv env
env\Scripts\activate

如果需要安装的依赖比较多
可以执行命令pip install -r requirements.txt

pip install fastapi
pip install uvicorn

ctrl+shift+p 找到Python Select  Interpreter（命令面板）

选第一个Enter xxx=> Find => 选择env>script>python3

这时就生成了settings.json文件

ctrl+shift+d => create a launch.json file.=>Python=>Flask Launch and debug a Flask web application（运行)
替换成


    {
        "name": "Python: FastAPI",
        "type": "python",
        "request": "launch",
        "module": "uvicorn",
        "env": {
            "db_username": "postgres",
            "db_password": "secret",
            "host_server": "localhost",
            "database_name": "fastapi",
            "ssl_mode": "prefer",
            "db_server_port": "5432"
        },
        "args": [
            "main:app",
            "--reload",
            "--port",
            "8000"
        ]
    }
    
    

之后在FastApiModel文件下创建main.py文件，复制

	from typing import Optional
	from fastapi import FastAPI
	
	app = FastAPI()


	@app.get("/")
	def read_root():
	    return {"Hello": "World"}


	@app.get("/items/{item_id}")
	def read_item(item_id: int, q: Optional[str] = None):
	    return {"item_id": item_id, "q": q}


按F5，成功执行，浏览器打开 127.0.0.1查看
