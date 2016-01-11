---
layout: post
title: "container of" from mt6605.c
category: Technology
comment: true
---

#container of from mt6605.c
***
##void mt6605_dev_irq_handler(void)
```C
369void mt6605_dev_irq_handler(void)
370{
371    struct mt6605_dev *mt6605_dev = mt6605_dev_ptr;
372	pr_debug("%s : &mt6605_dev=%p\n", __func__, mt6605_dev);
373
374	if (NULL == mt6605_dev) {
375		pr_debug("mt6605_dev NULL\n");
376		return;
377	}
378	mt6605_disable_irq(mt6605_dev);
379	wake_up(&mt6605_dev->read_wq);
380	/* wake_up_interruptible(&mt6605_dev->read_wq); */
381
382	pr_debug("%s : wake_up &read_wq=%p\n", __func__, &mt6605_dev->read_wq);
383	pr_debug("mt6605_dev_irq_handler\n");
384}
```
##static int mt6605_dev_open(struct inode *inode, struct file *filp)
```C
561static int mt6605_dev_open(struct inode *inode, struct file *filp)
562{
563
564	struct mt6605_dev *mt6605_dev =
565	    container_of(filp->private_data, struct mt6605_dev, mt6605_device);
566
567	filp->private_data = mt6605_dev;
568	mt6605_dev_ptr = mt6605_dev;
569
570
571	pr_debug("mt6605_dev_open,%s : %d,%d, &mt6605_dev_open=%p\n", __func__, imajor(inode),
572		 iminor(inode), mt6605_dev_ptr);
573
574	/* 20121009,LiangChi add */
575	/* mt_set_gpio_out(mt6605_dev->ven_gpio, GPIO_OUT_ZERO); */
576	/* mt_set_gpio_out(mt6605_dev->sysrstb_gpio, GPIO_OUT_ONE); */
577
578    forceExitBlockingRead = 0;
579    return 0;
580}
```
##kernel log for example
```C
 17355 <7>[  437.400329]<7> (5)[2590:NfcMainThread][mt6605]mt6605_dev_write : writing 25 bytes, remain bytes 25.
 17356 <7>[  437.401109]<7> (5)[2590:NfcMainThread][mt6605]mt6605_dev_write : 25,25,25
 17357 <7>[  437.401120]<7> (5)[2590:NfcMainThread][mt6605]mt6605_dev_write : ret== count_ori
 17358 <7>[  437.401129]<7> (5)[2590:NfcMainThread][mt6605]mt6605_dev_write : writing 25 bytes. Status 25
 17359 <7>[  437.401246]<7>-(0)[0:swapper/0][mt6605]mt6605_dev_irq_handler : &mt6605_dev=ffffffc0013ee030
 17360 <7>[  437.401260]<7>-(0)[0:swapper/0][mt6605]mt6605_disable_irq : irq 144, enable=0
 17361 <7>[  437.401267]<7>-(0)[0:swapper/0][mt6605]mt6605_disable_irq
 17362 <7>[  437.401278]<7>-(0)[0:swapper/0][mt6605]mt6605_dev_irq_handler : wake_up &read_wq=ffffffc0013ee030
 17363 <7>[  437.401299]<7>-(0)[0:swapper/0][mt6605]mt6605_dev_irq_handler
 17364 <7>[  437.401303]<7> (1)[2589:NfcReadThread][mt6605]mt6605_dev_read : wait_event_interruptible ret 0,gpio,1
 17365 <7>[  437.402237]<7> (2)[2589:NfcReadThread]mt6605_dev_read : i2c_master_recv returned 32, IRQ, 0
 17366 <7>[  437.402251]<7> (2)[2589:NfcReadThread][mt6605]mt6605_dev_read: return,ret,32
 17367 <7>[  437.402413]<7> (2)[2589:NfcReadThread]mt6605_dev_read : mt_eint_unmask 144, IRQ, 0 
 17368 <7>[  437.402609]<7> (3)[2590:NfcMainThread][mt6605]mt6605_dev_write : writing 13 bytes, remain bytes 13.
 17369 <7>[  437.403049]<7> (1)[2590:NfcMainThread][mt6605]mt6605_dev_write : 13,13,13
 17370 <7>[  437.403058]<7> (1)[2590:NfcMainThread][mt6605]mt6605_dev_write : ret== count_ori
 17371 <7>[  437.403067]<7> (1)[2590:NfcMainThread][mt6605]mt6605_dev_write : writing 13 bytes. Status 13
 17373 <7>[  437.404015]<7> (0)[2590:NfcMainThread][mt6605]mt6605_dev_unlocked_ioctl,cmd,0x1,0x201
 17374 <7>[  437.404029]<7> (0)[2590:NfcMainThread][mt6605]mt6605_dev_unlocked_ioctl,0
 17418 <7>[  437.409188]<7> (1)[2590:NfcMainThread][mt6605]mt6605_dev_write : writing 1 bytes, remain bytes 1.
 17423 <7>[  437.409347]<7> (1)[2590:NfcMainThread][mt6605]mt6605_dev_write : 1,1,1
 17424 <7>[  437.409356]<7> (1)[2590:NfcMainThread][mt6605]mt6605_dev_write : ret== count_ori
 17425 <7>[  437.409365]<7> (1)[2590:NfcMainThread][mt6605]mt6605_dev_write : writing 1 bytes. Status 1
 17430 <7>[  437.410718]<7> (1)[2590:NfcMainThread][mt6605]mt6605_dev_write : writing 22 bytes, remain bytes 22.
 17433 <7>[  437.411577]<4> (5)[2590:NfcMainThread][mt6605]mt6605_dev_write : 22,22,22
 17434 <7>[  437.411594]<4>-(0)[1689:Binder_8][mt6605]mt6605_dev_irq_handler : &mt6605_dev=ffffffc0013ee030
 17435 <7>[  437.411606]<4>-(0)[1689:Binder_8][mt6605]mt6605_disable_irq : irq 144, enable=0
 17436 <7>[  437.411614]<4>-(0)[1689:Binder_8][mt6605]mt6605_disable_irq
 17438 <7>[  437.411636]<4> (5)[2590:NfcMainThread][mt6605]mt6605_dev_write : ret== count_ori
 17439 <7>[  437.411644]<4> (5)[2590:NfcMainThread][mt6605]mt6605_dev_write : writing 22 bytes. Status 22
 17440 <7>[  437.411654]<4>-(0)[1689:Binder_8][mt6605]mt6605_dev_irq_handler
 17441 <7>[  437.411722]<4> (5)[2590:NfcMainThread][mt6605]mt6605_dev_unlocked_ioctl,cmd,0x1,0x200
 17442 <7>[  437.411742]<4> (2)[2589:NfcReadThread][mt6605]mt6605_dev_read : wait_event_interruptible ret 0,gpio,1
 17443 <7>[  437.411751]<4> (5)[2590:NfcMainThread][mt6605]mt6605_dev_unlocked_ioctl,0
 17448 <7>[  437.412687]<4> (1)[2589:NfcReadThread]mt6605_dev_read : i2c_master_recv returned 32, IRQ, 1
 17449 <7>[  437.412699]<4> (1)[2589:NfcReadThread][mt6605]mt6605_dev_read: return,ret,32
 17451 <7>[  437.414032]<4> (7)[2589:NfcReadThread]mt6605_dev_read : i2c_master_recv returned 32, IRQ, 0
 17452 <7>[  437.414055]<4> (7)[2589:NfcReadThread][mt6605]mt6605_dev_read: return,ret,32
 17453 <7>[  437.414221]<4> (7)[2589:NfcReadThread]mt6605_dev_read : mt_eint_unmask 144, IRQ, 0 
 18066 <7>[  438.164726]<2> (4)[2590:NfcMainThread][mt6605]mt6605_dev_write : writing 13 bytes, remain bytes 13.
 18067 <3>[  438.164976]<2> (1)[2590:NfcMainThread][mt-i2c]ERROR,485: id=2,addr: 28, transfer error
 18068 <3>[  438.164988]<2> (1)[2590:NfcMainThread][mt-i2c]ERROR,491: I2C_ACKERR
 18069 <3>[  438.164997]<2> (1)[2590:NfcMainThread][mt-i2c]I2C(2) dump info++++++++++++++++++++++
 18070 <3>[  438.165018]<2> (1)[2590:NfcMainThread][mt-i2c]I2C structure:
 18074 <3>[  438.165041]<2> (1)[2590:NfcMainThread][mt-i2c]base address 0xffffff80038b4000
 18075 <3>[  438.165062]<2> (1)[2590:NfcMainThread][mt-i2c]I2C register:
 18079 <3>[  438.165099]<2> (1)[2590:NfcMainThread][mt-i2c]before enable DMA register(0x-549696470400):
 18083 <3>[  438.165136]<2> (1)[2590:NfcMainThread][mt-i2c]DMA register(0xffffff8003898280):
 18087 <3>[  438.165175]<2> (1)[2590:NfcMainThread][mt-i2c]I2C(2) dump info------------------------------
 18088 <3>[  438.165272]<2> (1)[2590:NfcMainThread][mt-i2c]ERROR,395: id=2,addr: 28, dma HW reset
 18089 <7>[  438.165306]<2> (1)[2590:NfcMainThread][mt6605]mt6605_dev_write : i2c_master_send returned 0
 19042 <7>[  438.993131]<3> (5)[2590:NfcMainThread][mt6605]mt6605_dev_unlocked_ioctl,cmd,0x1,0x201
 19043 <7>[  438.993150]<3> (5)[2590:NfcMainThread][mt6605]mt6605_dev_unlocked_ioctl,0
 19052 <7>[  438.998318]<7> (6)[2590:NfcMainThread][mt6605]mt6605_dev_write : writing 1 bytes, remain bytes 1.
 19053 <3>[  438.998452]<7> (1)[2590:NfcMainThread][mt-i2c]ERROR,485: id=2,addr: 28, transfer error
 19054 <3>[  438.998472]<7> (1)[2590:NfcMainThread][mt-i2c]ERROR,491: I2C_ACKERR
```
##container of
[typeof、offsetof、container_of的解释](http://blog.chinaunix.net/uid-27714502-id-3335236.html)

[container_of 用法解析](http://blog.csdn.net/beyondioi/article/details/6896206)
