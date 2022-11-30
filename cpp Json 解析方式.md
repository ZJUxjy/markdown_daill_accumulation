暂时找到三种：*jsoncpp*、*QJson*、*json for modern c++*

# jsoncpp

### 安装
```
git clone https://github.com/open-source-parsers/jsoncpp
cd jsoncpp
mkdir build && cd build
cmake ..
make
```
把生成的bin、include、lib目录拷贝到工程引用的位置。

### 使用

##### Json::Value
分array（json数组）、null、int、real（double）、string、bool、object（json对象）
对象类型通过`value.type()`获取或者`bool isBool()`这类方法获得。

##### Json::Reader
读取类
```cpp
void read(std::string _JsinFile) {
	std::ifstream ifsJson(_JsinFile, std::ios::binary);
	Json::Reader reader;
	Json::Value root;
	if (!reader.parse(ifsJson, root))
		return;
	Json::Value::Members members = root.getMemberNames();
	for (Json::Value::Members::iterator it = members.begin(); it != members.end(); it++) {
		std::string key = it->c_str();
		for (auto member : *it) {
			/*遍历取值*/
		}
	}
}
```

##### Json::FastWriter
快速写入类
```cpp
std::string FastConstructJson() {
	Json::Value root = Json::objectValue;
	root["name"] = "xjy";
	root["age"] = 23;
	root["job"] = Json::objectValue;
	root["job"]["occupation"] = "wangguan";
	return Json::FastWriter().write(root);
}//将这个Json对象返回为一个字符串
```





# JSON for Modern C++

[Releases · nlohmann/json (github.com)](https://github.com/nlohmann/json/releases)
环境安装：上面的git仓库拉取源代码，然后把`json-develop\include\`下`nlohmann`这个文件夹拷贝到项目引用目录，无需引用第三方库。
使用的时候：
```cpp
#include "json.hpp"
//或
#include "nlohmann/json.hpp"
```
使用上比jsoncpp、Qt自带的json解析器都直观方便，使用样例：
```cpp
using json = nlohmann::json;
void jsonfunc(){
	json j;
	j["name"]="jingyao";
	j["age"]=23;
	j["array"]={1,2,3};
	j["obj"]={{"city","hangzhou"},{"have_a_job",true}};
	//另一种写法
	json js={
		{"name","xjy"},
		{"age",23},
		{"array",{1,2,3}},
		{"obj",{
			{"city","hangzhou"},
			{"have_a_job",true}
		}}
	};
	
}
```

读取、写入可以依赖文件流的方式进行：
```cpp
	json j;
	std::ifstream ifs("test.json");
	ifs >> j;

	std::ofstream ofs("output.json");
	ofs << std::setw(4)<<j<<std::endl;
```

---

# QJson

类名  |  功能
------ | -----
QJsonDocument | 读、写json文件
QJsonQbject | 与Json对象相对应，封装Jsond对象
QJsonValue | 封装Json值
QJsonArray | 封装Json数组

使用例子：
读
```cpp
void read(std::string _jsonFile)
{
	QFile file(QString::fromStdString(_jsonFile));
	set_m_JsonFile(file.fileName());
	file.open(QFile::ReadOnly);
	if (!file.isOpen()) return;
	QByteArray _all;
	_all = file.readAll();
	file.close();
    QJsonParseError jsonError;
    QJsonDocument document = QJsonDocument::fromJson(_all, &jsonError);
    if ((QJsonParseError::NoError == jsonError.error) &&(!document.isNull()))
    {
        if (document.isObject())
        {
            QJsonObject obj = document.object();
            QStringList keys = obj.keys();
            for (auto t:obj) {
            {
            /*正常情况下要判断类型然后进行赋值，这里就不展开了*/
	            static int i = 0;
	            qDebug() << t.type() << keys.at(i) << " " << obj.value(keys.at(i++));
            }
        }
        else {}
    }else{}
}
```
写
```cpp
void write(std::string _JSonFile){
	QJsonObject obj;
	obj.insert("name",QString("xjy"));
	obj.insert("sex",QString("man"));
	obj.insert("age",23);
	QJsonObject subobj;
	subobj.insert("occupation",QString("programmer"));
	obj.insert(subobj);
	QFile file(QString::fromStdString(_jsonFile));
	file.open(QFile::WriteOnly);
	if(!file.isOpen()) return;
	file.write(json);
	file.close();
}
```


