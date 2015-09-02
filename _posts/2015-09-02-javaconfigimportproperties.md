---
layout: post
title: Spring Import Properties Config file
tags: ValueAnnotation JavaConfig
categories: javaconfig
published: true
---

<div class="toc"></div>

#描述
Spring JavaConfig配置，关于导入properties配置文件的使用方法。以下方式都是通过
@PropertySource导入properties配置文件

#1.@Value注解方式之"$"
jdbc.properties
~~~java
jdbc.username=test
jdbc.password=password
jdbc.url=com.org.apache.test
~~~

AppConfig.java
~~~java
@Configuration
@PropertySource(value = "classpath:jdbc.properties")
public class AppConfig {
  @Value("${jdbc.username}")
  private String username ;

  //此bean一定要实现，否则${}引用不起作用
  @Bean
  public static PropertySourcesPlaceholderConfigurer propertyConfigInDev() {
    return new PropertySourcesPlaceholderConfigurer();
  }
}
~~~


#2.@Value注解方式之"#"
jdbc.properties
~~~java
jdbc.username=test
jdbc.password=password
url=com.org.apache.test
~~~

AppConfig.java
~~~java
@Value("#{config.url}")//url 一定不能是jdbc.url=***，应该是url=***
private String url ;

@Bean
public PropertiesFactoryBean config(){
    PropertiesFactoryBean p = new PropertiesFactoryBean() ;

    p.setLocation(new ClassPathResource("JDBC.properties"));
    return p ;
}
~~~
#2.Environment注入方式
jdbc.properties
~~~java
jdbc.username=test
jdbc.password=password
url=com.org.apache.test
~~~
AppConfig.java
~~~java
@Resource
private Environment env ;

@Bean
public String password(){
    return env.getProperty("jdbc.password") ;
}
~~~
