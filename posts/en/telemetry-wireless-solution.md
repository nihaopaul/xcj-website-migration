---
id: 339
title: ART Telemetry wireless solution
date: 2011-01-09 01:56:13
author: 4
---

Been researching wireless solutions to transmit in real-time sensor and decision information from ART in addition to possibly enabling minimal controls (on/off/behavior switch) and perhaps even wireless firmware updates.

My criteria:

* Low-cost (<200RMB, preferably <100RMB)
* Simplex or half-duplex OK
* Low-bandwidth (>1,200 bit/s)
* Low-power (<100 mAh)
* Medium-range (500m-1000m)
* TTL or SPI interface

One of the main issue is that I cannot find a clear reference to the spectrum allocation in China (The US has a very convenient Frequency Allocations Chart: <http://en.wikipedia.org/wiki/Frequency%5Fallocation>).

I know that 2.4Ghz is good worldwide (such as what the Nordic nRF240L uses) but that has a very limited range (50m-100m). So is Bluetooth and to a certain degree Wifi (and they are pretty expensive too).

There are these:

* PTR8000+ [Nordic nRF905 (433/868/915MHz)]
   * <http://www.nordicsemi.com/index.cfm?obj=product&act=display&pro=83>
   * <http://item.taobao.com/item.htm?id=6062297954> (50RMB!)
   * <http://www.techtoys.com.hk/RF%5FModules/Nordic%5F905/nRF905%5Frev1%5F4.pdf>
   * tops out at 500m LOS
* Laipac Tech RF 900DV(900 mhz)
   * <http://www.laipac.com/easy%5F900dv%5Feng.htm>
* Laipac ASK Transmitters (315 mhz)
   * <http://www.laipac.com/easy%5F900dv%5Feng.htm>
* Databridge
   * <http://www.starmanelectric.com/OrderDataBridge/tabid/71/Default.aspx>
   * <http://www.starmanelectric.com/LinkClick.aspx?fileticket=REf/38lk/L4%3d&tabid=75&mid=456>
   * Expensive (87$USD) and not available here?
* JZ871 Data RF transceiver for wireless telemetry system (433 MHz or 868Mhz/915Mhz)
   * <http://www.alibaba.com/product-gs/252550553/RF_data_transceiver.html>
   * <http://www.jizhuo.com/download/product%5Fimages/f/cn%5Ff%5F%5F101.pdf>
   * I'm guessing if Alibaba is selling it, it's ok in China? Or is it exactly just an export product?

Last one actually looks better than the Nordic on paper, but from what I gathered the price is pretty high. I wonder about the price and why I can't find it on Taobao...