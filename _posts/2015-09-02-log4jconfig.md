---
layout: post
title: log4j configuration
tags: log4j
categories: log4j
published: true
---

<div class="toc"></div>

#log4j配置举例

```ini
# log level
log4j.rootLogger = trace, stdout, logFileSize, errorlogFileSize

# stdout
log4j.appender.stdout = org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target = System.out
log4j.appender.stdout.layout = org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern =  %d{ABSOLUTE} %5p %c:%L - %m%n


# logFileSize
log4j.appender.logFileSize = org.apache.log4j.RollingFileAppender
log4j.appender.logFileSize.File = ${LOG.DIR}/${LOG.NAME}.log
log4j.appender.logFileSize.Append = true
log4j.appender.logFileSize.maxFileSize = 500MB
log4j.appender.logFileSize.maxBackupIndex = 100
log4j.appender.logFileSize.Threshold = DEBUG
log4j.appender.logFileSize.layout = org.apache.log4j.PatternLayout
log4j.appender.logFileSize.layout.ConversionPattern = %d [%t] [%-5p] -> %m (%c)%n

# errorlogFileSize
log4j.appender.errorlogFileSize = org.apache.log4j.RollingFileAppender
log4j.appender.errorlogFileSize.File = ${LOG.DIR}/${LOG.NAME}.error.log
log4j.appender.errorlogFileSize.Append = true
log4j.appender.errorlogFileSize.maxFileSize = 500MB
log4j.appender.errorlogFileSize.maxBackupIndex = 100
log4j.appender.errorlogFileSize.Threshold = ERROR
log4j.appender.errorlogFileSize.layout = org.apache.log4j.PatternLayout
log4j.appender.errorlogFileSize.layout.ConversionPattern = %d [%t] [%-5p] -> %m (%c)%n

```
