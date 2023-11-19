# grapple-m24c64
A Rust embedded-hal driver for the M24C64 I2C EEPROM, featuring arbitrary-length read/writes and timeout behaviour.

## Add to your project
```
cargo add grapple-m24c64
```

## Examples
```rust
use grapple_m24c64::M24C64;

let eeprom = M24C64::new(i2c, 0b000);
eeprom.write(0xA0, &[0x00, 0x01, 0x02, 0x03], &delay);

let mut my_buf = [0u8; 4];
eeprom.read(0xA0, &mut my_buf);
// my_buf = [0x00, 0x01, 0x02, 0x03]
```

Note the use of [`embedded_hal::blocking::delay::DelayMs`], which is used to retry the write every 1ms until it either succeeds, or 10ms has passed (2*t_w in the M24C64 datasheet).