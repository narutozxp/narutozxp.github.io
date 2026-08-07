---
title: 20250227组会汇报--efpga测试
author: narutozxp
date: 2025-02-26 20:45:27
permalink: slides/reports/20250227/report.html
layout: slides
---

# efpga测试汇报

---

## 测试环境搭建

`vscode` + `arm-none-eabi-gcc` + `openocd`便于后期开发调试。且便于于`efpga`的`vscode`插件进行集成。

---

## 测试结果

--

### SoC测试结果

* `ARM`运算操作正常（60MHz）
* `GPIO`运行正常
* `AHB`配置`efpga`正常
* `PLL`配置正常

--

### eFPGA测试结果

* 配置正常
* 组合逻辑运行正常
* `FF`、`全局rst`工作正常
* `23bit`计数器（使用`adder宏模块`）工作正常（`120MHz`）

---

## 已知问题

--

### SoC问题

* `SRAM`非*四字节对齐*写入错误
* `PA`-`PD`与`efpga out`的`pin`脚关联错误
* `SPI`缺少同步

--

### eFPGA问题

* `benchmark`中，信号驱动多个输出时会导致结果错误（软件问题？）
* 多时钟需要改进

--

### 玄学问题

* `rst`后没有从`RST_HANDLER`处开始执行
* 寄存器配置需要玄学延时
* 不可随意添加断点（会跑飞或者无效）
* 复杂程序执行问题

--

#### 程序问题举例

--

**正常工作**

```c
int main(void)
{
    ledInit();

    uint32_t test = PLL_CTRL_VAL;
    // seteFPGABitstreamMethod(EFPGA_BITSREAM_METHOD_AHB);
    seteFPGAIoOen((uint32_t*)EFPGA_CFG_IOE2H_OEN, PBF_Pin_4);
    uint32_t lodaed_num = loadBitstream(fabric_bitstream);

    delay();
    configClkEn();

    while (1);
}
```

--

**eFPGA配置无效 LED正常**

```c [13-15]
int main(void)
{
    ledInit();

    uint32_t test = PLL_CTRL_VAL;
    // seteFPGABitstreamMethod(EFPGA_BITSREAM_METHOD_AHB);
    seteFPGAIoOen((uint32_t*)EFPGA_CFG_IOE2H_OEN, PBF_Pin_4);
    uint32_t lodaed_num = loadBitstream(fabric_bitstream);

    delay();
    configClkEn();

    ledSet(0x00000001);
    delay();
    ledSet(0x00000000);

    while (1);
}
```

--

**eFPGA配置无效 LED异常**

```c [16-17]
int main(void)
{
    ledInit();

    uint32_t test = PLL_CTRL_VAL;
    // seteFPGABitstreamMethod(EFPGA_BITSREAM_METHOD_AHB);
    seteFPGAIoOen((uint32_t*)EFPGA_CFG_IOE2H_OEN, PBF_Pin_4);
    uint32_t lodaed_num = loadBitstream(fabric_bitstream);

    delay();
    configClkEn();

    ledSet(0x00000001);
    delay();
    ledSet(0x00000000);
    delay();
    ledSet(0x00000001);
    
    while (1);
}
```

---

## 补救措施

重新打板，使用系统时钟来同步`spi`的`sclk`。（有待验证）
