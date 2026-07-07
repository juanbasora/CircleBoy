# CircleBoy
CirlceBoy is a small circuit board that lets you replace the directional pad on a gameboy or other device with an analog joystick. CircleBoy was designed specifically to use the 3DS circle pad with a gameboy, but is adaptable to tons of use cases.

## Installation Gallery
A gallery of my installation of the board can be [found here](https://imgur.com/a/vMOLDO8).

## Hardware

Description | link
--- | ---
0603 0.1uf cap | [Mouser](https://www.mouser.com/ProductDetail/KYOCERA-AVX/0603ZD104KAT2A?qs=sGAEpiMZZMukHu%252BjC5l7YduOrE6ID6FF2yJLQZUxOqI%3D)
board | [Oshpark](https://oshpark.com/shared_projects/1QXsRf0p)
ribbon connector | [Aliexpress](https://www.aliexpress.us/item/3256805824448382.html?src=google&src=google&albch=shopping&acnt=708-803-3821&isdl=y&slnk=&plac=&mtctp=&albbt=Google_7_shopping&aff_platform=google&aff_short_key=UneMJZVf&gclsrc=aw.ds&albagn=888888&ds_e_adid=&ds_e_matchtype=&ds_e_device=c&ds_e_network=x&ds_e_product_group_id=&ds_e_product_id=en3256805824448382&ds_e_product_merchant_id=109236776&ds_e_product_country=US&ds_e_product_language=en&ds_e_product_channel=online&ds_e_product_store_id=&ds_url_v=2&albcp=20269108796&albag=&isSmbAutoCall=false&needSmbHouyi=false&gad_source=1&gad_campaignid=20273564092&gbraid=0AAAAAD6I-hFzlTf9eqbyt6xE9TfjUS78W&gclid=CjwKCAjwpK3SBhASEiwAtV1SPP48zSA_-ffP9JzkqHkfxDD8He2VcK_6ciWoUCsMmL7DUkOQjVJ_DhoCLOAQAvD_BwE&gatewayAdapt=glo2usa)
Attiny85 SOIC package | [Aliexpress example](https://www.aliexpress.us/item/3256811777632799.html?spm=a2g0o.productlist.main.43.51521e941e94YE&algo_pvid=186b4e06-d721-4894-8d3f-a62d102852c8&algo_exp_id=186b4e06-d721-4894-8d3f-a62d102852c8-42&pdp_ext_f=%7B%22order%22%3A%22-1%22%2C%22eval%22%3A%221%22%2C%22fromPage%22%3A%22search%22%7D&pdp_npi=6%40dis%21USD%213.19%213.19%21%21%2121.56%2121.56%21%4021032f3717833838713434118e046b%2112000057157424556%21sea%21US%21715054283%21X%211%210%21n_tag%3A-29919%3Bd%3Ab2d6a199%3Bm03_new_user%3A-29895&curPageLogUid=sNUJ0UGoJfY1&utparam-url=scene%3Asearch%7Cquery_from%3A%7Cx_object_id%3A1005011963947551%7C_p_origin_prod%3A)

## Configuration
You can select between 4 different modes for the stick. Modes are selected by shorting out the dpad contacts in the appropriate direction when you turn the system on. The configuration is stored in the EEPROM of the chip, so you only have to set it once.

Direction | Deadzone | Segments
--- | --- | ---
Up (default) | Small | Balanced
Down          | Large | Balanced
Left          | Small | 3/4 Straight, 1/4 Diagonals
Right         | Large | 3/4 Straight, 1/4 Diagonals

## ATtiny85 Fuses
Since this project uses the reset line on the ATtiny85, once you've written the firmware and enabled the `NO_GOING_BACK_NOW` macro, you'll need to disable the reset on the chip. I did this on my Mac with
```
/Applications/Arduino.app/Contents/Java/hardware/tools/avr/bin/avrdude -C/Applications/Arduino.app/Contents/Java/hardware/tools/avr/etc/avrdude.conf -v -v -v -v -pattiny85 -carduino -P/dev/cu.usbmodem143301 -b19200 -Uhfuse:w:0x5f:m
```
The important part of that is setting the hfuse to 0x5f.

