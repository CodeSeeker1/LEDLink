# LEDLink

<h2>Project Objective</h2> 
Control the onboard LEDs of the CC1350 Launchpad through Bluetooth using the nRF Connect app. The CC1350 will be programmed to receive commands over Bluetooth Low Energy(BLE) to turn the LEDs on and off.

<h2>Components of the project</h2>

   - TI SimpleLink CC1350 Wireless MCU Launchpad Development Kit
   - Code Composer Studio
   - nRF Connect app (available on iOS and Android)

<h2>Step-by-Step Approach</h2>
<h3>Step 1: Setup the Development Environment</h3>

1. Install Code Composer Studio:
   - Download and install Code Composer Studio from Texas Instruments' website.

2. Set Up the TI SimpleLink SDK:
   - Download the SimpleLink SDK that includes examples and libraries for the CC1350.
   - Set up the SDK in Code Composer Studio by creating a new project.

<h3>Step 2: Link Necessary Libraries for LED and Bluetooth Control</h3>
- Include the necessary headers for GPIO and BLE functionalities:

```c
#include "driverlib/prcm.h"
#include "driverlib/rf_ble_cmd.h"
#include "driverlib/gpio.h"
```
- Power on their domains:

```c
// Power on the GPIO and RF core domains
void powerOnDomains(void) {
    PRCMPowerDomainOn(PRCM_DOMAIN_PERIPH); // Enable GPIO domain
    while (PRCMPowerDomainStatus(PRCM_DOMAIN_PERIPH) != PRCM_DOMAIN_POWER_ON);

    PRCMPowerDomainOn(PRCM_DOMAIN_RFCORE); // Enable RF core domain
    while (PRCMPowerDomainStatus(PRCM_DOMAIN_RFCORE) != PRCM_DOMAIN_POWER_ON);
}
```

<h3>Step 3: Upload the Code to the CC1350</h3>
<h3>Step 4: Connect Device to nRF Connect App</h3>

1. Explore Services:
   - After connecting, you will see a list of services exposed by your CC1350. Look for the LED control service.

2. Send Commands:
   - Write the following commands to control the LEDs:
   - **Turn on LED1**: Send `0x01`
   - **Turn off LED1**: Send `0x02`
   - **Turn on LED2**: Send `0x03`
   - **Turn off LED2**: Send `0x04`

3. Monitor Responses:
   - If implemented, you can receive feedback from the CC1350 on the app when the LEDs change state.
