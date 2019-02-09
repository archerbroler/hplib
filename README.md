```
The net subsystem of Linux has a performance drawback for nowadays SMP CPU.
High performance net application often requeire core affinaty, so CPU and memory area used by the same thread should be on the same numa node.
On Linux kernel, it is not possible to make kernel receive a packet one a CPU and use the same numa node of the memory channel. Another big problem is if you bind core for your appliacation, you gain no mare performance than not binding. This is almost because even you can limit your application to a specific core, you cannot limit the kernel to receive this packet on the same core, not mentioning the same numa node of the memory.
I used to use DPDK for high performance network applactions. Writing DPDK program is not a easy work, but more easy for high performance programming in pure Linux kernel. DPDK bypass the kernel because its numa isolation strategy. DPDK get the high performance network attribution because of the ability for limiting receiving core and the processing core to a same core, so called run to complete mode. On the other hand, DPDK apps allocate memory on every core, which is only used by the same cpu. allocating memory pool for a CPU requires the same numa of the memory and CPU. This is easy on DPDK.
Linux kernel should also provide this ability. FOr example, Nginx worker can be bind to a specific CPU, At least, a estblished socket can be limited to the same CPU for receiving packets and sending them.
This is a reasonable demand.
```
