# Modem AT Commands

    AT&V                                      Status

    ATI                                       Manufacturer, model, firmware version, IMEI, capabilities
    AT+CGMI                                   Name of manufacturer
    AT+CGMM                                   Model number
    AT+CGMR                                   Firmware version
    AT+CGSN                                   IMEI number (International Mobile Equipment Identity)
    AT+CIMI                                   IMSI number of SIM card (International Mobile Subscriber Identity)

    AT^HWVER                                  Hardware version

    AT+CPAS                                   Mobile phone activity status
    AT+CREG                                   Mobile network registration status
    AT+CSQ                                    Radio signal strength
    AT+CBC                                    Battery charge level and charging status


    ATD
    ATA
    AT+F*

    AT+COPS=?                                 List available networks: (0-Unknown/2-Current/3-Forbidden, Longname, Shortname, Numerical ID, "AcT")

    ATSn?                                     Read value of register n
    ATSn=x                                    Write value to register n

    ATVn                                      Set result code format: 0-numerical, 1-string

    ATZ0                                      Reset the modem, use stored profile 0
    ATZ1                                      Reset the modem, use stored profile 1

    AT&Fn                                     Restore modem to factory settings: 0-profile0, 1-profile1

    AT^GETPORTMODE                            List all devices in the modem
    AT^SETPORT=?                              Get available port modes
    AT^SETPORT?                               Get port configuration
    AT^SETPORT="..."                          Set port configuration

    AT^VERSION                                Version of the modem firmware

    AT+CLAC                                   List of supported commands

### S-Registers

    S0  (0-255)                               Auto answer: number of rings required before answer call, 0 disables auto-answer mode
    S1  (0-255)                               Ring counter: incremented each time modem detects a ring signal
    S2  (0-127, default: 43)                  Escape character: >127 disables escape process
    S3  (0-127, default: 13)                  Carriage return character
    S4  (0-127, default: 10)                  Line feed character
    S5  (0-32,  default: 8)                   Backspace character
