.. module:: mcp4921

****************
 MCP4921 Module
****************

This module contains the driver for Microchip MCP4921 single channel 12-bit digital to analog converter
with SPI serial interface (`datasheet <http://ww1.microchip.com/downloads/en/DeviceDoc/22248a.pdf>`_).

Example: ::

        from microchip.mcp4921 import mcp4921

        ...

        mcp = mcp4921.MCP4921(SPI0, D17)
        mcp.set_value(1600)

    
===============
 MCP4921 class
===============


.. class:: MCP4921(spidrv, cs, clk = 400000)

    Creates an instance of the MCP4921 class.

    :param spidrv: SPI Bus used '(SPI0, ...)'
    :param cs: Chip select pin
    :param clk: Clock speed, default 400 kHz

    
.. method:: set_value(v, gain = 1, buff = False)

    Sends the 12-bit value *v* to the DAC. The gain of the output amplifier can be set through *gain* parameter,
    valid values are ``1`` and ``2``.

    Analog Output Voltage = ( v / 4096) * Vref * gain 

    If *buff* is ``True``, the device buffers the Voltage Reference input increasing the input impedance but limiting
    the input range and frequency response. If *buff* is ``False`` the input range is wider (from 0V to Vdd) and the 
    typical input impedence is 165 kOhm with 7pF.
    If in Shutdown mode, the device is changed to Active mode. In this case the output settling time
    increases to 10 us.
.. method:: shutdown()

    Shutdown the device. During Shutdown mode, most of the internal circuits are turned off for 
    power savings and there will be no analog output.
