# 电控组第二次培训作业
- **宁彦博**
- ***20253003139***
### 基础部分(homework002)：依靠hal_delay函数实现了流水灯
## 非阻塞延时加分项(homework0022):
### 实现原理：依靠计时器中断，配置计时器使其每0.5s发送一次中断。在中断回调函数中主要依靠包含3种case的switch函数来实现流水灯。
### 核心代码：  
```c
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim)
{
  if (htim->Instance == TIM3)
  {
    static uint8_t i = 0;

    switch (i)
    {
      case 0:
        {
          HAL_GPIO_WritePin(LED0_GPIO_Port,LED0_Pin,GPIO_PIN_SET);
          HAL_GPIO_WritePin(LED1_GPIO_Port,LED1_Pin,GPIO_PIN_RESET);
          HAL_GPIO_WritePin(LED2_GPIO_Port,LED2_Pin,GPIO_PIN_RESET);
          break;
        }
      case 1:
        {
          HAL_GPIO_WritePin(LED0_GPIO_Port,LED0_Pin,GPIO_PIN_RESET);
          HAL_GPIO_WritePin(LED1_GPIO_Port,LED1_Pin,GPIO_PIN_SET);
          HAL_GPIO_WritePin(LED2_GPIO_Port,LED2_Pin,GPIO_PIN_RESET);
          break;
        }
      case 2:
        {
          HAL_GPIO_WritePin(LED0_GPIO_Port,LED0_Pin,GPIO_PIN_RESET);
          HAL_GPIO_WritePin(LED1_GPIO_Port,LED1_Pin,GPIO_PIN_RESET);
          HAL_GPIO_WritePin(LED2_GPIO_Port,LED2_Pin,GPIO_PIN_SET);
          break;
        }
    }

    i++;

    if (i==3) i=0;

  }
}