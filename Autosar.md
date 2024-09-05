# Autosar 

automotive open system architecture汽车开放式系统架构

Classic Platform（CP）和Adaptive Platform（AP）

CP一般用在MCU上，而AP一般用在MPU上。[【AutoSAR】 CP 和 AP_autosar ap和cp-CSDN博客](https://blog.csdn.net/qq_38089448/article/details/125844793)

## 架构

![image-20240811164851350](https://s2.loli.net/2024/08/11/WUikyXe6hpCsurz.png)

## Autosar分层软件架构

![image-20240905095230732](https://s2.loli.net/2024/09/05/V7qMBA5cawlEoHO.png)

APP(application layer)

RTE(runtime environment)

BSW(basic software)   分为services layer、ecu abstraction layer、microcontroller abstraction layer、complex driver

[【小猫爪】AUTOSAR学习笔记01-AUTOSAR架构简介-CSDN博客](https://blog.csdn.net/Oushuwen/article/details/128818564?spm=1001.2014.3001.5501)

## 概念

## RTE

## SWC软件组件

软件组件是封装了部分或者全部汽车电子功能的模块，包括了其具体的功能实现以及与对应的描述。各个软件组件通过虚拟功能总线进行交互，从而形成一个AUTOSAR应用软件。

AUTOSAR软件组件大体上可分为原子软件组件 (Atomic SWC)和部件 (Composition SWC)。部件可以包含若干原子软件组件或部件。原子软件组件则可根据不同用途分为以下几种类型：

应用软件组件 (Application SWC)
主要用于实现应用层控制算法

传感器/执行器软件组件 (Sensor/Actuator SWC) 
用于处理具体传感器/执行器的信号，可以直接与ECU抽象层交互

标定参数软件组件 (Parameter SWC) 
主要提供标定参数值

ECU抽象软件组件 (ECU Abstraction SWC) 
提供访问ECU具体I/O的能力

复杂设备驱动软件组件 (Complex Device Driver SWC) 
可定义端口与其他软件组件通信，还可以与ECU硬件直接交互

服务软件组件 (Service SWC) 
主要用于基础软件层，可通过标准接口或标准AUTOSAR接口与其他类型的软件组件进行交互

## port

软件组件通过端口（Port）来进行不同软件组件间或者软件组件与硬件间的通讯或者交互。每个软件组件都需要定义端口，根据输入/输出方向可分为：

需型端口：用于从其他软件组件获得所需数据或者所请求的操作 require port

供型端口：用于对外提供某种数据或者某类操作 provide port

供需端口：兼有需型端口与供型端口的特性 provide and require port

## interface

每个端口虽然定义了软件组件间通信内容及其方向，但是通信内容以及用于交互的操作却仍不得而知。AUTOSAR中使用端口接口（Port-Interface）来描述端口之间的供需关系。端口接口主要有以下几种类型：

**发送者-接收者接口 (Sender-Receiver Interface，S/R)**  **//implicit(获取的周期值，会有延迟) Explicit(获取的最新)**

**客户端-服务器接口 (Client-Server Interface，C/S)**

模式转换接口 (Mode Switch Interface ) 

非易失性数据接口 (Non-volatile Data Interface)

参数接口 (Parameter Interface) 

触发接口 (Trigger Interface)

其中，发送者-接收者接口 (Sender-Receiver Interface，S/R)和客户端-服务器接口 (Client-Server Interface，C/S)最为常用。

发送者-接收者接口

发送者-接收者接口用于数据的传递关系，发送者发送数据到一个或多个接收者。需要指出的是，一个软件组件的多个需型端口、供型端口、供需端口可以引用同一个发送者-接收者接口，并且它们可以使用该接口中所定义的任意一个或者多个数据元素，而并不一定使用所有数据元素。

客户端-服务器接口

客户端-服务器接口用于操作 (Operation，OP)，即函数调用关系，服务器是操作的提供者，多个客户端可以调用同一个操作，但同一个客户端不能调用多个操作。

每个端口只能定义其中一种接口类型，具有相同端口接口类型或者兼容接口类型的端口才可以进行通讯。

![image-20240904205829287](https://s2.loli.net/2024/09/04/GvODxwRMuB1oQdV.png)