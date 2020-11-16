# RPI-HD44780-I2C-Lib
https://github.com/joesphan/RPI-HD44780-I2C-Lib

raspberry pi hd44780 i2c python library

Forked from https://gist.github.com/DenisFromHR/cc863375a6e19dce359d

## Documentation

The following below is all in example.py

##### Object initiation:

```python
mylcd = I2C_LCD_driver.lcd(bus, address)
```

To find the address, run:

```bash
sudo i2cdetect -y $bus
```

Where $bus = the I2C channel (usually 1 on the Pi)

##### Write String Function:

```python
mylcd.lcd_display_string_pos("Hello World!", row, column)
```

Where row = start row on the LCD, and column = start column of LCD

##### Clear:

```Pythong
mylcd.lcd_clear()
```

##### Custom Fonts:

creating a font:

```python
fontdata1 = [
        # Char 0 - Upper-left
        [ 0x00, 0x00, 0x03, 0x04, 0x08, 0x19, 0x11, 0x10 ],
        # Char 1 - Upper-middle
        [ 0x00, 0x1F, 0x00, 0x00, 0x00, 0x11, 0x11, 0x00 ],
        # Char 2 - Upper-right
        [ 0x00, 0x00, 0x18, 0x04, 0x02, 0x13, 0x11, 0x01 ],
        # Char 3 - Lower-left
        [ 0x12, 0x13, 0x1b, 0x09, 0x04, 0x03, 0x00, 0x00 ],
        # Char 4 - Lower-middle
        [ 0x00, 0x11, 0x1f, 0x1f, 0x0e, 0x00, 0x1F, 0x00 ],
        # Char 5 - Lower-right
        [ 0x09, 0x19, 0x1b, 0x12, 0x04, 0x18, 0x00, 0x00 ],
        # Char 6 - my test
		[ 0x1f,0x0,0x4,0xe,0x0,0x1f,0x1f,0x1f],
]


```

initiating:

```python
mylcd.lcd_load_custom_chars(fontdata1)
```

writing custom font 0, 1, and 2 to row 1:

```python
mylcd.lcd_write(0x80)
mylcd.lcd_write_char(0)
mylcd.lcd_write_char(1)
mylcd.lcd_write_char(2)
```

writing custom font 3, 4, and 5 to row 2:

```python
mylcd.lcd_write(0xC0)
mylcd.lcd_write_char(3)
mylcd.lcd_write_char(4)
mylcd.lcd_write_char(5)
```

##### Backlight:

off:

```python
mylcd.backlight(0)
```

on:

```python
mylcd.backlight(1)
```

##### Low level custom commands:

```python
mylcd.lcd_write($command)
```

HD44780 specific commands:

```python

# commands
LCD_CLEARDISPLAY = 0x01
LCD_RETURNHOME = 0x02
LCD_ENTRYMODESET = 0x04
LCD_DISPLAYCONTROL = 0x08
LCD_CURSORSHIFT = 0x10
LCD_FUNCTIONSET = 0x20
LCD_SETCGRAMADDR = 0x40
LCD_SETDDRAMADDR = 0x80

# flags for display entry mode
LCD_ENTRYRIGHT = 0x00
LCD_ENTRYLEFT = 0x02
LCD_ENTRYSHIFTINCREMENT = 0x01
LCD_ENTRYSHIFTDECREMENT = 0x00

# flags for display on/off control
LCD_DISPLAYON = 0x04
LCD_DISPLAYOFF = 0x00
LCD_CURSORON = 0x02
LCD_CURSOROFF = 0x00
LCD_BLINKON = 0x01
LCD_BLINKOFF = 0x00

# flags for display/cursor shift
LCD_DISPLAYMOVE = 0x08
LCD_CURSORMOVE = 0x00
LCD_MOVERIGHT = 0x04
LCD_MOVELEFT = 0x00

# flags for function set
LCD_8BITMODE = 0x10
LCD_4BITMODE = 0x00
LCD_2LINE = 0x08
LCD_1LINE = 0x00
LCD_5x10DOTS = 0x04
LCD_5x8DOTS = 0x00

# flags for backlight control
LCD_BACKLIGHT = 0x08
LCD_NOBACKLIGHT = 0x00
```

Original Library by [Denis Pleic](https://gist.github.com/DenisFromHR)

changes by Joesphan Lu:

- enabled initiating of address and bus via .lcd initiation