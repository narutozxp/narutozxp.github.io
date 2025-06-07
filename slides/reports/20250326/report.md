---
title: 20250326进展汇报
author: <img src="$reporoot-url$/markdown_revealjs/images/me.png" style="height:1.5em;">narutozxp<br/>
date: 2025年3月26日
headerl: <img src="$reporoot-url$/markdown_revealjs/themes/hust/hust_logo.svg" style="height:1.0em; margin:0;"><span style="color:#01378c; font-size:1.0em;">华中科技大学</span>
headerr: <span style="color:#01378c; font-size:1.0em;">集成电路学院</span><img src="$reporoot-url$/markdown_revealjs/themes/hust/ic_logo.jpg" style="height:1.0em; margin:0;">
footerl: <span style="color:#01378c; font-size:0.6em;">narutozxp・2025年3月26日</span>

title-slide-background-image:  $reporoot-url$/markdown_revealjs/themes/ucas_ict_thesis/liquid-cheese_sky_title.svg
toc-slide-background-image:    $reporoot-url$/markdown_revealjs/themes/ucas_ict_thesis/liquid-cheese_sky_l1.svg
level1-slide-background-image: $reporoot-url$/markdown_revealjs/themes/ucas_ict_thesis/liquid-cheese_sky_l1.svg
level2-slide-background-image: $reporoot-url$/markdown_revealjs/themes/ucas_ict_thesis/liquid-cheese_sky_l2.svg
level3-slide-background-image: $reporoot-url$/markdown_revealjs/themes/ucas_ict_thesis/liquid-cheese_sky_l3.svg
background-size: cover

pandoc-opts: "--toc=false"
---

# Yosys综合

## 综合鲁棒性

* 支持赋初值`reg a = 0;`操作
* 支持ROM综合
* 支持异步低电平置位
* 单口ram/双口ram(transparent or non-transparetn)

# VTR Benchmark评估

## 资源消耗

![资源消耗](./img/vtr_benchmark.png)

# Adder Threshold测试

## 基于simple Adder

![面积延迟结果](./img/simple_add.png)

## 基于VTR Benchmark的测试

![延迟与阈值的关系](./img/delay.png)

## 

![CLB数量与阈值的关系](./img/clbs.png)

## 

![FLE数量与阈值的关系](./img/fles.png)

## 

**综合Simple与VTR测试的结果，后续将阈值定为16**


# 谢谢 {.slide-count-end data-background-image="$reporoot-url$/markdown_revealjs/themes/ucas_ict_thesis/liquid-cheese_sky_title.svg" data-sminvisible=true}

