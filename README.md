# PWM-BRIGHTNESS-LEVEL
Analyse the relationship between PWM duty cycle and LED brightness by gradually varying the brightness from 0% to 100% and then from 100% to 0%. Observe the resulting breathing effect. 
---

## Apparatus Required

| S. No. | Apparatus / Software | Specification |
|:---:|---|---|
| 1 | Microcontroller Development Board | **NXP S32K144 Development Board** |
| 2 | IDE | **S32 Design Studio** |
| 3 | Programming Language | **Embedded C** |
| 4 | SDK | **S32K144 SDK** |
| 5 | LED | On-board LED / External LED |
| 6 | Programmer / Debugger | On-board Debugger / OpenSDA |
| 7 | USB Cable | For programming and power supply |

---
## Procedure
1. Connect the S32K144 Development Board to the computer using a USB cable.
2. Open S32 Design Studio.
3. Create a new project for the S32K144 microcontroller.
4. Select and configure the appropriate S32K144 SDK for the project.
5. Identify the GPIO pin connected to the LED on the S32K144 development board.
6. Configure the selected GPIO pin/Drivers as a Digital Output/input.
7. Initialize the required GPIO peripheral using the GPIO initialization functions provided by the S32K144 SDK.
8. Write the Embedded C program to control the LED using the GPIO Toggle-Pin API.
9. Insert a one-second delay between successive GPIO toggle operations.
10. The program should continuously execute the following sequence.
11. Build the project in S32 Design Studio.
12. Verify that the project is compiled successfully without errors.
13. Connect the debugger/programmer to the S32K144 Development Board.
14. Download the generated program to the S32K144 microcontroller.
15. Run the program on the S32K144 board.

---
## Program
```
#include "sdk_project_config.h"
int main(void)
{
	CLOCK_DRV_Init(&clockMan1_InitConfig0);
	PINS_DRV_Init(NUM_OF_CONFIGURED_PINS0,g_pin_mux_InitConfigArr0);
	PWM_Init(&pwm_pal_1_instance,&pwm_pal_1_configs);
	while(1)
	{
		for(int i=0;i<500;i++)
		{
			PWM_UpdateDuty(&pwm_pal_1_instance,0U,i);
			OSIF_TimeDelay(10);
		}
		for(int i=500;i>0;i--)
		{
			PWM_UpdateDuty(&pwm_pal_1_instance,0U,i);
			OSIF_TimeDelay(10);
		}
	}
}

```
---
## OUTPUT
<img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/37201a81-6f55-477a-a061-8c58ad618705" />


---
## Result

The relationship between the **PWM duty cycle and LED brightness** was successfully analyzed. The LED brightness increased gradually from **0% to 100%** as the PWM duty cycle increased and decreased gradually from **100% to 0%** as the duty cycle decreased, producing a smooth **breathing effect**.
