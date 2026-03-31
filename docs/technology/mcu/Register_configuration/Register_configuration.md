# 寄存器配置 Register configuration

> 平常对于MCU或者一些器件的寄存器进行配置时，如果直接使用寄存器的数值进行配置比较麻烦，每次都需要看手册，并且查看寄存器每个位的功能。
> 这里面说明一些使用结构体 + 枚举变量进行寄存器配置的方法


## .h 头文件
```c
// 1.定义 OSCCON 寄存器的地址 
// 通常MCU已经定义好了寄存器名称，不需要用户另外定义

// 通常器件未定义寄存器名称，只给出寄存器地址 需要用户定义
#define OSCCON (0x14)

// 2. 
// 查看手册，根据OSCCON寄存器 定义枚举
// 这样做的好处是代码自解释，不需要去查手册就能知道每个值代表什么
typedef enum {
    IRCF_32KHZ        = 0b000, // 32kHz 低频内部振荡器
    IRCF_FOSC_DIV_64  = 0b001, // Fosc / 64
    IRCF_FOSC_DIV_32  = 0b010, // Fosc / 32
    IRCF_FOSC_DIV_16  = 0b011, // Fosc / 16
    IRCF_FOSC_DIV_8   = 0b100, // Fosc / 8
    IRCF_FOSC_DIV_4   = 0b101, // Fosc / 4 (默认)
    IRCF_FOSC_DIV_2   = 0b110, // Fosc / 2
    IRCF_FOSC_DIV_0   = 0b111  // Fosc (全速)
} OSCCON_IRCF_t;


// 3. 
// 定义 OSCCON 寄存器的位结构体
// 用户配置时需使用
typedef struct {
    uint8_t reserved0  : 1; // Bit 0: 未用
    uint8_t SWDTEN     : 1; // Bit 1: 软件看门狗使能
    uint8_t reserved2  : 2; // Bit 2-3: 未用
    uint8_t IRCF       : 3; // Bit 4-6: 频率选择 (3位)
    uint8_t reserved7  : 1; // Bit 7: 未用
} OSCCON_Bits_t;

```

## 使用方法（代码示例）
```c
void OSCCON_INIT(void) {
    
    OSCCON_Bits_t temp_cfg; // 1. 定义一个临时变量
    
    // 2. 配置
    temp_cfg.SWDTEN = 0;
    temp_cfg.IRCF = IRCF_FOSC_DIV_4;
    
    OSCCON = temp_cfg.all;  // 3. 一次性写入寄存器
}
```