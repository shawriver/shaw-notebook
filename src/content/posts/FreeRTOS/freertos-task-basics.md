---
title: FreeRTOS 任务基础
published: 2026-09-07
description: 任务的创建、优先级和不能返回这件事
tags: ["FreeRTOS", "嵌入式"]
category: FreeRTOS
book: FreeRTOS
order: 1
draft: false
---

## 任务是什么

FreeRTOS 里的任务就是一个死循环函数，调度器让它们轮流占用 CPU。

## 创建一个任务

```c
xTaskCreate(vTaskCode, "NAME", STACK_DEPTH, NULL, tskIDLE_PRIORITY + 1, NULL);
```

参数依次是函数、名字、栈深度、传入参数、优先级、任务句柄。

## 注意

任务函数不能返回。要结束就调用 `vTaskDelete(NULL)`。
