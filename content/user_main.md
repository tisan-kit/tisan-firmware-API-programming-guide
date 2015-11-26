# 用户应用函数  
用户应用函数包含了入口函数、产品配置，以及上网配置。 

## 入口函数  
基于ESP8266的入口函数位于 /app/user/user_main.c。  
函数说明  
***
`void user_init(void)` 
> 用户程序入口函数。  

**描述**  
> 程序启动后将在这里进行初始化用户函数。  
>下面是一个用户程序入口函数的典型例子：  

```c    
void user_init(void)
{
	uart_init(115200, 115200); // serial bound rate:11520.

	//long press gpio4, enter into wifi config mode.
	peri_config_key_init(4);
	base_keys_init();               //base keys init at the last of every single key init.

	// add you object init here.
	led_object_init();

	pando_framework_init();
}
```  

## 产品配置  
产品配置主要是配置产品 key，产品 key 是为平台进行服务注册的 key。位于 /app/user/device_config.h 。  
产品key是一个宏定义，更新相应的产品 key 即可。 
`#define PANDO_PRODUCT_KEY "(key update here)"`  

## 上网配置  
基于ESP8266的上网配置为wifi配置，有两个文件： /app/user/wifi_config.c 以及 /app/user/wifi_config.h 两个文件。  
**函数说明**  
***  
`void wifi_config(wifi_config_callback config_cb)`  
> 配置wifi的SSID和密码。  

**参数**  

| in/out  | 参数      | 说明                       |  
| --- |:--------:|:-------------------------:|  
| in  | callback | 在执行上网配置后进行回调的函数 |   


**描述**  
调用该函数将进行smartconfig配置，支持AIRKISS。  


`void auto_check_connect_init(void)`  
> 开机自自动联网配置初始化。

**描述**  
该函数先延时一段时间（时间可调），再调用wifi_auto_connect_check进行wifi自动配置。在该函数里可以设定设备重启后进入自动配置的时间。 

`void ICACHE_FLASH_ATTR wifi_auto_connect_check(void)`  
> wifi连接检测和配置。  

**描述**  
先检测是否已经连上网络， 尝试几次（次数可以自定义，默认是5次）后仍旧连接不上就进入wifi配置模式，调用wifi_config函数。  






