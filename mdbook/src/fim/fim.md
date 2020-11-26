# The Fog Infrastructure Manager (FIM)

The Eclipse fog05 Fog Infrastructure Manager (FIM) module virtualises the hardware infrastructure, such as computational, communication, storage and I/O resources. It provides key primitives for the management of the infrastructure and the application deployed in it.

It also provide a set of abstraction. The FIM is designed to be distributed, without any controller node. The system state is managed in a location-transparent manner leveraging Zenoh for data distribution and sharing across the system.

To kick off our tour of Eclipse fog05 and to demonstrate use and access of the Fog Infrastructure Manager, we will start with the obligatory “hello world” example. This example will deploy a docker container that just prints ["Hello World"!](./fim_hello_world.md).

