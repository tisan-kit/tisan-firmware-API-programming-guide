# 3 pando框架函数  
这里主要介绍pando框架的内容，包括了通用接口、网关模块，以及协议模块，由于应用开发者理解通用接口即可，网关模块和协议模块不在这里介绍。  

## 3.1 框架通用接口  
pando 框架通用接口包含几个文件，包含了如下内容：  
- pando 框架初始化函数；  
- pando 框架 object 通用操作，有两大类别：   
	- object 管理函数类别  
	- object迭代器管理函数类别
- pando 子设备数据处理函数  

### 3.1.1 pando 框架初始化函数   
位于/app/pando/pando_framework.c文件。  
函数说明  
***
`void ICACHE_FLASH_ATTR pando_framework_init()`   
> pando 框架初始化函数。  

** 描述 **   
> 进行 pando 网关初始化  
分配子设备接收数据的通道   

### 3.1.2 pando 框架 object 通用操作  
pando object 是基于pando框架的object，object跟物理实体有一定的关联性，但更多是倾向于逻辑上的划分。
通用操作涉及object 管理函数类别以及迭代器管理函数类别。  
函数说明  
***
`void ICACHE_FLASH_ATTR register_pando_object(pando_object object)`  
> pando object注册函数。 

**参数**  

| in/out  | 参数      | 说明                       |    
| --- |:--------:|:-------------------------:|    
| in  | object | 新注册的object |   

**描述**  
object注册是将object添加到链表里面，object是由链表的形式进行管理。  

`pando_object* ICACHE_FLASH_ATTR find_pando_object(int8 no)`  
> 查找指定编号的object  

**参数**  

| in/out  | 参数      | 说明                       |    
| --- |:--------:|:-------------------------:|    
| in  | no | 要查找的object的编号 |  

**描述**  
查找指定编号的object，如果有指定编号的object，则返回该object指针，否则返回NULL。

`pando_objects_iterator* ICACHE_FLASH_ATTR create_pando_objects_iterator()`
> 创建pando object迭代器。  

**描述**  
创建pando object迭代器，给迭代器分配空间。  

`void ICACHE_FLASH_ATTR delete_pando_objects_iterator(pando_objects_iterator* it)`   
> 删除pando object 迭代器。  

**描述**  
删除pando object迭代器，释放空间。 

`pando_object* ICACHE_FLASH_ATTR pando_objects_iterator_next(pando_objects_iterator *it)`   
> 迭代下一个pando object。  

**参数**  

| in/out  | 参数      | 说明                       |    
| --- |:--------:|:-------------------------:|    
| in  | it | 要进行处理的pando object迭代器 |  

**描述**  
> 迭代输出下一个pando object。  

### 3.1.3 pando 子设备数据处理函数   
pando 子设备收发数据是通过网关进行的。  
函数说明  
***  
`void ICACHE_FLASH_ATTR pando_subdevice_recv(uint8_t * buffer, uint16_t length)`  
> 子设备接收到到数据，进行解析处理。  

**参数**  

| in/out  | 参数      | 说明                       |    
| --- |:--------:|:-------------------------:|    
| in  | *buffer | 从网关发来的数据 |  
| in  | length | 从网关发来的数据的长度 |  

**描述**  
> 处理网关的数据，调用数据或者命令解析进行处理，并最终传递到执行和反馈。


## 网关模块  
网关模块的接口文件位于 /app/pando/gateway/ 目录下，这里的函数开发者不用去改。
## 协议模块  
协议模块的接口文件位于 /app/pando/protocol/ 目录下，这里的函数开发者不用去改。



