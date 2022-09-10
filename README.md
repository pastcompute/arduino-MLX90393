# arduino-MLX90393
Arduino library for MLX90393 magnetometer sensor.

Extended to support the Raspberry Pi Pico / rp2040 SDK ecosystem.
To use with the Pico, setup the i2c first before calling `begin()` (example):

```
static void setupI2c(uint8_t sda, uint8_t scl) {
  i2c_init(i2c1, 1000 * 1000);
  gpio_set_function(sda, GPIO_FUNC_I2C);
  gpio_set_function(scl, GPIO_FUNC_I2C);
  gpio_pull_up(sda);
  gpio_pull_up(scl);
  // Make the I2C pins available to picotool
  bi_decl(bi_2pins_with_func(sda, scl, GPIO_FUNC_I2C));
}

int main() {
  auto t0 = to_ms_since_boot(get_absolute_time());
  stdio_init_all();
  setupI2c(6,7);
  mlx.begin(0,0,-1,i2c1);
```