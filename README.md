# **Daisy Seed Breakout PCBs**

Handy Breakout PCBs for the electrosmith Daisy Seed that can be very helpful for prototyping,\
especially when working with eurorack signals.

- DC DC converter and input / output opamps board
  [Easy EDA project](https://oshwlab.com/scape_rob/seed_power_opamps)
- Eight channel input protection and multiplexer board 
  [Easy EDA project](https://oshwlab.com/scape_rob/kxmx_bluemchen_copy)

[Microsite](https://www.robertheel.com/++/daisy-seed-breakout-boards/) with relevant links.
 
 
 ![daisy_seed_breakouts](https://www.robertheel.com/++/wp-content/uploads/2025/09/seed_dcdc_and_muxes.jpg) 
 
  
 # DC DC converter and input output opamps board
DC DC converter from +/- 12 Volts eurorack power to +5 Volts.\
Opamps for audio in and audio out, eurorack level.

 ![daisy_seed_breakouts](https://www.robertheel.com/++/wp-content/uploads/2025/08/seed_dcdc_01.jpg) 

When using long headers it can be plugged into a breadboard for fast prototyping\
while using the clean power and the op amps.

 ![daisy_seed_breakouts](https://www.robertheel.com/++/wp-content/uploads/2025/09/seed_breadboard_01.jpg) 

Bit fiddly to install on breadboard, but once in place worth the hassle.\
To install on breadboard i use long female headers.\
Daisy seed with normal male headers plugs in the female headers,\
female headers through PCB plug into breadboard. 


 
 # Eight channel input protection and multiplexer board 
Scales Eurorack level -/+ 5 Volts to safe 0 - 3.3 Volts, these scaled signals can be used directly
or via the multiplexer thats on board. 


 ![daisy_seed_breakouts](https://www.robertheel.com/++/wp-content/uploads/2025/08/seed_mcp6004_mux_screen_01.jpg) 

 
# C++ abstraction to use with unipolar LFOs

I use a lot of Arduino based unipolar LFOs. In order to get full parameter range with
these unipolar LfOs, but also be able to use bipolar LFOs i use this abstraction.

```

    // center 1.64 volt from mcp6004 input protection + Dead zone to prevent tiny floating
    inline float bipolar_center_mod(uint16_t adc_val, uint16_t center = 32768)
    {
        int deviation = abs((int)adc_val - (int)center);
        if(deviation < 100) // ~1% deadzone = 100
            return 0.0f;
        return daisysp::fclamp((float)deviation / (float)center, 0.0f, 1.0f);
    }
```

 ![daisy_seed_breakouts](https://www.robertheel.com/++/wp-content/uploads/2025/08/seed_muxes_002.jpg) 


# Max Gen abstraction to use with unipolar LFOs

In max gen this abstraction should do the trick, with or without deadzone.

 ![daisy_seed_breakouts](https://www.robertheel.com/++/wp-content/uploads/2025/08/max_gen_unipolar.png) 
 

These breakout boards helped me tremendously while developing DSP audio on the Daisy Seed and interfacing with eurorack. 

 ![daisy_seed_breakouts](https://www.robertheel.com/++/wp-content/uploads/2025/08/seed_dcdc-and-mux.jpg) 


# Open source

The daisy seed breakout boards are an open source project.\
The schematics and PCB designs are licenced as CC BY-NC-SA 4.0.

For the daisy seed power management and op amps i refered to:\
kxmx [blümchen](https://kxmx-bluemchen.recursinging.com/)\
daisy patch by [electrosmith](https://daisy.nyc3.cdn.digitaloceanspaces.com/products/patch/ES_Daisy_Patch_Rev8.pdf)

For input protection:\
kxmx [blümchen](https://kxmx-bluemchen.recursinging.com/)\
Mutable instruments [clouds](https://pichenettes.github.io/mutable-instruments-documentation/modules/clouds/downloads/clouds_v30.pdf) 

For multiplexing:\
Takumi Ogata electrosmith [tutorial](https://forum.electro-smith.com/t/cd4051-multiplexer-tutorial-is-here/3481)

Code examples: MIT license\
Hardware: CC BY-NC-SA 4.0

[Microsite](https://www.robertheel.com/++/daisy-seed-breakout-boards/) with relevant links.
